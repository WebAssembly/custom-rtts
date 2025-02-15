# Custom RTTs and JS Interop for WasmGC Structs

This proposal primarily provides mechanisms to:

 1. Save memory in WasmGC structs by allowing data associated with source types
    (e.g. static fields, vtables, itables, etc.)
    to be stored alongside the engine-managed type information
    in a custom runtime type object (RTT) for their corresponding WebAssembly types.
    Rather than using a user-controlled reference field
    to point to this type-associated information,
    structs can now use the RTT reference in their engine-managed header
    to refer to this information.

 1. Associate JS prototypes with WasmGC structs by storing them on the custom RTT,
    allowing methods to be called on WasmGC structs from JS.

Secondarily, this proposal provides mechanisms
to alleviate anticipated problems that will arise from the use of its primary features:

 1. A way to declaratively populate JS prototypes with wrapped exported functions
    to reduce startup time when there are many prototypes to populate.

 2. A way to deduplicate lists of fields in type sections.
    Using custom RTTs may otherwise lead to more duplication in the type section
    than there is today.

We should validate that these problem actually arise in practice and quantify their cost
before we commit to including these extra solutions in the final version of the proposal.

## Custom RTT Definitions

Custom RTT types are defined struct types with a `describes` clause saying
what other defined struct type they contain runtime type information for.
Similarly, struct types that use custom RTTs have a `descriptor` clause saying
what type their custom RTTs have.

> Note: If we want to lean into the "RTT" terminology, `describes` and `descriptor`
> could instead be `rtt-for` and `with-rtt` or similar.

```wasm
(rec
  (type $foo (struct (descriptor $foo.rtt) (field ...)))
  (type $foo.rtt (struct (describes $foo) (field ...)))
)
```

Note that because the definitions of the describing and described types
must refer to each other,
they must be in a recursion group with each other.

Just like all other parts of a type definition,
`descriptor` and `describes` clauses are part of the structure of a type definition
and help determine the type's identity.

In the following example,
types `$A` and `$B` are the same,
but type `$C` is different.

```wasm
(rec
  (type $A (struct (descriptor $A.rtt) (field i32)))
  (type $A.rtt (struct (describes $A) (field i32)))
)

(rec
  (type $B (struct (descriptor $B.rtt) (field i32)))
  (type $B.rtt (struct (describes $B) (field i32)))
)

(rec
  ;; Different: no describes or descriptor clauses.
  (type $C (struct (field i32)))
  (type $C.rtt (struct (field i32)))
)
```

A type may have both `descriptor` and `describes` clauses,
creating arbitrarily long chains of meta-descriptors:

```wasm
(rec
  (type $foo (struct (descriptor $foo.rtt)))
  (type $foo.rtt (struct (describes $foo) (descriptor $foo.meta-rtt)))
  (type $foo.meta-rtt (struct (describes $foo.rtt)))
)
```

> Note: If engines encounter difficulties implementing this,
> we can alternatively disallow types from having
> both `describes` and `descriptor` clauses.

`descriptor` and `describes` clauses must agree,
i.e. a describing type must have a `describes` clause referring to its described type,
which in turn must have a `descriptor` clause referring to the describing type.

```wasm
(rec
  (type $A (struct))
  (type $B (struct (descriptor $C)))
  (type $C (struct (describes $A))) ;; Invalid: must be 'describes $B'
)
```

> Note: This rule means that the `describes` clause is redundant
> and could be inferred from the existence of the `descriptor` clause,
> but we require the `describes` clause anyway so the layout of the custom RTT type
> can be determined just by looking at its definition.

It is also invalid for a type to be its own descriptor,
or more generally for it to appear in its descriptor chain.
This is statically enforced by validating that `describes` clauses may only refer
to previously defined types.
This is the same strategy we use for ensuring supertype chains do not have cycles.

```wasm
(rec
  ;; Invalid describes clause: $self is not a previously defined type.
  (type $self (struct (describes $self) (descriptor $self)))

  ;; Invalid describes clause: $pong is not a previously defined type.
  (type $ping (struct (describes $pong) (descriptor $pong)))
  (type $pong (struct (describes $ping) (descriptor $ping)))

  ;; Invalid describes clause: $foo is not a previously defined type.
  (type $foo.rtt (struct (describes $foo)))
  (type $foo (struct (descriptor $foo.rtt)))
)
```

Just like any other struct types,
struct types with `describes` or `descriptor` clauses support width and depth subtyping.
However, the following new subtyping rules are introduced:

 - A declared supertype of a type with a `(descriptor $x)` clause must either
   not have a `descriptor` clause or have a `(descriptor $y)` clause,
   where `$y` is a declared supertype of `$x`.

 - A declared supertype of a type without a `descriptor` clause must also
   not have a `descriptor` clause.

 - A declared supertype of a type with a `describes` clause must have a
   `describes` clause.

 - A declared supertype of a type without a `describes` clause must also
   not have a `describes` clause.

The first two rules,
governing types with or without `descriptor` clauses,
are necessary to ensure the soundness of the `ref.get_rtt` instruction described below.
The latter two rules,
governing types with or without `describes` clauses,
are necessary to ensure subtypes have layouts compatible with their supertypes.
Custom RTT types (i.e. those with `describes` clauses)
have different layouts than other structs because their user-controlled fields
are laid out after the engine-managed RTT for the type they describe.

```wasm
(rec
  (type $super (sub (struct (descriptor $super.rtt))))
  (type $super.rtt (sub (struct (describes $super))))

  ;; Ok
  (type $sub (sub $super (struct (descriptor $sub.rtt))))
  (type $sub.rtt (sub $super.rtt (struct (describes $sub))))
)

(rec
  (type $super (sub (struct)))

  ;; Ok
  (type $sub (sub $super (struct (descriptor $sub.rtt))))
  (type $sub.rtt (struct (describes $sub)))
)

(rec
  (type $super (sub (struct (descriptor $super.rtt))))
  (type $super.rtt (sub (struct (describes $super))))

  ;; Ok (but strange)
  (type $other (struct))
  (type $sub.rtt (sub $super.rtt (struct (describes $other))))
)

(rec
  (type $super (sub (struct (descriptor $super.rtt))))
  (type $super.rtt (sub (struct (describes $super))))

  ;; Invalid: Must be described by an immediate subtype of $super.rtt.
  (type $sub (sub $super (struct)))

  ;; Invalid: Must describe an immediate subtype of $super.
  (type $sub.rtt (sub $super.rtt (struct)))
)

(rec
  (type $super (sub (struct (descriptor $super.rtt))))
  (type $super.rtt (sub (struct (describes $super))))

  ;; Invalid: $other.rtt must be a an immediate subtype of $super.rtt.
  (type $sub (sub $super (struct (descriptor $other.rtt))))
  (type $other.rtt (struct (describes $sub)))
)
```

> Note: We could also allow types with `(descriptor none)` clauses,
> which would have no associated RTT at all,
> saving even more space.
> Casts to these types would always fail,
> so lost type information would never be able to be recovered for these types.
> This would make certain code patterns and transformations incorrect only for these types,
> so they may be more trouble than they are worth.

## Exact Reference Types

Allocating an instance of a type with a custom RTT necessarily
requires supplying a custom RTT value.
Specified naively,
this could allow the following unsound program to validate and run:

```wasm
(rec
  (type $foo (sub (struct (descriptor $foo.rtt))))
  (type $foo.rtt (sub (struct (describes $foo))))

  (type $bar (sub $foo (struct (descxriptor $bar.rtt) (field $bar-only i32))))
  (type $bar.rtt (sub $foo.rtt (struct (describes $bar))))
)

(func $unsound (result i32)
  (local $rtt (ref $foo.rtt))
  ;; We can store a $bar.rtt in the local due to subtyping.
  (local.set $rtt (struct.new $bar.rtt))
  ;; Allocate a $foo with a $foo.rtt that is actually a $bar.rtt.
  (struct.new $foo (local.get $rtt))
  ;; Now cast the $foo to a $bar. This will succeed because it has an RTT for $bar.
  (ref.cast (ref $bar))
  ;; Out-of-bounds read.
  (struct.get $bar $bar-only)
)
```

The problem here is that the normal subtyping rules make it possible
to allocate a `$foo` with an RTT for `$bar`,
causing subsequent casts to behave incorrectly.
One solution would be to have `struct.new` dynamically check that the provided RTT value
describes precisely the allocated type.
A better solution would be to allow userspace to perform that check if necessary,
but also be able to statically prove via the type system that it is not necessary.

To facilitate that, we introduce exact reference types,
which are inhabited by references to a particular heap type (and possibly the null value)
but not any of the heap type's strict subtypes.

Exact reference types can be nullable with the form `(ref exact null ht)`
or non-nullable with the form `(ref exact ht)`.

For any heap type `ht`:

```
(ref ht) <: (ref null ht)
(ref exact null ht) <: (ref null ht)
(ref exact ht) <: (ref ht)
(ref exact ht) <: (ref exact null ht)
```

Furthermore, to ensure that each type hierarchy remains a lattice,
we have:

```
(ref null exact bot) <: (ref null exact ht)
(ref exact bot) <: (ref exact ht)
```

where `bot` is the bottom type
(e.g. `none`, `nofunc`, `noextern`, `noexnt`, or `nocont`) of `ht`'s hierarchy.

All instructions that create reference to a particular heap type
(e.g. `ref.func`, `struct.new`, `array.new`, `ref.i31`, `ref.null`,  etc.)
are refined to produce exact references to that heap type.
In contrast, `any.convert_extern` and `extern.convert_any` never produce exact references.
`(ref exact any)` and `(ref exact extern)` are uninhabited.
Internalized host references and externalized internal references are modeled
as having "hidden" subtypes of `any` and `extern`,
respectively.
This preserves our ability to assign them more specific types in the future.

When allocating types with custom RTTs,
`struct.new` and `struct.new_default` take exact references to the RTTs
as their first operands.
This makes the unsound program above invalid.

## New Instructions

Given a reference to a type with a custom RTT,
a reference to the custom RTT value can be retrieved with `ref.get_rtt`.

```
ref.get_rtt typeidx

C |- ref.get_rtt x : (ref exact_1 null x) -> (ref exact_1 y)
-- C.types[x] ~ struct (descriptor y) field*
```

If the provided reference is exact,
then the type of the custom RTT is known precisely,
so the result can be exact as well.
Otherwise, the subtyping rules described above ensure that there will be some custom RTT value
and that it will be a subtype of the custom RTT type for `x`,
so the result can be a non-null inexact reference.

Being able to retrieve a custom RTT means you can then compare it for equality
with an expected custom RTT value.
If the values are equal,
that lets you reason about the type of the value the custom RTT was attached to.
But the type system cannot make those logical deductions on its own,
so to help it out we introduce a new set of cast instructions that take custom RTTs
as additional operands.
These instructions compare the RTT of the provided reference with the provided RTT and if they match,
return the provided reference with the type described by the RTT.
If the type of the RTT is exact,
then the type of the cast output can also be exact.

```
ref.cast_rtt reftype

C |- ref.cast_rtt rt : (ref null ht) (ref null exact_1 y) -> rt
-- rt = (ref null? exact_1 x)
-- C |- C.types[x] <: ht
-- C.types[x] = struct (descriptor y) field*
```

```
br_on_cast_rtt labelidx reftype reftype

C |- br_on_cast_rtt l rt_1 rt_2 : t* rt_1 (ref null exact_1 y) -> t* (rt_1 \ rt_2)
-- C.labels[l] = t* rt
-- C |- rt_2 <: rt
-- C |- rt_2 <: rt_1
-- rt_2 = (ref null? exact_1 x)
-- C.types[x] = struct (descriptor y) field*
```

```
br_on_cast_rtt_fail labelidx reftype reftype

C |- br_on_cast_rtt_fail l rt_1 rt_2 : t* rt_1 (ref null exact_1 y) -> t* rt_2
-- C.labels[l] = t* rt
-- C |- rt_1 \ rt_2 <: rt
-- C |- rt_2 <: rt_1
-- rt_2 = (ref null? exact_1 x)
-- C.types[x] = struct (descriptor y) field*
```

## JS Prototypes

In JS engines,
WebAssembly RTTs correspond to JS shape descriptors.
Custom RTTs act as first-class handles to the engine-managed RTTs,
so they can serve as extension points for the JS reflection of the Wasm objects they describe.

We introduce a new `WebAssembly.setDescriptorPrototype()` API
that takes a custom RTT instance and a prototype object.
The provided prototype will be attached to the custom RTT
and will become the prototype for the JS reflection
of all Wasm objects the custom RTT describes.

The following is a full example that uses `WebAssembly.setDescriptorPrototype()`
to allow JS to call `get()` and `inc()` methods on counter objects implemented in
WebAssembly.

> Note: If there is demand for it,
> a similar API could configure property names that JS could use to access fields
> of the described WebAssembly objects.

```wasm
;; counter.wasm
(module
  (rec
    (type $counter (struct (descriptor $counter.vtable (field $val i32))))
    (type $counter.vtable (struct
      (describes $counter)
      (field $get (ref $get_t))
      (field $inc (ref $inc_t))
    ))
    (type $get_t (func (param (ref null $counter)) (result i32)))
    (type $inc_t (func (param (ref null $counter))))
  )

  (elem declare func $counter.get $counter.inc)

  (global $counter.vtable (export "counter.vtable") (ref exact $counter.vtable)
    (struct.new $counter.vtable
      (ref.func $counter.get)
      (ref.func $counter.inc)
    )
  )

  (global $counter (export "counter") (ref $counter)
    (struct.new_default $counter
      (global.get $counter.vtable)
    )
  )

  (func $counter.get (export "counter.get") (type $get_t) (param (ref null $counter)) (result i32)
    (struct.get $counter $val (local.get 0))
  )

  (func $counter.inc (export "counter.inc") (type $inc_t) (param (ref null $counter))
    (struct.set $counter $val
      (local.get 0)
      (i32.add
        (struct.get $counter $val (local.get 0))
        (i32.const 1)
      )
    )
  )
)
```

```js
// counter.js
var {module, instance} = await WebAssembly.instantiateStreaming(fetch('counter.wasm'));

WebAssembly.setDescriptorPrototype(instance.exports['counter.vtable'], {
  get: function() { instance.exports['counter.get'](this); },
  inc: function() { return instance.exports['counter.get'](this); }
});

var counter = instance.exports['counter'];

console.log(counter.get()); // 0
counter.inc();
console.log(counter.get()); // 1
```

## Declarative Prototype Initialization

TODO

## Type Section Field Deduplication

TODO
