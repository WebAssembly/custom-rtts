# Test

```sh
$ (../src/exe-watsup/main.exe test.watsup -o test.tex && cat test.tex)
cat: test.tex: No such file or directory
[1]
```


# Preview

```sh
$ (cd ../spec/wasm-3.0 && ../../src/exe-watsup/main.exe *.watsup -v -l --print-il --print-no-pos --check)
watsup 0.4 generator
== Parsing...
== Elaboration...

;; 1-syntax.watsup
syntax NULL =
  | NULL

;; 1-syntax.watsup
syntax MUT =
  | MUT

;; 1-syntax.watsup
syntax FINAL =
  | FINAL

;; 0-aux.watsup
syntax N = nat

;; 0-aux.watsup
syntax M = nat

;; 0-aux.watsup
syntax K = nat

;; 0-aux.watsup
syntax n = nat

;; 0-aux.watsup
syntax m = nat

;; 0-aux.watsup
def $min(nat : nat, nat : nat) : nat
  ;; 0-aux.watsup
  def $min{i : nat, j : nat}(i, j) = i
    -- if (i <= j)
  ;; 0-aux.watsup
  def $min{i : nat, j : nat}(i, j) = j
    -- otherwise

;; 0-aux.watsup
rec {

;; 0-aux.watsup:20.1-20.56
def $sum(nat*) : nat
  ;; 0-aux.watsup:21.1-21.18
  def $sum([]) = 0
  ;; 0-aux.watsup:22.1-22.35
  def $sum{n : n, `n'*` : n*}([n] ++ n'*{n' <- `n'*`}) = (n + $sum(n'*{n' <- `n'*`}))
}

;; 0-aux.watsup
rec {

;; 0-aux.watsup:24.1-24.57
def $prod(nat*) : nat
  ;; 0-aux.watsup:25.1-25.19
  def $prod([]) = 1
  ;; 0-aux.watsup:26.1-26.37
  def $prod{n : n, `n'*` : n*}([n] ++ n'*{n' <- `n'*`}) = (n * $prod(n'*{n' <- `n'*`}))
}

;; 0-aux.watsup
def $opt_(syntax X, X*) : X?
  ;; 0-aux.watsup
  def $opt_{syntax X}(syntax X, []) = ?()
  ;; 0-aux.watsup
  def $opt_{syntax X, w : X}(syntax X, [w]) = ?(w)

;; 0-aux.watsup
rec {

;; 0-aux.watsup:35.1-35.55
def $concat_(syntax X, X**) : X*
  ;; 0-aux.watsup:36.1-36.34
  def $concat_{syntax X}(syntax X, []) = []
  ;; 0-aux.watsup:37.1-37.64
  def $concat_{syntax X, `w*` : X*, `w'**` : X**}(syntax X, [w*{w <- `w*`}] ++ w'*{w' <- `w'*`}*{`w'*` <- `w'**`}) = w*{w <- `w*`} ++ $concat_(syntax X, w'*{w' <- `w'*`}*{`w'*` <- `w'**`})
}

;; 0-aux.watsup
rec {

;; 0-aux.watsup:39.1-39.61
def $concatn_(syntax X, X**, nat : nat) : X*
  ;; 0-aux.watsup:40.1-40.38
  def $concatn_{syntax X, n : n}(syntax X, [], n) = []
  ;; 0-aux.watsup:41.1-41.73
  def $concatn_{syntax X, `w*` : X*, n : n, `w'**` : X**}(syntax X, [w^n{w <- `w*`}] ++ w'^n{w' <- `w'*`}*{`w'*` <- `w'**`}, n) = w^n{w <- `w*`} ++ $concatn_(syntax X, w'^n{w' <- `w'*`}*{`w'*` <- `w'**`}, n)
}

;; 0-aux.watsup
rec {

;; 0-aux.watsup:46.1-46.78
def $disjoint_(syntax X, X*) : bool
  ;; 0-aux.watsup:47.1-47.37
  def $disjoint_{syntax X}(syntax X, []) = true
  ;; 0-aux.watsup:48.1-48.68
  def $disjoint_{syntax X, w : X, `w'*` : X*}(syntax X, [w] ++ w'*{w' <- `w'*`}) = (~ w <- w'*{w' <- `w'*`} /\ $disjoint_(syntax X, w'*{w' <- `w'*`}))
}

;; 0-aux.watsup
rec {

;; 0-aux.watsup:51.1-51.38
def $setminus1_(syntax X, X : X, X*) : X*
  ;; 0-aux.watsup:55.1-55.38
  def $setminus1_{syntax X, w : X}(syntax X, w, []) = [w]
  ;; 0-aux.watsup:56.1-56.78
  def $setminus1_{syntax X, w : X, w_1 : X, `w'*` : X*}(syntax X, w, [w_1] ++ w'*{w' <- `w'*`}) = []
    -- if (w = w_1)
  ;; 0-aux.watsup:57.1-57.77
  def $setminus1_{syntax X, w : X, w_1 : X, `w'*` : X*}(syntax X, w, [w_1] ++ w'*{w' <- `w'*`}) = $setminus1_(syntax X, w, w'*{w' <- `w'*`})
    -- otherwise
}

;; 0-aux.watsup
rec {

;; 0-aux.watsup:50.1-50.56
def $setminus_(syntax X, X*, X*) : X*
  ;; 0-aux.watsup:53.1-53.40
  def $setminus_{syntax X, `w*` : X*}(syntax X, [], w*{w <- `w*`}) = []
  ;; 0-aux.watsup:54.1-54.90
  def $setminus_{syntax X, w_1 : X, `w'*` : X*, `w*` : X*}(syntax X, [w_1] ++ w'*{w' <- `w'*`}, w*{w <- `w*`}) = $setminus1_(syntax X, w_1, w*{w <- `w*`}) ++ $setminus_(syntax X, w'*{w' <- `w'*`}, w*{w <- `w*`})
}

;; 0-aux.watsup
rec {

;; 0-aux.watsup:62.1-62.46
def $setproduct2_(syntax X, X : X, X**) : X**
  ;; 0-aux.watsup:68.1-68.44
  def $setproduct2_{syntax X, w_1 : X}(syntax X, w_1, []) = []
  ;; 0-aux.watsup:69.1-69.90
  def $setproduct2_{syntax X, w_1 : X, `w'*` : X*, `w**` : X**}(syntax X, w_1, [w'*{w' <- `w'*`}] ++ w*{w <- `w*`}*{`w*` <- `w**`}) = [[w_1] ++ w'*{w' <- `w'*`}] ++ $setproduct2_(syntax X, w_1, w*{w <- `w*`}*{`w*` <- `w**`})
}

;; 0-aux.watsup
rec {

;; 0-aux.watsup:61.1-61.47
def $setproduct1_(syntax X, X*, X**) : X**
  ;; 0-aux.watsup:66.1-66.46
  def $setproduct1_{syntax X, `w**` : X**}(syntax X, [], w*{w <- `w*`}*{`w*` <- `w**`}) = []
  ;; 0-aux.watsup:67.1-67.107
  def $setproduct1_{syntax X, w_1 : X, `w'*` : X*, `w**` : X**}(syntax X, [w_1] ++ w'*{w' <- `w'*`}, w*{w <- `w*`}*{`w*` <- `w**`}) = $setproduct2_(syntax X, w_1, w*{w <- `w*`}*{`w*` <- `w**`}) ++ $setproduct1_(syntax X, w'*{w' <- `w'*`}, w*{w <- `w*`}*{`w*` <- `w**`})
}

;; 0-aux.watsup
rec {

;; 0-aux.watsup:60.1-60.82
def $setproduct_(syntax X, X**) : X**
  ;; 0-aux.watsup:64.1-64.40
  def $setproduct_{syntax X}(syntax X, []) = [[]]
  ;; 0-aux.watsup:65.1-65.90
  def $setproduct_{syntax X, `w_1*` : X*, `w**` : X**}(syntax X, [w_1*{w_1 <- `w_1*`}] ++ w*{w <- `w*`}*{`w*` <- `w**`}) = $setproduct1_(syntax X, w_1*{w_1 <- `w_1*`}, $setproduct_(syntax X, w*{w <- `w*`}*{`w*` <- `w**`}))
}

;; 1-syntax.watsup
def $ND : bool

;; 1-syntax.watsup
syntax bit =
  | `%`{i : nat}(i : nat)
    -- if ((i = 0) \/ (i = 1))

;; 1-syntax.watsup
syntax byte =
  | `%`{i : nat}(i : nat)
    -- if ((i >= 0) /\ (i <= 255))

;; 1-syntax.watsup
syntax uN{N : N}(N) =
  | `%`{i : nat}(i : nat)
    -- if ((i >= 0) /\ (i <= ((((2 ^ N) : nat <:> int) - (1 : nat <:> int)) : int <:> nat)))

;; 1-syntax.watsup
syntax sN{N : N}(N) =
  | `%`{i : int}(i : int)
    -- if ((((i >= - ((2 ^ (((N : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) : nat <:> int)) /\ (i <= - (1 : nat <:> int))) \/ (i = (0 : nat <:> int))) \/ ((i >= + (1 : nat <:> int)) /\ (i <= (+ ((2 ^ (((N : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) : nat <:> int) - (1 : nat <:> int)))))

;; 1-syntax.watsup
syntax iN{N : N}(N) = uN(N)

;; 1-syntax.watsup
syntax u8 = uN(8)

;; 1-syntax.watsup
syntax u16 = uN(16)

;; 1-syntax.watsup
syntax u31 = uN(31)

;; 1-syntax.watsup
syntax u32 = uN(32)

;; 1-syntax.watsup
syntax u64 = uN(64)

;; 1-syntax.watsup
syntax u128 = uN(128)

;; 1-syntax.watsup
syntax s33 = sN(33)

;; 1-syntax.watsup
def $signif(N : N) : nat
  ;; 1-syntax.watsup
  def $signif(32) = 23
  ;; 1-syntax.watsup
  def $signif(64) = 52

;; 1-syntax.watsup
def $expon(N : N) : nat
  ;; 1-syntax.watsup
  def $expon(32) = 8
  ;; 1-syntax.watsup
  def $expon(64) = 11

;; 1-syntax.watsup
def $M(N : N) : nat
  ;; 1-syntax.watsup
  def $M{N : N}(N) = $signif(N)

;; 1-syntax.watsup
def $E(N : N) : nat
  ;; 1-syntax.watsup
  def $E{N : N}(N) = $expon(N)

;; 1-syntax.watsup
syntax exp = int

;; 1-syntax.watsup
syntax fNmag{N : N}(N) =
  | NORM{m : m, exp : exp}(m : m, exp : exp)
    -- if ((m < (2 ^ $M(N))) /\ ((((2 : nat <:> int) - ((2 ^ ((($E(N) : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) : nat <:> int)) <= exp) /\ (exp <= (((2 ^ ((($E(N) : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) : nat <:> int) - (1 : nat <:> int)))))
  | SUBNORM{m : m, exp : exp}(m : m)
    -- if ((m < (2 ^ $M(N))) /\ (((2 : nat <:> int) - ((2 ^ ((($E(N) : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) : nat <:> int)) = exp))
  | INF
  | NAN{m : m}(m : m)
    -- if ((1 <= m) /\ (m < (2 ^ $M(N))))

;; 1-syntax.watsup
syntax fN{N : N}(N) =
  | POS{fNmag : fNmag(N)}(fNmag : fNmag(N))
  | NEG{fNmag : fNmag(N)}(fNmag : fNmag(N))

;; 1-syntax.watsup
syntax f32 = fN(32)

;; 1-syntax.watsup
syntax f64 = fN(64)

;; 1-syntax.watsup
def $fzero(N : N) : fN(N)
  ;; 1-syntax.watsup
  def $fzero{N : N}(N) = POS_fN(SUBNORM_fNmag(0))

;; 1-syntax.watsup
def $fone(N : N) : fN(N)
  ;; 1-syntax.watsup
  def $fone{N : N}(N) = POS_fN(NORM_fNmag(1, (0 : nat <:> int)))

;; 1-syntax.watsup
def $fnat(N : N, nat : nat) : fN(N)
  ;; 1-syntax.watsup
  def $fnat{N : N, n : n}(N, n) = POS_fN(NORM_fNmag(n, (0 : nat <:> int)))

;; 1-syntax.watsup
def $canon_(N : N) : nat
  ;; 1-syntax.watsup
  def $canon_{N : N}(N) = (2 ^ ((($signif(N) : nat <:> int) - (1 : nat <:> int)) : int <:> nat))

;; 1-syntax.watsup
syntax vN{N : N}(N) = uN(N)

;; 1-syntax.watsup
syntax v128 = vN(128)

;; 1-syntax.watsup
syntax list{syntax X}(syntax X) =
  | `%`{`X*` : X*}(X*{X <- `X*`} : X*)
    -- if (|X*{X <- `X*`}| < (2 ^ 32))

;; 1-syntax.watsup
syntax char =
  | `%`{i : nat}(i : nat)
    -- if (((i >= 0) /\ (i <= 55295)) \/ ((i >= 57344) /\ (i <= 1114111)))

;; A-binary.watsup
def $cont(byte : byte) : nat
  ;; A-binary.watsup
  def $cont{b : byte}(b) = (((b!`%`_byte.0 : nat <:> int) - (128 : nat <:> int)) : int <:> nat)
    -- if ((128 < b!`%`_byte.0) /\ (b!`%`_byte.0 < 192))

;; 1-syntax.watsup
rec {

;; 1-syntax.watsup:100.1-100.25
def $utf8(char*) : byte*
  ;; A-binary.watsup:53.1-53.44
  def $utf8{`ch*` : char*}(ch*{ch <- `ch*`}) = $concat_(syntax byte, $utf8([ch])*{ch <- `ch*`})
  ;; A-binary.watsup:54.1-56.15
  def $utf8{ch : char, b : byte}([ch]) = [b]
    -- if (ch!`%`_char.0 < 128)
    -- if (`%`_byte(ch!`%`_char.0) = b)
  ;; A-binary.watsup:57.1-59.46
  def $utf8{ch : char, b_1 : byte, b_2 : byte}([ch]) = [b_1 b_2]
    -- if ((128 <= ch!`%`_char.0) /\ (ch!`%`_char.0 < 2048))
    -- if (ch!`%`_char.0 = (((2 ^ 6) * (((b_1!`%`_byte.0 : nat <:> int) - (192 : nat <:> int)) : int <:> nat)) + $cont(b_2)))
  ;; A-binary.watsup:60.1-62.64
  def $utf8{ch : char, b_1 : byte, b_2 : byte, b_3 : byte}([ch]) = [b_1 b_2 b_3]
    -- if (((2048 <= ch!`%`_char.0) /\ (ch!`%`_char.0 < 55296)) \/ ((57344 <= ch!`%`_char.0) /\ (ch!`%`_char.0 < 65536)))
    -- if (ch!`%`_char.0 = ((((2 ^ 12) * (((b_1!`%`_byte.0 : nat <:> int) - (224 : nat <:> int)) : int <:> nat)) + ((2 ^ 6) * $cont(b_2))) + $cont(b_3)))
  ;; A-binary.watsup:63.1-65.82
  def $utf8{ch : char, b_1 : byte, b_2 : byte, b_3 : byte, b_4 : byte}([ch]) = [b_1 b_2 b_3 b_4]
    -- if ((65536 <= ch!`%`_char.0) /\ (ch!`%`_char.0 < 69632))
    -- if (ch!`%`_char.0 = (((((2 ^ 18) * (((b_1!`%`_byte.0 : nat <:> int) - (240 : nat <:> int)) : int <:> nat)) + ((2 ^ 12) * $cont(b_2))) + ((2 ^ 6) * $cont(b_3))) + $cont(b_4)))
}

;; 1-syntax.watsup
syntax name =
  | `%`{`char*` : char*}(char*{char <- `char*`} : char*)
    -- if (|$utf8(char*{char <- `char*`})| < (2 ^ 32))

;; 1-syntax.watsup
syntax idx = u32

;; 1-syntax.watsup
syntax laneidx = u8

;; 1-syntax.watsup
syntax typeidx = idx

;; 1-syntax.watsup
syntax funcidx = idx

;; 1-syntax.watsup
syntax globalidx = idx

;; 1-syntax.watsup
syntax tableidx = idx

;; 1-syntax.watsup
syntax memidx = idx

;; 1-syntax.watsup
syntax tagidx = idx

;; 1-syntax.watsup
syntax elemidx = idx

;; 1-syntax.watsup
syntax dataidx = idx

;; 1-syntax.watsup
syntax labelidx = idx

;; 1-syntax.watsup
syntax localidx = idx

;; 1-syntax.watsup
syntax fieldidx = idx

;; 1-syntax.watsup
syntax externidx =
  | FUNC{funcidx : funcidx}(funcidx : funcidx)
  | GLOBAL{globalidx : globalidx}(globalidx : globalidx)
  | TABLE{tableidx : tableidx}(tableidx : tableidx)
  | MEM{memidx : memidx}(memidx : memidx)
  | TAG{tagidx : tagidx}(tagidx : tagidx)

;; 1-syntax.watsup
syntax nul = NULL?

;; 1-syntax.watsup
syntax nul1 = NULL?

;; 1-syntax.watsup
syntax nul2 = NULL?

;; 1-syntax.watsup
syntax addrtype =
  | I32
  | I64

;; 1-syntax.watsup
syntax numtype =
  | I32
  | I64
  | F32
  | F64

;; 1-syntax.watsup
syntax vectype =
  | V128

;; 1-syntax.watsup
syntax consttype =
  | I32
  | I64
  | F32
  | F64
  | V128

;; 1-syntax.watsup
syntax absheaptype =
  | ANY
  | EQ
  | I31
  | STRUCT
  | ARRAY
  | NONE
  | FUNC
  | NOFUNC
  | EXN
  | NOEXN
  | EXTERN
  | NOEXTERN
  | BOT

;; 1-syntax.watsup
syntax mut = MUT?

;; 1-syntax.watsup
syntax fin = FINAL?

;; 1-syntax.watsup
rec {

;; 1-syntax.watsup:174.1-175.26
syntax typeuse =
  | _IDX{typeidx : typeidx}(typeidx : typeidx)
  | DEF{rectype : rectype, n : n}(rectype : rectype, n : n)
  | REC{n : n}(n : n)

;; 1-syntax.watsup:180.1-181.26
syntax heaptype =
  | ANY
  | EQ
  | I31
  | STRUCT
  | ARRAY
  | NONE
  | FUNC
  | NOFUNC
  | EXN
  | NOEXN
  | EXTERN
  | NOEXTERN
  | BOT
  | _IDX{typeidx : typeidx}(typeidx : typeidx)
  | REC{n : n}(n : n)
  | DEF{rectype : rectype, n : n}(rectype : rectype, n : n)

;; 1-syntax.watsup:188.1-189.14
syntax valtype =
  | I32
  | I64
  | F32
  | F64
  | V128
  | REF{nul : nul, heaptype : heaptype}(nul : nul, heaptype : heaptype)
  | BOT

;; 1-syntax.watsup:228.1-228.66
syntax storagetype =
  | BOT
  | I32
  | I64
  | F32
  | F64
  | V128
  | REF{nul : nul, heaptype : heaptype}(nul : nul, heaptype : heaptype)
  | I8
  | I16

;; 1-syntax.watsup:237.1-238.16
syntax resulttype = list(syntax valtype)

;; 1-syntax.watsup:250.1-250.60
syntax fieldtype =
  | `%%`{mut : mut, storagetype : storagetype}(mut : mut, storagetype : storagetype)

;; 1-syntax.watsup:252.1-252.90
syntax functype =
  | `%->%`{resulttype : resulttype}(resulttype : resulttype, resulttype)

;; 1-syntax.watsup:253.1-253.64
syntax structtype = list(syntax fieldtype)

;; 1-syntax.watsup:254.1-254.54
syntax arraytype = fieldtype

;; 1-syntax.watsup:256.1-259.18
syntax comptype =
  | STRUCT{structtype : structtype}(structtype : structtype)
  | ARRAY{arraytype : arraytype}(arraytype : arraytype)
  | FUNC{functype : functype}(functype : functype)

;; 1-syntax.watsup:261.1-262.30
syntax subtype =
  | SUB{fin : fin, `typeuse*` : typeuse*, comptype : comptype}(fin : fin, typeuse*{typeuse <- `typeuse*`} : typeuse*, comptype : comptype)

;; 1-syntax.watsup:264.1-265.22
syntax rectype =
  | REC{list : list(syntax subtype)}(list : list(syntax subtype))
}

;; 1-syntax.watsup
syntax deftype =
  | DEF{rectype : rectype, n : n}(rectype : rectype, n : n)

;; 1-syntax.watsup
syntax typevar =
  | _IDX{typeidx : typeidx}(typeidx : typeidx)
  | REC{nat : nat}(nat : nat)

;; 1-syntax.watsup
syntax reftype =
  | REF{nul : nul, heaptype : heaptype}(nul : nul, heaptype : heaptype)

;; 1-syntax.watsup
syntax Inn =
  | I32
  | I64

;; 1-syntax.watsup
syntax Fnn =
  | F32
  | F64

;; 1-syntax.watsup
syntax Vnn =
  | V128

;; 1-syntax.watsup
syntax Cnn =
  | I32
  | I64
  | F32
  | F64
  | V128

;; 1-syntax.watsup
def $ANYREF : reftype
  ;; 1-syntax.watsup
  def $ANYREF = REF_reftype(?(NULL_NULL), ANY_heaptype)

;; 1-syntax.watsup
def $EQREF : reftype
  ;; 1-syntax.watsup
  def $EQREF = REF_reftype(?(NULL_NULL), EQ_heaptype)

;; 1-syntax.watsup
def $I31REF : reftype
  ;; 1-syntax.watsup
  def $I31REF = REF_reftype(?(NULL_NULL), I31_heaptype)

;; 1-syntax.watsup
def $STRUCTREF : reftype
  ;; 1-syntax.watsup
  def $STRUCTREF = REF_reftype(?(NULL_NULL), STRUCT_heaptype)

;; 1-syntax.watsup
def $ARRAYREF : reftype
  ;; 1-syntax.watsup
  def $ARRAYREF = REF_reftype(?(NULL_NULL), ARRAY_heaptype)

;; 1-syntax.watsup
def $FUNCREF : reftype
  ;; 1-syntax.watsup
  def $FUNCREF = REF_reftype(?(NULL_NULL), FUNC_heaptype)

;; 1-syntax.watsup
def $EXNREF : reftype
  ;; 1-syntax.watsup
  def $EXNREF = REF_reftype(?(NULL_NULL), EXTERN_heaptype)

;; 1-syntax.watsup
def $EXTERNREF : reftype
  ;; 1-syntax.watsup
  def $EXTERNREF = REF_reftype(?(NULL_NULL), EXTERN_heaptype)

;; 1-syntax.watsup
def $NULLREF : reftype
  ;; 1-syntax.watsup
  def $NULLREF = REF_reftype(?(NULL_NULL), NONE_heaptype)

;; 1-syntax.watsup
def $NULLFUNCREF : reftype
  ;; 1-syntax.watsup
  def $NULLFUNCREF = REF_reftype(?(NULL_NULL), NOFUNC_heaptype)

;; 1-syntax.watsup
def $NULLEXNREF : reftype
  ;; 1-syntax.watsup
  def $NULLEXNREF = REF_reftype(?(NULL_NULL), NOEXN_heaptype)

;; 1-syntax.watsup
def $NULLEXTERNREF : reftype
  ;; 1-syntax.watsup
  def $NULLEXTERNREF = REF_reftype(?(NULL_NULL), NOEXTERN_heaptype)

;; 1-syntax.watsup
syntax packtype =
  | I8
  | I16

;; 1-syntax.watsup
syntax lanetype =
  | I32
  | I64
  | F32
  | F64
  | I8
  | I16

;; 1-syntax.watsup
syntax Pnn =
  | I8
  | I16

;; 1-syntax.watsup
syntax Jnn =
  | I32
  | I64
  | I8
  | I16

;; 1-syntax.watsup
syntax Lnn =
  | I32
  | I64
  | F32
  | F64
  | I8
  | I16

;; 1-syntax.watsup
syntax mut1 = MUT?

;; 1-syntax.watsup
syntax mut2 = MUT?

;; 1-syntax.watsup
syntax limits =
  | `[%..%]`{u64 : u64}(u64 : u64, u64)

;; 1-syntax.watsup
syntax globaltype =
  | `%%`{mut : mut, valtype : valtype}(mut : mut, valtype : valtype)

;; 1-syntax.watsup
syntax tabletype =
  | `%%%`{addrtype : addrtype, limits : limits, reftype : reftype}(addrtype : addrtype, limits : limits, reftype : reftype)

;; 1-syntax.watsup
syntax memtype =
  | `%%PAGE`{addrtype : addrtype, limits : limits}(addrtype : addrtype, limits : limits)

;; 1-syntax.watsup
syntax tagtype = deftype

;; 1-syntax.watsup
syntax elemtype = reftype

;; 1-syntax.watsup
syntax datatype =
  | OK

;; 1-syntax.watsup
syntax externtype =
  | FUNC{typeuse : typeuse}(typeuse : typeuse)
  | GLOBAL{globaltype : globaltype}(globaltype : globaltype)
  | TABLE{tabletype : tabletype}(tabletype : tabletype)
  | MEM{memtype : memtype}(memtype : memtype)
  | TAG{typeuse : typeuse}(typeuse : typeuse)

;; 1-syntax.watsup
syntax moduletype =
  | `%->%`{`externtype*` : externtype*}(externtype*{externtype <- `externtype*`} : externtype*, externtype*)

;; 1-syntax.watsup
def $size(numtype : numtype) : nat
  ;; 1-syntax.watsup
  def $size(I32_numtype) = 32
  ;; 1-syntax.watsup
  def $size(I64_numtype) = 64
  ;; 1-syntax.watsup
  def $size(F32_numtype) = 32
  ;; 1-syntax.watsup
  def $size(F64_numtype) = 64

;; 1-syntax.watsup
def $vsize(vectype : vectype) : nat
  ;; 1-syntax.watsup
  def $vsize(V128_vectype) = 128

;; 1-syntax.watsup
def $psize(packtype : packtype) : nat
  ;; 1-syntax.watsup
  def $psize(I8_packtype) = 8
  ;; 1-syntax.watsup
  def $psize(I16_packtype) = 16

;; 1-syntax.watsup
def $lsize(lanetype : lanetype) : nat
  ;; 1-syntax.watsup
  def $lsize{numtype : numtype}((numtype : numtype <: lanetype)) = $size(numtype)
  ;; 1-syntax.watsup
  def $lsize{packtype : packtype}((packtype : packtype <: lanetype)) = $psize(packtype)

;; 1-syntax.watsup
def $zsize(storagetype : storagetype) : nat
  ;; 1-syntax.watsup
  def $zsize{numtype : numtype}((numtype : numtype <: storagetype)) = $size(numtype)
  ;; 1-syntax.watsup
  def $zsize{vectype : vectype}((vectype : vectype <: storagetype)) = $vsize(vectype)
  ;; 1-syntax.watsup
  def $zsize{packtype : packtype}((packtype : packtype <: storagetype)) = $psize(packtype)

;; 1-syntax.watsup
def $sizenn(numtype : numtype) : nat
  ;; 1-syntax.watsup
  def $sizenn{nt : numtype}(nt) = $size(nt)

;; 1-syntax.watsup
def $sizenn1(numtype : numtype) : nat
  ;; 1-syntax.watsup
  def $sizenn1{nt : numtype}(nt) = $size(nt)

;; 1-syntax.watsup
def $sizenn2(numtype : numtype) : nat
  ;; 1-syntax.watsup
  def $sizenn2{nt : numtype}(nt) = $size(nt)

;; 1-syntax.watsup
def $vsizenn(vectype : vectype) : nat
  ;; 1-syntax.watsup
  def $vsizenn{vt : vectype}(vt) = $vsize(vt)

;; 1-syntax.watsup
def $psizenn(packtype : packtype) : nat
  ;; 1-syntax.watsup
  def $psizenn{pt : packtype}(pt) = $psize(pt)

;; 1-syntax.watsup
def $lsizenn(lanetype : lanetype) : nat
  ;; 1-syntax.watsup
  def $lsizenn{lt : lanetype}(lt) = $lsize(lt)

;; 1-syntax.watsup
def $lsizenn1(lanetype : lanetype) : nat
  ;; 1-syntax.watsup
  def $lsizenn1{lt : lanetype}(lt) = $lsize(lt)

;; 1-syntax.watsup
def $lsizenn2(lanetype : lanetype) : nat
  ;; 1-syntax.watsup
  def $lsizenn2{lt : lanetype}(lt) = $lsize(lt)

;; 1-syntax.watsup
def $lunpack(lanetype : lanetype) : numtype
  ;; 1-syntax.watsup
  def $lunpack{numtype : numtype}((numtype : numtype <: lanetype)) = numtype
  ;; 1-syntax.watsup
  def $lunpack{packtype : packtype}((packtype : packtype <: lanetype)) = I32_numtype

;; 1-syntax.watsup
def $unpack(storagetype : storagetype) : valtype
  ;; 1-syntax.watsup
  def $unpack{valtype : valtype}((valtype : valtype <: storagetype)) = valtype
  ;; 1-syntax.watsup
  def $unpack{packtype : packtype}((packtype : packtype <: storagetype)) = I32_valtype

;; 1-syntax.watsup
def $nunpack(storagetype : storagetype) : numtype
  ;; 1-syntax.watsup
  def $nunpack{numtype : numtype}((numtype : numtype <: storagetype)) = numtype
  ;; 1-syntax.watsup
  def $nunpack{packtype : packtype}((packtype : packtype <: storagetype)) = I32_numtype

;; 1-syntax.watsup
def $vunpack(storagetype : storagetype) : vectype
  ;; 1-syntax.watsup
  def $vunpack{vectype : vectype}((vectype : vectype <: storagetype)) = vectype

;; 1-syntax.watsup
def $cunpack(storagetype : storagetype) : consttype
  ;; 1-syntax.watsup
  def $cunpack{consttype : consttype}((consttype : consttype <: storagetype)) = consttype
  ;; 1-syntax.watsup
  def $cunpack{packtype : packtype}((packtype : packtype <: storagetype)) = I32_consttype
  ;; 1-syntax.watsup
  def $cunpack{lanetype : lanetype}((lanetype : lanetype <: storagetype)) = ($lunpack(lanetype) : numtype <: consttype)

;; 1-syntax.watsup
syntax num_(numtype : numtype)
  ;; 1-syntax.watsup
  syntax num_{Inn : Inn}((Inn : Inn <: numtype)) = iN($sizenn((Inn : Inn <: numtype)))


  ;; 1-syntax.watsup
  syntax num_{Fnn : Fnn}((Fnn : Fnn <: numtype)) = fN($sizenn((Fnn : Fnn <: numtype)))


;; 1-syntax.watsup
syntax pack_{Pnn : Pnn}(Pnn) = iN($psizenn(Pnn))

;; 1-syntax.watsup
syntax lane_(lanetype : lanetype)
  ;; 1-syntax.watsup
  syntax lane_{numtype : numtype}((numtype : numtype <: lanetype)) = num_(numtype)


  ;; 1-syntax.watsup
  syntax lane_{packtype : packtype}((packtype : packtype <: lanetype)) = pack_(packtype)


  ;; 1-syntax.watsup
  syntax lane_{Jnn : Jnn}((Jnn : Jnn <: lanetype)) = iN($lsize((Jnn : Jnn <: lanetype)))


;; 1-syntax.watsup
syntax vec_{Vnn : Vnn}(Vnn) = vN($vsize(Vnn))

;; 1-syntax.watsup
syntax lit_(storagetype : storagetype)
  ;; 1-syntax.watsup
  syntax lit_{numtype : numtype}((numtype : numtype <: storagetype)) = num_(numtype)


  ;; 1-syntax.watsup
  syntax lit_{vectype : vectype}((vectype : vectype <: storagetype)) = vec_(vectype)


  ;; 1-syntax.watsup
  syntax lit_{packtype : packtype}((packtype : packtype <: storagetype)) = pack_(packtype)


;; 1-syntax.watsup
syntax sz =
  | `%`{i : nat}(i : nat)
    -- if ((((i = 8) \/ (i = 16)) \/ (i = 32)) \/ (i = 64))

;; 1-syntax.watsup
syntax sx =
  | U
  | S

;; 1-syntax.watsup
syntax unop_(numtype : numtype)
  ;; 1-syntax.watsup
  syntax unop_{Inn : Inn}((Inn : Inn <: numtype)) =
  | CLZ
  | CTZ
  | POPCNT
  | EXTEND{sz : sz}(sz : sz)
    -- if (sz!`%`_sz.0 < $sizenn((Inn : Inn <: numtype)))


  ;; 1-syntax.watsup
  syntax unop_{Fnn : Fnn}((Fnn : Fnn <: numtype)) =
  | ABS
  | NEG
  | SQRT
  | CEIL
  | FLOOR
  | TRUNC
  | NEAREST


;; 1-syntax.watsup
syntax binop_(numtype : numtype)
  ;; 1-syntax.watsup
  syntax binop_{Inn : Inn}((Inn : Inn <: numtype)) =
  | ADD
  | SUB
  | MUL
  | DIV{sx : sx}(sx : sx)
  | REM{sx : sx}(sx : sx)
  | AND
  | OR
  | XOR
  | SHL
  | SHR{sx : sx}(sx : sx)
  | ROTL
  | ROTR


  ;; 1-syntax.watsup
  syntax binop_{Fnn : Fnn}((Fnn : Fnn <: numtype)) =
  | ADD
  | SUB
  | MUL
  | DIV
  | MIN
  | MAX
  | COPYSIGN


;; 1-syntax.watsup
syntax testop_{Inn : Inn}((Inn : Inn <: numtype)) =
  | EQZ

;; 1-syntax.watsup
syntax relop_(numtype : numtype)
  ;; 1-syntax.watsup
  syntax relop_{Inn : Inn}((Inn : Inn <: numtype)) =
  | EQ
  | NE
  | LT{sx : sx}(sx : sx)
  | GT{sx : sx}(sx : sx)
  | LE{sx : sx}(sx : sx)
  | GE{sx : sx}(sx : sx)


  ;; 1-syntax.watsup
  syntax relop_{Fnn : Fnn}((Fnn : Fnn <: numtype)) =
  | EQ
  | NE
  | LT
  | GT
  | LE
  | GE


;; 1-syntax.watsup
syntax cvtop__(numtype_1 : numtype, numtype_2 : numtype)
  ;; 1-syntax.watsup
  syntax cvtop__{Inn_1 : Inn, Inn_2 : Inn}((Inn_1 : Inn <: numtype), (Inn_2 : Inn <: numtype)) =
  | EXTEND{sx : sx}(sx : sx)
    -- if ($sizenn1((Inn_1 : Inn <: numtype)) < $sizenn2((Inn_2 : Inn <: numtype)))
  | WRAP
    -- if ($sizenn1((Inn_1 : Inn <: numtype)) > $sizenn2((Inn_2 : Inn <: numtype)))


  ;; 1-syntax.watsup
  syntax cvtop__{Inn_1 : Inn, Fnn_2 : Fnn}((Inn_1 : Inn <: numtype), (Fnn_2 : Fnn <: numtype)) =
  | CONVERT{sx : sx}(sx : sx)
  | REINTERPRET
    -- if ($sizenn1((Inn_1 : Inn <: numtype)) = $sizenn2((Fnn_2 : Fnn <: numtype)))


  ;; 1-syntax.watsup
  syntax cvtop__{Fnn_1 : Fnn, Inn_2 : Inn}((Fnn_1 : Fnn <: numtype), (Inn_2 : Inn <: numtype)) =
  | TRUNC{sx : sx}(sx : sx)
  | TRUNC_SAT{sx : sx}(sx : sx)
  | REINTERPRET
    -- if ($sizenn1((Fnn_1 : Fnn <: numtype)) = $sizenn2((Inn_2 : Inn <: numtype)))


  ;; 1-syntax.watsup
  syntax cvtop__{Fnn_1 : Fnn, Fnn_2 : Fnn}((Fnn_1 : Fnn <: numtype), (Fnn_2 : Fnn <: numtype)) =
  | PROMOTE
    -- if ($sizenn1((Fnn_1 : Fnn <: numtype)) < $sizenn2((Fnn_2 : Fnn <: numtype)))
  | DEMOTE
    -- if ($sizenn1((Fnn_1 : Fnn <: numtype)) > $sizenn2((Fnn_2 : Fnn <: numtype)))


;; 1-syntax.watsup
syntax dim =
  | `%`{i : nat}(i : nat)
    -- if (((((i = 1) \/ (i = 2)) \/ (i = 4)) \/ (i = 8)) \/ (i = 16))

;; 1-syntax.watsup
syntax shape =
  | `%X%`{lanetype : lanetype, dim : dim}(lanetype : lanetype, dim : dim)
    -- if (($lsize(lanetype) * dim!`%`_dim.0) = 128)

;; 1-syntax.watsup
def $dim(shape : shape) : dim
  ;; 1-syntax.watsup
  def $dim{Lnn : Lnn, N : N}(`%X%`_shape(Lnn, `%`_dim(N))) = `%`_dim(N)

;; 1-syntax.watsup
def $lanetype(shape : shape) : lanetype
  ;; 1-syntax.watsup
  def $lanetype{Lnn : Lnn, N : N}(`%X%`_shape(Lnn, `%`_dim(N))) = Lnn

;; 1-syntax.watsup
def $unpackshape(shape : shape) : numtype
  ;; 1-syntax.watsup
  def $unpackshape{Lnn : Lnn, N : N}(`%X%`_shape(Lnn, `%`_dim(N))) = $lunpack(Lnn)

;; 1-syntax.watsup
syntax ishape =
  | `%`{shape : shape, Jnn : Jnn}(shape : shape)
    -- if ($lanetype(shape) = (Jnn : Jnn <: lanetype))

;; 1-syntax.watsup
syntax bshape =
  | `%`{shape : shape}(shape : shape)
    -- if ($lanetype(shape) = I8_lanetype)

;; 1-syntax.watsup
syntax half__(shape_1 : shape, shape_2 : shape)
  ;; 1-syntax.watsup
  syntax half__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M}(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))) =
  | LOW
  | HIGH
    -- if ((2 * $lsizenn1((Jnn_1 : Jnn <: lanetype))) = $lsizenn2((Jnn_2 : Jnn <: lanetype)))


  ;; 1-syntax.watsup
  syntax half__{Lnn_1 : Lnn, M_1 : M, Fnn_2 : Fnn, M_2 : M}(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape((Fnn_2 : Fnn <: lanetype), `%`_dim(M_2))) =
  | LOW
    -- if (((2 * $lsizenn1(Lnn_1)) = $sizenn2((Fnn_2 : Fnn <: numtype))) /\ ($sizenn2((Fnn_2 : Fnn <: numtype)) = 64))


;; 1-syntax.watsup
syntax zero__{Fnn_1 : Fnn, M_1 : M, Lnn_2 : Lnn, M_2 : M}(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)), `%X%`_shape(Lnn_2, `%`_dim(M_2))) =
  | ZERO
    -- if (((2 * $lsizenn2(Lnn_2)) = $sizenn1((Fnn_1 : Fnn <: numtype))) /\ ($sizenn1((Fnn_1 : Fnn <: numtype)) = 64))

;; 1-syntax.watsup
syntax vvunop =
  | NOT

;; 1-syntax.watsup
syntax vvbinop =
  | AND
  | ANDNOT
  | OR
  | XOR

;; 1-syntax.watsup
syntax vvternop =
  | BITSELECT

;; 1-syntax.watsup
syntax vvtestop =
  | ANY_TRUE

;; 1-syntax.watsup
syntax vunop_(shape : shape)
  ;; 1-syntax.watsup
  syntax vunop_{Jnn : Jnn, M : M}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))) =
  | ABS
  | NEG
  | POPCNT
    -- if ($lsizenn((Jnn : Jnn <: lanetype)) = 8)


  ;; 1-syntax.watsup
  syntax vunop_{Fnn : Fnn, M : M}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))) =
  | ABS
  | NEG
  | SQRT
  | CEIL
  | FLOOR
  | TRUNC
  | NEAREST


;; 1-syntax.watsup
syntax vbinop_(shape : shape)
  ;; 1-syntax.watsup
  syntax vbinop_{Jnn : Jnn, M : M}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))) =
  | ADD
  | SUB
  | ADD_SAT{sx : sx}(sx : sx)
    -- if ($lsizenn((Jnn : Jnn <: lanetype)) <= 16)
  | SUB_SAT{sx : sx}(sx : sx)
    -- if ($lsizenn((Jnn : Jnn <: lanetype)) <= 16)
  | MUL
    -- if ($lsizenn((Jnn : Jnn <: lanetype)) >= 16)
  | `AVGRU`
    -- if ($lsizenn((Jnn : Jnn <: lanetype)) <= 16)
  | `Q15MULR_SATS`
    -- if ($lsizenn((Jnn : Jnn <: lanetype)) = 16)
  | `RELAXED_Q15MULRS`
    -- if ($lsizenn((Jnn : Jnn <: lanetype)) = 16)
  | MIN{sx : sx}(sx : sx)
    -- if ($lsizenn((Jnn : Jnn <: lanetype)) <= 32)
  | MAX{sx : sx}(sx : sx)
    -- if ($lsizenn((Jnn : Jnn <: lanetype)) <= 32)


  ;; 1-syntax.watsup
  syntax vbinop_{Fnn : Fnn, M : M}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))) =
  | ADD
  | SUB
  | MUL
  | DIV
  | MIN
  | MAX
  | PMIN
  | PMAX
  | RELAXED_MIN
  | RELAXED_MAX


;; 1-syntax.watsup
syntax vternop_(shape : shape)
  ;; 1-syntax.watsup
  syntax vternop_{Jnn : Jnn, M : M}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))) =
  | RELAXED_LANESELECT


  ;; 1-syntax.watsup
  syntax vternop_{Fnn : Fnn, M : M}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))) =
  | RELAXED_MADD
  | RELAXED_NMADD


;; 1-syntax.watsup
syntax vtestop_{Jnn : Jnn, M : M}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))) =
  | ALL_TRUE

;; 1-syntax.watsup
syntax vrelop_(shape : shape)
  ;; 1-syntax.watsup
  syntax vrelop_{Jnn : Jnn, M : M}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))) =
  | EQ
  | NE
  | LT{sx : sx}(sx : sx)
    -- if (($lsizenn((Jnn : Jnn <: lanetype)) =/= 64) \/ (sx = S_sx))
  | GT{sx : sx}(sx : sx)
    -- if (($lsizenn((Jnn : Jnn <: lanetype)) =/= 64) \/ (sx = S_sx))
  | LE{sx : sx}(sx : sx)
    -- if (($lsizenn((Jnn : Jnn <: lanetype)) =/= 64) \/ (sx = S_sx))
  | GE{sx : sx}(sx : sx)
    -- if (($lsizenn((Jnn : Jnn <: lanetype)) =/= 64) \/ (sx = S_sx))


  ;; 1-syntax.watsup
  syntax vrelop_{Fnn : Fnn, M : M}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))) =
  | EQ
  | NE
  | LT
  | GT
  | LE
  | GE


;; 1-syntax.watsup
syntax vshiftop_{Jnn : Jnn, M : M}(`%`_ishape(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)))) =
  | SHL
  | SHR{sx : sx}(sx : sx)

;; 1-syntax.watsup
syntax vswizzlop_{M : M}(`%`_bshape(`%X%`_shape(I8_lanetype, `%`_dim(M)))) =
  | SWIZZLE
  | RELAXED_SWIZZLE

;; 1-syntax.watsup
syntax vextunop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M}(`%`_ishape(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))), `%`_ishape(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)))) =
  | EXTADD_PAIRWISE{sx : sx}(sx : sx)
    -- if ((16 <= (2 * $lsizenn1((Jnn_1 : Jnn <: lanetype)))) /\ (((2 * $lsizenn1((Jnn_1 : Jnn <: lanetype))) = $lsizenn2((Jnn_2 : Jnn <: lanetype))) /\ ($lsizenn2((Jnn_2 : Jnn <: lanetype)) <= 32)))

;; 1-syntax.watsup
syntax vextbinop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M}(`%`_ishape(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))), `%`_ishape(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)))) =
  | EXTMUL{sx : sx, half__ : half__(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)))}(sx : sx, half__ : half__(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))))
    -- if (((2 * $lsizenn1((Jnn_1 : Jnn <: lanetype))) = $lsizenn2((Jnn_2 : Jnn <: lanetype))) /\ ($lsizenn2((Jnn_2 : Jnn <: lanetype)) >= 16))
  | `DOTS`
    -- if (((2 * $lsizenn1((Jnn_1 : Jnn <: lanetype))) = $lsizenn2((Jnn_2 : Jnn <: lanetype))) /\ ($lsizenn2((Jnn_2 : Jnn <: lanetype)) = 32))
  | `RELAXED_DOTS`
    -- if (((2 * $lsizenn1((Jnn_1 : Jnn <: lanetype))) = $lsizenn2((Jnn_2 : Jnn <: lanetype))) /\ ($lsizenn2((Jnn_2 : Jnn <: lanetype)) = 16))

;; 1-syntax.watsup
syntax vextternop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M}(`%`_ishape(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))), `%`_ishape(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)))) =
  | `RELAXED_DOT_ADDS`
    -- if (((4 * $lsizenn1((Jnn_1 : Jnn <: lanetype))) = $lsizenn2((Jnn_2 : Jnn <: lanetype))) /\ ($lsizenn2((Jnn_2 : Jnn <: lanetype)) = 32))

;; 1-syntax.watsup
syntax vcvtop__(shape_1 : shape, shape_2 : shape)
  ;; 1-syntax.watsup
  syntax vcvtop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M}(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))) =
  | EXTEND{sx : sx}(sx : sx)
    -- if ($lsizenn2((Jnn_2 : Jnn <: lanetype)) = (2 * $lsizenn1((Jnn_1 : Jnn <: lanetype))))


  ;; 1-syntax.watsup
  syntax vcvtop__{Jnn_1 : Jnn, M_1 : M, Fnn_2 : Fnn, M_2 : M}(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Fnn_2 : Fnn <: lanetype), `%`_dim(M_2))) =
  | CONVERT{sx : sx}(sx : sx)
    -- if (($sizenn2((Fnn_2 : Fnn <: numtype)) >= $lsizenn1((Jnn_1 : Jnn <: lanetype))) /\ ($lsizenn1((Jnn_1 : Jnn <: lanetype)) = 32))


  ;; 1-syntax.watsup
  syntax vcvtop__{Fnn_1 : Fnn, M_1 : M, Jnn_2 : Jnn, M_2 : M}(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))) =
  | TRUNC_SAT{sx : sx}(sx : sx)
    -- if (($sizenn1((Fnn_1 : Fnn <: numtype)) >= $lsizenn2((Jnn_2 : Jnn <: lanetype))) /\ ($lsizenn2((Jnn_2 : Jnn <: lanetype)) = 32))
  | RELAXED_TRUNC{sx : sx}(sx : sx)
    -- if (($sizenn1((Fnn_1 : Fnn <: numtype)) >= $lsizenn2((Jnn_2 : Jnn <: lanetype))) /\ ($lsizenn2((Jnn_2 : Jnn <: lanetype)) = 32))


  ;; 1-syntax.watsup
  syntax vcvtop__{Fnn_1 : Fnn, M_1 : M, Fnn_2 : Fnn, M_2 : M}(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Fnn_2 : Fnn <: lanetype), `%`_dim(M_2))) =
  | DEMOTE
    -- if ($sizenn1((Fnn_1 : Fnn <: numtype)) > $sizenn2((Fnn_2 : Fnn <: numtype)))
  | PROMOTE
    -- if ($sizenn1((Fnn_1 : Fnn <: numtype)) < $sizenn2((Fnn_2 : Fnn <: numtype)))


;; 1-syntax.watsup
syntax memarg =
{
  ALIGN{u32 : u32} u32,
  OFFSET{u32 : u32} u32
}

;; 1-syntax.watsup
syntax loadop_{Inn : Inn}((Inn : Inn <: numtype)) =
  | `%_%`{sz : sz, sx : sx}(sz : sz, sx : sx)
    -- if (sz!`%`_sz.0 < $sizenn((Inn : Inn <: numtype)))

;; 1-syntax.watsup
syntax storeop_{Inn : Inn}((Inn : Inn <: numtype)) =
  | `%`{sz : sz}(sz : sz)
    -- if (sz!`%`_sz.0 < $sizenn((Inn : Inn <: numtype)))

;; 1-syntax.watsup
syntax vloadop_{vectype : vectype}(vectype) =
  | `SHAPE%X%_%`{sz : sz, M : M, sx : sx}(sz : sz, M : M, sx : sx)
    -- if (((sz!`%`_sz.0 * M) : nat <:> rat) = (($vsize(vectype) : nat <:> rat) / (2 : nat <:> rat)))
  | SPLAT{sz : sz}(sz : sz)
  | ZERO{sz : sz}(sz : sz)
    -- if (sz!`%`_sz.0 >= 32)

;; 1-syntax.watsup
syntax blocktype =
  | _RESULT{`valtype?` : valtype?}(valtype?{valtype <- `valtype?`} : valtype?)
  | _IDX{funcidx : funcidx}(funcidx : funcidx)

;; 5-runtime.watsup
syntax addr = nat

;; 5-runtime.watsup
syntax arrayaddr = addr

;; 5-runtime.watsup
syntax exnaddr = addr

;; 5-runtime.watsup
syntax funcaddr = addr

;; 5-runtime.watsup
syntax hostaddr = addr

;; 5-runtime.watsup
syntax structaddr = addr

;; 5-runtime.watsup
rec {

;; 5-runtime.watsup:33.1-40.23
syntax addrref =
  | REF.I31_NUM{u31 : u31}(u31 : u31)
  | REF.STRUCT_ADDR{structaddr : structaddr}(structaddr : structaddr)
  | REF.ARRAY_ADDR{arrayaddr : arrayaddr}(arrayaddr : arrayaddr)
  | REF.FUNC_ADDR{funcaddr : funcaddr}(funcaddr : funcaddr)
  | REF.EXN_ADDR{exnaddr : exnaddr}(exnaddr : exnaddr)
  | REF.HOST_ADDR{hostaddr : hostaddr}(hostaddr : hostaddr)
  | REF.EXTERN{addrref : addrref}(addrref : addrref)
}

;; 1-syntax.watsup
syntax catch =
  | CATCH{tagidx : tagidx, labelidx : labelidx}(tagidx : tagidx, labelidx : labelidx)
  | CATCH_REF{tagidx : tagidx, labelidx : labelidx}(tagidx : tagidx, labelidx : labelidx)
  | CATCH_ALL{labelidx : labelidx}(labelidx : labelidx)
  | CATCH_ALL_REF{labelidx : labelidx}(labelidx : labelidx)

;; 5-runtime.watsup
syntax dataaddr = addr

;; 5-runtime.watsup
syntax elemaddr = addr

;; 5-runtime.watsup
syntax globaladdr = addr

;; 5-runtime.watsup
syntax memaddr = addr

;; 5-runtime.watsup
syntax tableaddr = addr

;; 5-runtime.watsup
syntax tagaddr = addr

;; 5-runtime.watsup
syntax externaddr =
  | FUNC{funcaddr : funcaddr}(funcaddr : funcaddr)
  | GLOBAL{globaladdr : globaladdr}(globaladdr : globaladdr)
  | TABLE{tableaddr : tableaddr}(tableaddr : tableaddr)
  | MEM{memaddr : memaddr}(memaddr : memaddr)
  | TAG{tagaddr : tagaddr}(tagaddr : tagaddr)

;; 5-runtime.watsup
syntax exportinst =
{
  NAME{name : name} name,
  ADDR{externaddr : externaddr} externaddr
}

;; 5-runtime.watsup
syntax moduleinst =
{
  TYPES{`deftype*` : deftype*} deftype*,
  FUNCS{`funcaddr*` : funcaddr*} funcaddr*,
  GLOBALS{`globaladdr*` : globaladdr*} globaladdr*,
  TABLES{`tableaddr*` : tableaddr*} tableaddr*,
  MEMS{`memaddr*` : memaddr*} memaddr*,
  TAGS{`tagaddr*` : tagaddr*} tagaddr*,
  ELEMS{`elemaddr*` : elemaddr*} elemaddr*,
  DATAS{`dataaddr*` : dataaddr*} dataaddr*,
  EXPORTS{`exportinst*` : exportinst*} exportinst*
}

;; 5-runtime.watsup
syntax val =
  | CONST{numtype : numtype, num_ : num_(numtype)}(numtype : numtype, num_ : num_(numtype))
  | VCONST{vectype : vectype, vec_ : vec_(vectype)}(vectype : vectype, vec_ : vec_(vectype))
  | REF.NULL{heaptype : heaptype}(heaptype : heaptype)
  | REF.I31_NUM{u31 : u31}(u31 : u31)
  | REF.STRUCT_ADDR{structaddr : structaddr}(structaddr : structaddr)
  | REF.ARRAY_ADDR{arrayaddr : arrayaddr}(arrayaddr : arrayaddr)
  | REF.FUNC_ADDR{funcaddr : funcaddr}(funcaddr : funcaddr)
  | REF.EXN_ADDR{exnaddr : exnaddr}(exnaddr : exnaddr)
  | REF.HOST_ADDR{hostaddr : hostaddr}(hostaddr : hostaddr)
  | REF.EXTERN{addrref : addrref}(addrref : addrref)

;; 5-runtime.watsup
syntax frame =
{
  LOCALS{`val?*` : val?*} val?*,
  MODULE{moduleinst : moduleinst} moduleinst
}

;; 5-runtime.watsup
rec {

;; 5-runtime.watsup:157.1-163.9
syntax instr =
  | NOP
  | UNREACHABLE
  | DROP
  | SELECT{`valtype*?` : valtype*?}(valtype*{valtype <- `valtype*`}?{`valtype*` <- `valtype*?`} : valtype*?)
  | BLOCK{blocktype : blocktype, `instr*` : instr*}(blocktype : blocktype, instr*{instr <- `instr*`} : instr*)
  | LOOP{blocktype : blocktype, `instr*` : instr*}(blocktype : blocktype, instr*{instr <- `instr*`} : instr*)
  | `IF%%ELSE%`{blocktype : blocktype, `instr*` : instr*}(blocktype : blocktype, instr*{instr <- `instr*`} : instr*, instr*)
  | BR{labelidx : labelidx}(labelidx : labelidx)
  | BR_IF{labelidx : labelidx}(labelidx : labelidx)
  | BR_TABLE{`labelidx*` : labelidx*}(labelidx*{labelidx <- `labelidx*`} : labelidx*, labelidx)
  | BR_ON_NULL{labelidx : labelidx}(labelidx : labelidx)
  | BR_ON_NON_NULL{labelidx : labelidx}(labelidx : labelidx)
  | BR_ON_CAST{labelidx : labelidx, reftype : reftype}(labelidx : labelidx, reftype : reftype, reftype)
  | BR_ON_CAST_FAIL{labelidx : labelidx, reftype : reftype}(labelidx : labelidx, reftype : reftype, reftype)
  | CALL{funcidx : funcidx}(funcidx : funcidx)
  | CALL_REF{typeuse : typeuse}(typeuse : typeuse)
  | CALL_INDIRECT{tableidx : tableidx, typeuse : typeuse}(tableidx : tableidx, typeuse : typeuse)
  | RETURN
  | RETURN_CALL{funcidx : funcidx}(funcidx : funcidx)
  | RETURN_CALL_REF{typeuse : typeuse}(typeuse : typeuse)
  | RETURN_CALL_INDIRECT{tableidx : tableidx, typeuse : typeuse}(tableidx : tableidx, typeuse : typeuse)
  | THROW{tagidx : tagidx}(tagidx : tagidx)
  | THROW_REF
  | TRY_TABLE{blocktype : blocktype, list : list(syntax catch), `instr*` : instr*}(blocktype : blocktype, list : list(syntax catch), instr*{instr <- `instr*`} : instr*)
  | CONST{numtype : numtype, num_ : num_(numtype)}(numtype : numtype, num_ : num_(numtype))
  | UNOP{numtype : numtype, unop_ : unop_(numtype)}(numtype : numtype, unop_ : unop_(numtype))
  | BINOP{numtype : numtype, binop_ : binop_(numtype)}(numtype : numtype, binop_ : binop_(numtype))
  | TESTOP{numtype : numtype, testop_ : testop_(numtype)}(numtype : numtype, testop_ : testop_(numtype))
  | RELOP{numtype : numtype, relop_ : relop_(numtype)}(numtype : numtype, relop_ : relop_(numtype))
  | CVTOP{numtype_1 : numtype, numtype_2 : numtype, cvtop__ : cvtop__(numtype_2, numtype_1)}(numtype_1 : numtype, numtype_2 : numtype, cvtop__ : cvtop__(numtype_2, numtype_1))
  | VCONST{vectype : vectype, vec_ : vec_(vectype)}(vectype : vectype, vec_ : vec_(vectype))
  | VVUNOP{vectype : vectype, vvunop : vvunop}(vectype : vectype, vvunop : vvunop)
  | VVBINOP{vectype : vectype, vvbinop : vvbinop}(vectype : vectype, vvbinop : vvbinop)
  | VVTERNOP{vectype : vectype, vvternop : vvternop}(vectype : vectype, vvternop : vvternop)
  | VVTESTOP{vectype : vectype, vvtestop : vvtestop}(vectype : vectype, vvtestop : vvtestop)
  | VUNOP{shape : shape, vunop_ : vunop_(shape)}(shape : shape, vunop_ : vunop_(shape))
  | VBINOP{shape : shape, vbinop_ : vbinop_(shape)}(shape : shape, vbinop_ : vbinop_(shape))
  | VTERNOP{shape : shape, vternop_ : vternop_(shape)}(shape : shape, vternop_ : vternop_(shape))
  | VTESTOP{shape : shape, vtestop_ : vtestop_(shape)}(shape : shape, vtestop_ : vtestop_(shape))
  | VRELOP{shape : shape, vrelop_ : vrelop_(shape)}(shape : shape, vrelop_ : vrelop_(shape))
  | VSHIFTOP{ishape : ishape, vshiftop_ : vshiftop_(ishape)}(ishape : ishape, vshiftop_ : vshiftop_(ishape))
  | VBITMASK{ishape : ishape}(ishape : ishape)
  | VSWIZZLOP{bshape : bshape, vswizzlop_ : vswizzlop_(bshape)}(bshape : bshape, vswizzlop_ : vswizzlop_(bshape))
  | VSHUFFLE{bshape : bshape, `laneidx*` : laneidx*}(bshape : bshape, laneidx*{laneidx <- `laneidx*`} : laneidx*)
    -- if (`%`_dim(|laneidx*{laneidx <- `laneidx*`}|) = $dim(bshape!`%`_bshape.0))
  | VEXTUNOP{ishape_1 : ishape, ishape_2 : ishape, vextunop__ : vextunop__(ishape_2, ishape_1)}(ishape_1 : ishape, ishape_2 : ishape, vextunop__ : vextunop__(ishape_2, ishape_1))
  | VEXTBINOP{ishape_1 : ishape, ishape_2 : ishape, vextbinop__ : vextbinop__(ishape_2, ishape_1)}(ishape_1 : ishape, ishape_2 : ishape, vextbinop__ : vextbinop__(ishape_2, ishape_1))
  | VEXTTERNOP{ishape_1 : ishape, ishape_2 : ishape, vextternop__ : vextternop__(ishape_2, ishape_1)}(ishape_1 : ishape, ishape_2 : ishape, vextternop__ : vextternop__(ishape_2, ishape_1))
  | VNARROW{ishape_1 : ishape, ishape_2 : ishape, sx : sx}(ishape_1 : ishape, ishape_2 : ishape, sx : sx)
    -- if (($lsize($lanetype(ishape_2!`%`_ishape.0)) = (2 * $lsize($lanetype(ishape_1!`%`_ishape.0)))) /\ ((2 * $lsize($lanetype(ishape_1!`%`_ishape.0))) <= 32))
  | VCVTOP{shape_1 : shape, shape_2 : shape, vcvtop__ : vcvtop__(shape_2, shape_1), `half__?` : half__(shape_2, shape_1)?, `zero__?` : zero__(shape_2, shape_1)?}(shape_1 : shape, shape_2 : shape, vcvtop__ : vcvtop__(shape_2, shape_1), half__?{half__ <- `half__?`} : half__(shape_2, shape_1)?, zero__?{zero__ <- `zero__?`} : zero__(shape_2, shape_1)?)
  | VSPLAT{shape : shape}(shape : shape)
  | VEXTRACT_LANE{shape : shape, `sx?` : sx?, laneidx : laneidx, numtype : numtype}(shape : shape, sx?{sx <- `sx?`} : sx?, laneidx : laneidx)
    -- if ((sx?{sx <- `sx?`} = ?()) <=> ($lanetype(shape) = (numtype : numtype <: lanetype)))
  | VREPLACE_LANE{shape : shape, laneidx : laneidx}(shape : shape, laneidx : laneidx)
  | REF.NULL{heaptype : heaptype}(heaptype : heaptype)
  | REF.IS_NULL
  | REF.AS_NON_NULL
  | REF.EQ
  | REF.TEST{reftype : reftype}(reftype : reftype)
  | REF.CAST{reftype : reftype}(reftype : reftype)
  | REF.FUNC{funcidx : funcidx}(funcidx : funcidx)
  | REF.I31
  | I31.GET{sx : sx}(sx : sx)
  | STRUCT.NEW{typeidx : typeidx}(typeidx : typeidx)
  | STRUCT.NEW_DEFAULT{typeidx : typeidx}(typeidx : typeidx)
  | STRUCT.GET{`sx?` : sx?, typeidx : typeidx, u32 : u32}(sx?{sx <- `sx?`} : sx?, typeidx : typeidx, u32 : u32)
  | STRUCT.SET{typeidx : typeidx, u32 : u32}(typeidx : typeidx, u32 : u32)
  | ARRAY.NEW{typeidx : typeidx}(typeidx : typeidx)
  | ARRAY.NEW_DEFAULT{typeidx : typeidx}(typeidx : typeidx)
  | ARRAY.NEW_FIXED{typeidx : typeidx, u32 : u32}(typeidx : typeidx, u32 : u32)
  | ARRAY.NEW_DATA{typeidx : typeidx, dataidx : dataidx}(typeidx : typeidx, dataidx : dataidx)
  | ARRAY.NEW_ELEM{typeidx : typeidx, elemidx : elemidx}(typeidx : typeidx, elemidx : elemidx)
  | ARRAY.GET{`sx?` : sx?, typeidx : typeidx}(sx?{sx <- `sx?`} : sx?, typeidx : typeidx)
  | ARRAY.SET{typeidx : typeidx}(typeidx : typeidx)
  | ARRAY.LEN
  | ARRAY.FILL{typeidx : typeidx}(typeidx : typeidx)
  | ARRAY.COPY{typeidx : typeidx}(typeidx : typeidx, typeidx)
  | ARRAY.INIT_DATA{typeidx : typeidx, dataidx : dataidx}(typeidx : typeidx, dataidx : dataidx)
  | ARRAY.INIT_ELEM{typeidx : typeidx, elemidx : elemidx}(typeidx : typeidx, elemidx : elemidx)
  | EXTERN.CONVERT_ANY
  | ANY.CONVERT_EXTERN
  | LOCAL.GET{localidx : localidx}(localidx : localidx)
  | LOCAL.SET{localidx : localidx}(localidx : localidx)
  | LOCAL.TEE{localidx : localidx}(localidx : localidx)
  | GLOBAL.GET{globalidx : globalidx}(globalidx : globalidx)
  | GLOBAL.SET{globalidx : globalidx}(globalidx : globalidx)
  | TABLE.GET{tableidx : tableidx}(tableidx : tableidx)
  | TABLE.SET{tableidx : tableidx}(tableidx : tableidx)
  | TABLE.SIZE{tableidx : tableidx}(tableidx : tableidx)
  | TABLE.GROW{tableidx : tableidx}(tableidx : tableidx)
  | TABLE.FILL{tableidx : tableidx}(tableidx : tableidx)
  | TABLE.COPY{tableidx : tableidx}(tableidx : tableidx, tableidx)
  | TABLE.INIT{tableidx : tableidx, elemidx : elemidx}(tableidx : tableidx, elemidx : elemidx)
  | ELEM.DROP{elemidx : elemidx}(elemidx : elemidx)
  | LOAD{numtype : numtype, `loadop_?` : loadop_(numtype)?, memidx : memidx, memarg : memarg}(numtype : numtype, loadop_?{loadop_ <- `loadop_?`} : loadop_(numtype)?, memidx : memidx, memarg : memarg)
  | STORE{numtype : numtype, `storeop_?` : storeop_(numtype)?, memidx : memidx, memarg : memarg}(numtype : numtype, storeop_?{storeop_ <- `storeop_?`} : storeop_(numtype)?, memidx : memidx, memarg : memarg)
  | VLOAD{vectype : vectype, `vloadop_?` : vloadop_(vectype)?, memidx : memidx, memarg : memarg}(vectype : vectype, vloadop_?{vloadop_ <- `vloadop_?`} : vloadop_(vectype)?, memidx : memidx, memarg : memarg)
  | VLOAD_LANE{vectype : vectype, sz : sz, memidx : memidx, memarg : memarg, laneidx : laneidx}(vectype : vectype, sz : sz, memidx : memidx, memarg : memarg, laneidx : laneidx)
  | VSTORE{vectype : vectype, memidx : memidx, memarg : memarg}(vectype : vectype, memidx : memidx, memarg : memarg)
  | VSTORE_LANE{vectype : vectype, sz : sz, memidx : memidx, memarg : memarg, laneidx : laneidx}(vectype : vectype, sz : sz, memidx : memidx, memarg : memarg, laneidx : laneidx)
  | MEMORY.SIZE{memidx : memidx}(memidx : memidx)
  | MEMORY.GROW{memidx : memidx}(memidx : memidx)
  | MEMORY.FILL{memidx : memidx}(memidx : memidx)
  | MEMORY.COPY{memidx : memidx}(memidx : memidx, memidx)
  | MEMORY.INIT{memidx : memidx, dataidx : dataidx}(memidx : memidx, dataidx : dataidx)
  | DATA.DROP{dataidx : dataidx}(dataidx : dataidx)
  | REF.I31_NUM{u31 : u31}(u31 : u31)
  | REF.STRUCT_ADDR{structaddr : structaddr}(structaddr : structaddr)
  | REF.ARRAY_ADDR{arrayaddr : arrayaddr}(arrayaddr : arrayaddr)
  | REF.FUNC_ADDR{funcaddr : funcaddr}(funcaddr : funcaddr)
  | REF.EXN_ADDR{exnaddr : exnaddr}(exnaddr : exnaddr)
  | REF.HOST_ADDR{hostaddr : hostaddr}(hostaddr : hostaddr)
  | REF.EXTERN{addrref : addrref}(addrref : addrref)
  | `LABEL_%{%}%`{n : n, `instr*` : instr*}(n : n, instr*{instr <- `instr*`} : instr*, instr*)
  | `FRAME_%{%}%`{n : n, frame : frame, `instr*` : instr*}(n : n, frame : frame, instr*{instr <- `instr*`} : instr*)
  | `HANDLER_%{%}%`{n : n, `catch*` : catch*, `instr*` : instr*}(n : n, catch*{catch <- `catch*`} : catch*, instr*{instr <- `instr*`} : instr*)
  | TRAP
}

;; 1-syntax.watsup
syntax expr = instr*

;; 1-syntax.watsup
syntax elemmode =
  | ACTIVE{tableidx : tableidx, expr : expr}(tableidx : tableidx, expr : expr)
  | PASSIVE
  | DECLARE

;; 1-syntax.watsup
syntax datamode =
  | ACTIVE{memidx : memidx, expr : expr}(memidx : memidx, expr : expr)
  | PASSIVE

;; 1-syntax.watsup
syntax type =
  | TYPE{rectype : rectype}(rectype : rectype)

;; 1-syntax.watsup
syntax local =
  | LOCAL{valtype : valtype}(valtype : valtype)

;; 1-syntax.watsup
syntax func =
  | FUNC{typeidx : typeidx, `local*` : local*, expr : expr}(typeidx : typeidx, local*{local <- `local*`} : local*, expr : expr)

;; 1-syntax.watsup
syntax global =
  | GLOBAL{globaltype : globaltype, expr : expr}(globaltype : globaltype, expr : expr)

;; 1-syntax.watsup
syntax table =
  | TABLE{tabletype : tabletype, expr : expr}(tabletype : tabletype, expr : expr)

;; 1-syntax.watsup
syntax mem =
  | MEMORY{memtype : memtype}(memtype : memtype)

;; 1-syntax.watsup
syntax tag =
  | TAG{typeidx : typeidx}(typeidx : typeidx)

;; 1-syntax.watsup
syntax elem =
  | ELEM{reftype : reftype, `expr*` : expr*, elemmode : elemmode}(reftype : reftype, expr*{expr <- `expr*`} : expr*, elemmode : elemmode)

;; 1-syntax.watsup
syntax data =
  | DATA{`byte*` : byte*, datamode : datamode}(byte*{byte <- `byte*`} : byte*, datamode : datamode)

;; 1-syntax.watsup
syntax start =
  | START{funcidx : funcidx}(funcidx : funcidx)

;; 1-syntax.watsup
syntax export =
  | EXPORT{name : name, externidx : externidx}(name : name, externidx : externidx)

;; 1-syntax.watsup
syntax import =
  | IMPORT{name : name, externtype : externtype}(name : name, name, externtype : externtype)

;; 1-syntax.watsup
syntax module =
  | MODULE{`type*` : type*, `import*` : import*, `func*` : func*, `global*` : global*, `table*` : table*, `mem*` : mem*, `tag*` : tag*, `elem*` : elem*, `data*` : data*, `start?` : start?, `export*` : export*}(type*{type <- `type*`} : type*, import*{import <- `import*`} : import*, func*{func <- `func*`} : func*, global*{global <- `global*`} : global*, table*{table <- `table*`} : table*, mem*{mem <- `mem*`} : mem*, tag*{tag <- `tag*`} : tag*, elem*{elem <- `elem*`} : elem*, data*{data <- `data*`} : data*, start?{start <- `start?`} : start?, export*{export <- `export*`} : export*)

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:9.1-9.86
def $funcsxx(externidx*) : typeidx*
  ;; 2-syntax-aux.watsup:15.1-15.24
  def $funcsxx([]) = []
  ;; 2-syntax-aux.watsup:16.1-16.45
  def $funcsxx{x : idx, `xx*` : externidx*}([FUNC_externidx(x)] ++ xx*{xx <- `xx*`}) = [x] ++ $funcsxx(xx*{xx <- `xx*`})
  ;; 2-syntax-aux.watsup:17.1-17.58
  def $funcsxx{externidx : externidx, `xx*` : externidx*}([externidx] ++ xx*{xx <- `xx*`}) = $funcsxx(xx*{xx <- `xx*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:10.1-10.88
def $globalsxx(externidx*) : globalidx*
  ;; 2-syntax-aux.watsup:19.1-19.26
  def $globalsxx([]) = []
  ;; 2-syntax-aux.watsup:20.1-20.51
  def $globalsxx{x : idx, `xx*` : externidx*}([GLOBAL_externidx(x)] ++ xx*{xx <- `xx*`}) = [x] ++ $globalsxx(xx*{xx <- `xx*`})
  ;; 2-syntax-aux.watsup:21.1-21.62
  def $globalsxx{externidx : externidx, `xx*` : externidx*}([externidx] ++ xx*{xx <- `xx*`}) = $globalsxx(xx*{xx <- `xx*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:11.1-11.87
def $tablesxx(externidx*) : tableidx*
  ;; 2-syntax-aux.watsup:23.1-23.25
  def $tablesxx([]) = []
  ;; 2-syntax-aux.watsup:24.1-24.48
  def $tablesxx{x : idx, `xx*` : externidx*}([TABLE_externidx(x)] ++ xx*{xx <- `xx*`}) = [x] ++ $tablesxx(xx*{xx <- `xx*`})
  ;; 2-syntax-aux.watsup:25.1-25.60
  def $tablesxx{externidx : externidx, `xx*` : externidx*}([externidx] ++ xx*{xx <- `xx*`}) = $tablesxx(xx*{xx <- `xx*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:12.1-12.85
def $memsxx(externidx*) : memidx*
  ;; 2-syntax-aux.watsup:27.1-27.23
  def $memsxx([]) = []
  ;; 2-syntax-aux.watsup:28.1-28.42
  def $memsxx{x : idx, `xx*` : externidx*}([MEM_externidx(x)] ++ xx*{xx <- `xx*`}) = [x] ++ $memsxx(xx*{xx <- `xx*`})
  ;; 2-syntax-aux.watsup:29.1-29.56
  def $memsxx{externidx : externidx, `xx*` : externidx*}([externidx] ++ xx*{xx <- `xx*`}) = $memsxx(xx*{xx <- `xx*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:13.1-13.85
def $tagsxx(externidx*) : tagidx*
  ;; 2-syntax-aux.watsup:31.1-31.23
  def $tagsxx([]) = []
  ;; 2-syntax-aux.watsup:32.1-32.42
  def $tagsxx{x : idx, `xx*` : externidx*}([TAG_externidx(x)] ++ xx*{xx <- `xx*`}) = [x] ++ $tagsxx(xx*{xx <- `xx*`})
  ;; 2-syntax-aux.watsup:33.1-33.56
  def $tagsxx{externidx : externidx, `xx*` : externidx*}([externidx] ++ xx*{xx <- `xx*`}) = $tagsxx(xx*{xx <- `xx*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
def $IN(N : N) : Inn
  ;; 2-syntax-aux.watsup
  def $IN(32) = I32_Inn
  ;; 2-syntax-aux.watsup
  def $IN(64) = I64_Inn

;; 2-syntax-aux.watsup
def $FN(N : N) : Fnn
  ;; 2-syntax-aux.watsup
  def $FN(32) = F32_Fnn
  ;; 2-syntax-aux.watsup
  def $FN(64) = F64_Fnn

;; 2-syntax-aux.watsup
def $JN(N : N) : Jnn
  ;; 2-syntax-aux.watsup
  def $JN(8) = I8_Jnn
  ;; 2-syntax-aux.watsup
  def $JN(16) = I16_Jnn
  ;; 2-syntax-aux.watsup
  def $JN(32) = I32_Jnn
  ;; 2-syntax-aux.watsup
  def $JN(64) = I64_Jnn

;; 2-syntax-aux.watsup
def $minat(addrtype : addrtype, addrtype : addrtype) : addrtype
  ;; 2-syntax-aux.watsup
  def $minat{at_1 : addrtype, at_2 : addrtype}(at_1, at_2) = at_1
    -- if ($size((at_1 : addrtype <: numtype)) <= $size((at_2 : addrtype <: numtype)))
  ;; 2-syntax-aux.watsup
  def $minat{at_1 : addrtype, at_2 : addrtype}(at_1, at_2) = at_2
    -- otherwise

;; 2-syntax-aux.watsup
def $diffrt(reftype : reftype, reftype : reftype) : reftype
  ;; 2-syntax-aux.watsup
  def $diffrt{nul1 : nul1, ht_1 : heaptype, ht_2 : heaptype}(REF_reftype(nul1, ht_1), REF_reftype(?(NULL_NULL), ht_2)) = REF_reftype(?(), ht_1)
  ;; 2-syntax-aux.watsup
  def $diffrt{nul1 : nul1, ht_1 : heaptype, ht_2 : heaptype}(REF_reftype(nul1, ht_1), REF_reftype(?(), ht_2)) = REF_reftype(nul1, ht_1)

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:75.1-75.88
def $funcsxt(externtype*) : deftype*
  ;; 2-syntax-aux.watsup:81.1-81.24
  def $funcsxt([]) = []
  ;; 2-syntax-aux.watsup:82.1-82.47
  def $funcsxt{dt : deftype, `xt*` : externtype*}([FUNC_externtype((dt : deftype <: typeuse))] ++ xt*{xt <- `xt*`}) = [dt] ++ $funcsxt(xt*{xt <- `xt*`})
  ;; 2-syntax-aux.watsup:83.1-83.59
  def $funcsxt{externtype : externtype, `xt*` : externtype*}([externtype] ++ xt*{xt <- `xt*`}) = $funcsxt(xt*{xt <- `xt*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:76.1-76.90
def $globalsxt(externtype*) : globaltype*
  ;; 2-syntax-aux.watsup:85.1-85.26
  def $globalsxt([]) = []
  ;; 2-syntax-aux.watsup:86.1-86.53
  def $globalsxt{gt : globaltype, `xt*` : externtype*}([GLOBAL_externtype(gt)] ++ xt*{xt <- `xt*`}) = [gt] ++ $globalsxt(xt*{xt <- `xt*`})
  ;; 2-syntax-aux.watsup:87.1-87.63
  def $globalsxt{externtype : externtype, `xt*` : externtype*}([externtype] ++ xt*{xt <- `xt*`}) = $globalsxt(xt*{xt <- `xt*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:77.1-77.89
def $tablesxt(externtype*) : tabletype*
  ;; 2-syntax-aux.watsup:89.1-89.25
  def $tablesxt([]) = []
  ;; 2-syntax-aux.watsup:90.1-90.50
  def $tablesxt{tt : tabletype, `xt*` : externtype*}([TABLE_externtype(tt)] ++ xt*{xt <- `xt*`}) = [tt] ++ $tablesxt(xt*{xt <- `xt*`})
  ;; 2-syntax-aux.watsup:91.1-91.61
  def $tablesxt{externtype : externtype, `xt*` : externtype*}([externtype] ++ xt*{xt <- `xt*`}) = $tablesxt(xt*{xt <- `xt*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:78.1-78.87
def $memsxt(externtype*) : memtype*
  ;; 2-syntax-aux.watsup:93.1-93.23
  def $memsxt([]) = []
  ;; 2-syntax-aux.watsup:94.1-94.44
  def $memsxt{mt : memtype, `xt*` : externtype*}([MEM_externtype(mt)] ++ xt*{xt <- `xt*`}) = [mt] ++ $memsxt(xt*{xt <- `xt*`})
  ;; 2-syntax-aux.watsup:95.1-95.57
  def $memsxt{externtype : externtype, `xt*` : externtype*}([externtype] ++ xt*{xt <- `xt*`}) = $memsxt(xt*{xt <- `xt*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:79.1-79.87
def $tagsxt(externtype*) : tagtype*
  ;; 2-syntax-aux.watsup:97.1-97.23
  def $tagsxt([]) = []
  ;; 2-syntax-aux.watsup:98.1-98.44
  def $tagsxt{jt : tagtype, `xt*` : externtype*}([TAG_externtype((jt : deftype <: typeuse))] ++ xt*{xt <- `xt*`}) = [jt] ++ $tagsxt(xt*{xt <- `xt*`})
  ;; 2-syntax-aux.watsup:99.1-99.57
  def $tagsxt{externtype : externtype, `xt*` : externtype*}([externtype] ++ xt*{xt <- `xt*`}) = $tagsxt(xt*{xt <- `xt*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:104.1-104.112
def $subst_typevar(typevar : typevar, typevar*, typeuse*) : typeuse
  ;; 2-syntax-aux.watsup:133.1-133.38
  def $subst_typevar{tv : typevar}(tv, [], []) = (tv : typevar <: typeuse)
  ;; 2-syntax-aux.watsup:134.1-134.95
  def $subst_typevar{tv : typevar, tv_1 : typevar, `tv'*` : typevar*, tu_1 : typeuse, `tu'*` : typeuse*}(tv, [tv_1] ++ tv'*{tv' <- `tv'*`}, [tu_1] ++ tu'*{tu' <- `tu'*`}) = tu_1
    -- if (tv = tv_1)
  ;; 2-syntax-aux.watsup:135.1-135.92
  def $subst_typevar{tv : typevar, tv_1 : typevar, `tv'*` : typevar*, tu_1 : typeuse, `tu'*` : typeuse*}(tv, [tv_1] ++ tv'*{tv' <- `tv'*`}, [tu_1] ++ tu'*{tu' <- `tu'*`}) = $subst_typevar(tv, tv'*{tv' <- `tv'*`}, tu'*{tu' <- `tu'*`})
    -- otherwise
}

;; 2-syntax-aux.watsup
def $subst_packtype(packtype : packtype, typevar*, typeuse*) : packtype
  ;; 2-syntax-aux.watsup
  def $subst_packtype{pt : packtype, `tv*` : typevar*, `tu*` : typeuse*}(pt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = pt

;; 2-syntax-aux.watsup
def $subst_numtype(numtype : numtype, typevar*, typeuse*) : numtype
  ;; 2-syntax-aux.watsup
  def $subst_numtype{nt : numtype, `tv*` : typevar*, `tu*` : typeuse*}(nt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = nt

;; 2-syntax-aux.watsup
def $subst_vectype(vectype : vectype, typevar*, typeuse*) : vectype
  ;; 2-syntax-aux.watsup
  def $subst_vectype{vt : vectype, `tv*` : typevar*, `tu*` : typeuse*}(vt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = vt

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:105.1-105.112
def $subst_typeuse(typeuse : typeuse, typevar*, typeuse*) : typeuse
  ;; 2-syntax-aux.watsup:137.1-137.66
  def $subst_typeuse{tv' : typevar, `tv*` : typevar*, `tu*` : typeuse*}((tv' : typevar <: typeuse), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = $subst_typevar(tv', tv*{tv <- `tv*`}, tu*{tu <- `tu*`})
  ;; 2-syntax-aux.watsup:138.1-138.64
  def $subst_typeuse{dt : deftype, `tv*` : typevar*, `tu*` : typeuse*}((dt : deftype <: typeuse), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = ($subst_deftype(dt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) : deftype <: typeuse)

;; 2-syntax-aux.watsup:110.1-110.112
def $subst_heaptype(heaptype : heaptype, typevar*, typeuse*) : heaptype
  ;; 2-syntax-aux.watsup:144.1-144.67
  def $subst_heaptype{tv' : typevar, `tv*` : typevar*, `tu*` : typeuse*}((tv' : typevar <: heaptype), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = ($subst_typevar(tv', tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) : typeuse <: heaptype)
  ;; 2-syntax-aux.watsup:145.1-145.65
  def $subst_heaptype{dt : deftype, `tv*` : typevar*, `tu*` : typeuse*}((dt : deftype <: heaptype), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = ($subst_deftype(dt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) : deftype <: heaptype)
  ;; 2-syntax-aux.watsup:146.1-146.53
  def $subst_heaptype{ht : heaptype, `tv*` : typevar*, `tu*` : typeuse*}(ht, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = ht
    -- otherwise

;; 2-syntax-aux.watsup:111.1-111.112
def $subst_reftype(reftype : reftype, typevar*, typeuse*) : reftype
  ;; 2-syntax-aux.watsup:148.1-148.83
  def $subst_reftype{nul : nul, ht : heaptype, `tv*` : typevar*, `tu*` : typeuse*}(REF_reftype(nul, ht), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = REF_reftype(nul, $subst_heaptype(ht, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}))

;; 2-syntax-aux.watsup:112.1-112.112
def $subst_valtype(valtype : valtype, typevar*, typeuse*) : valtype
  ;; 2-syntax-aux.watsup:150.1-150.64
  def $subst_valtype{nt : numtype, `tv*` : typevar*, `tu*` : typeuse*}((nt : numtype <: valtype), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = ($subst_numtype(nt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) : numtype <: valtype)
  ;; 2-syntax-aux.watsup:151.1-151.64
  def $subst_valtype{vt : vectype, `tv*` : typevar*, `tu*` : typeuse*}((vt : vectype <: valtype), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = ($subst_vectype(vt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) : vectype <: valtype)
  ;; 2-syntax-aux.watsup:152.1-152.64
  def $subst_valtype{rt : reftype, `tv*` : typevar*, `tu*` : typeuse*}((rt : reftype <: valtype), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = ($subst_reftype(rt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) : reftype <: valtype)
  ;; 2-syntax-aux.watsup:153.1-153.40
  def $subst_valtype{`tv*` : typevar*, `tu*` : typeuse*}(BOT_valtype, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = BOT_valtype

;; 2-syntax-aux.watsup:115.1-115.112
def $subst_storagetype(storagetype : storagetype, typevar*, typeuse*) : storagetype
  ;; 2-syntax-aux.watsup:157.1-157.66
  def $subst_storagetype{t : valtype, `tv*` : typevar*, `tu*` : typeuse*}((t : valtype <: storagetype), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = ($subst_valtype(t, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) : valtype <: storagetype)
  ;; 2-syntax-aux.watsup:158.1-158.69
  def $subst_storagetype{pt : packtype, `tv*` : typevar*, `tu*` : typeuse*}((pt : packtype <: storagetype), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = ($subst_packtype(pt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) : packtype <: storagetype)

;; 2-syntax-aux.watsup:116.1-116.112
def $subst_fieldtype(fieldtype : fieldtype, typevar*, typeuse*) : fieldtype
  ;; 2-syntax-aux.watsup:160.1-160.80
  def $subst_fieldtype{mut : mut, zt : storagetype, `tv*` : typevar*, `tu*` : typeuse*}(`%%`_fieldtype(mut, zt), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = `%%`_fieldtype(mut, $subst_storagetype(zt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}))

;; 2-syntax-aux.watsup:118.1-118.112
def $subst_comptype(comptype : comptype, typevar*, typeuse*) : comptype
  ;; 2-syntax-aux.watsup:162.1-162.85
  def $subst_comptype{`yt*` : fieldtype*, `tv*` : typevar*, `tu*` : typeuse*}(STRUCT_comptype(`%`_structtype(yt*{yt <- `yt*`})), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = STRUCT_comptype(`%`_structtype($subst_fieldtype(yt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`})*{yt <- `yt*`}))
  ;; 2-syntax-aux.watsup:163.1-163.81
  def $subst_comptype{yt : fieldtype, `tv*` : typevar*, `tu*` : typeuse*}(ARRAY_comptype(yt), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = ARRAY_comptype($subst_fieldtype(yt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}))
  ;; 2-syntax-aux.watsup:164.1-164.78
  def $subst_comptype{ft : functype, `tv*` : typevar*, `tu*` : typeuse*}(FUNC_comptype(ft), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = FUNC_comptype($subst_functype(ft, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}))

;; 2-syntax-aux.watsup:119.1-119.112
def $subst_subtype(subtype : subtype, typevar*, typeuse*) : subtype
  ;; 2-syntax-aux.watsup:166.1-167.71
  def $subst_subtype{fin : fin, `tu'*` : typeuse*, ct : comptype, `tv*` : typevar*, `tu*` : typeuse*}(SUB_subtype(fin, tu'*{tu' <- `tu'*`}, ct), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = SUB_subtype(fin, $subst_typeuse(tu', tv*{tv <- `tv*`}, tu*{tu <- `tu*`})*{tu' <- `tu'*`}, $subst_comptype(ct, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}))

;; 2-syntax-aux.watsup:120.1-120.112
def $subst_rectype(rectype : rectype, typevar*, typeuse*) : rectype
  ;; 2-syntax-aux.watsup:169.1-169.76
  def $subst_rectype{`st*` : subtype*, `tv*` : typevar*, `tu*` : typeuse*}(REC_rectype(`%`_list(st*{st <- `st*`})), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = REC_rectype(`%`_list($subst_subtype(st, tv*{tv <- `tv*`}, tu*{tu <- `tu*`})*{st <- `st*`}))

;; 2-syntax-aux.watsup:121.1-121.112
def $subst_deftype(deftype : deftype, typevar*, typeuse*) : deftype
  ;; 2-syntax-aux.watsup:171.1-171.78
  def $subst_deftype{qt : rectype, i : n, `tv*` : typevar*, `tu*` : typeuse*}(DEF_deftype(qt, i), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = DEF_deftype($subst_rectype(qt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}), i)

;; 2-syntax-aux.watsup:124.1-124.112
def $subst_functype(functype : functype, typevar*, typeuse*) : functype
  ;; 2-syntax-aux.watsup:174.1-174.113
  def $subst_functype{`t_1*` : valtype*, `t_2*` : valtype*, `tv*` : typevar*, `tu*` : typeuse*}(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`})), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = `%->%`_functype(`%`_resulttype($subst_valtype(t_1, tv*{tv <- `tv*`}, tu*{tu <- `tu*`})*{t_1 <- `t_1*`}), `%`_resulttype($subst_valtype(t_2, tv*{tv <- `tv*`}, tu*{tu <- `tu*`})*{t_2 <- `t_2*`}))
}

;; 2-syntax-aux.watsup
def $subst_addrtype(addrtype : addrtype, typevar*, typeuse*) : addrtype
  ;; 2-syntax-aux.watsup
  def $subst_addrtype{at : addrtype, `tv*` : typevar*, `tu*` : typeuse*}(at, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = at

;; 2-syntax-aux.watsup
def $subst_globaltype(globaltype : globaltype, typevar*, typeuse*) : globaltype
  ;; 2-syntax-aux.watsup
  def $subst_globaltype{mut : mut, t : valtype, `tv*` : typevar*, `tu*` : typeuse*}(`%%`_globaltype(mut, t), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = `%%`_globaltype(mut, $subst_valtype(t, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}))

;; 2-syntax-aux.watsup
def $subst_tabletype(tabletype : tabletype, typevar*, typeuse*) : tabletype
  ;; 2-syntax-aux.watsup
  def $subst_tabletype{at : addrtype, lim : limits, rt : reftype, `tv*` : typevar*, `tu*` : typeuse*}(`%%%`_tabletype(at, lim, rt), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = `%%%`_tabletype(at, lim, $subst_reftype(rt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}))

;; 2-syntax-aux.watsup
def $subst_memtype(memtype : memtype, typevar*, typeuse*) : memtype
  ;; 2-syntax-aux.watsup
  def $subst_memtype{at : addrtype, lim : limits, `tv*` : typevar*, `tu*` : typeuse*}(`%%PAGE`_memtype(at, lim), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = `%%PAGE`_memtype(at, lim)

;; 2-syntax-aux.watsup
def $subst_tagtype(tagtype : tagtype, typevar*, typeuse*) : tagtype
  ;; 2-syntax-aux.watsup
  def $subst_tagtype{dt : deftype, `tv*` : typevar*, `tu*` : typeuse*}(dt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = $subst_deftype(dt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`})

;; 2-syntax-aux.watsup
def $subst_externtype(externtype : externtype, typevar*, typeuse*) : externtype
  ;; 2-syntax-aux.watsup
  def $subst_externtype{dt : deftype, `tv*` : typevar*, `tu*` : typeuse*}(FUNC_externtype((dt : deftype <: typeuse)), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = FUNC_externtype(($subst_deftype(dt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) : deftype <: typeuse))
  ;; 2-syntax-aux.watsup
  def $subst_externtype{gt : globaltype, `tv*` : typevar*, `tu*` : typeuse*}(GLOBAL_externtype(gt), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = GLOBAL_externtype($subst_globaltype(gt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}))
  ;; 2-syntax-aux.watsup
  def $subst_externtype{tt : tabletype, `tv*` : typevar*, `tu*` : typeuse*}(TABLE_externtype(tt), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = TABLE_externtype($subst_tabletype(tt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}))
  ;; 2-syntax-aux.watsup
  def $subst_externtype{mt : memtype, `tv*` : typevar*, `tu*` : typeuse*}(MEM_externtype(mt), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = MEM_externtype($subst_memtype(mt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}))
  ;; 2-syntax-aux.watsup
  def $subst_externtype{jt : tagtype, `tv*` : typevar*, `tu*` : typeuse*}(TAG_externtype((jt : deftype <: typeuse)), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = TAG_externtype(($subst_tagtype(jt, tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) : deftype <: typeuse))

;; 2-syntax-aux.watsup
def $subst_moduletype(moduletype : moduletype, typevar*, typeuse*) : moduletype
  ;; 2-syntax-aux.watsup
  def $subst_moduletype{`xt_1*` : externtype*, `xt_2*` : externtype*, `tv*` : typevar*, `tu*` : typeuse*}(`%->%`_moduletype(xt_1*{xt_1 <- `xt_1*`}, xt_2*{xt_2 <- `xt_2*`}), tv*{tv <- `tv*`}, tu*{tu <- `tu*`}) = `%->%`_moduletype($subst_externtype(xt_1, tv*{tv <- `tv*`}, tu*{tu <- `tu*`})*{xt_1 <- `xt_1*`}, $subst_externtype(xt_2, tv*{tv <- `tv*`}, tu*{tu <- `tu*`})*{xt_2 <- `xt_2*`})

;; 2-syntax-aux.watsup
def $subst_all_valtype(valtype : valtype, heaptype*) : valtype
  ;; 2-syntax-aux.watsup
  def $subst_all_valtype{t : valtype, `tu*` : typeuse*, n : n, `i*` : nat*}(t, (tu : typeuse <: heaptype)^n{tu <- `tu*`}) = $subst_valtype(t, _IDX_typevar(`%`_typeidx(i))^(i<n){i <- `i*`}, tu^n{tu <- `tu*`})

;; 2-syntax-aux.watsup
def $subst_all_reftype(reftype : reftype, heaptype*) : reftype
  ;; 2-syntax-aux.watsup
  def $subst_all_reftype{rt : reftype, `tu*` : typeuse*, n : n, `i*` : nat*}(rt, (tu : typeuse <: heaptype)^n{tu <- `tu*`}) = $subst_reftype(rt, _IDX_typevar(`%`_typeidx(i))^(i<n){i <- `i*`}, tu^n{tu <- `tu*`})

;; 2-syntax-aux.watsup
def $subst_all_deftype(deftype : deftype, heaptype*) : deftype
  ;; 2-syntax-aux.watsup
  def $subst_all_deftype{dt : deftype, `tu*` : typeuse*, n : n, `i*` : nat*}(dt, (tu : typeuse <: heaptype)^n{tu <- `tu*`}) = $subst_deftype(dt, _IDX_typevar(`%`_typeidx(i))^(i<n){i <- `i*`}, tu^n{tu <- `tu*`})

;; 2-syntax-aux.watsup
def $subst_all_globaltype(globaltype : globaltype, heaptype*) : globaltype
  ;; 2-syntax-aux.watsup
  def $subst_all_globaltype{gt : globaltype, `tu*` : typeuse*, n : n, `i*` : nat*}(gt, (tu : typeuse <: heaptype)^n{tu <- `tu*`}) = $subst_globaltype(gt, _IDX_typevar(`%`_typeidx(i))^(i<n){i <- `i*`}, tu^n{tu <- `tu*`})

;; 2-syntax-aux.watsup
def $subst_all_tabletype(tabletype : tabletype, heaptype*) : tabletype
  ;; 2-syntax-aux.watsup
  def $subst_all_tabletype{tt : tabletype, `tu*` : typeuse*, n : n, `i*` : nat*}(tt, (tu : typeuse <: heaptype)^n{tu <- `tu*`}) = $subst_tabletype(tt, _IDX_typevar(`%`_typeidx(i))^(i<n){i <- `i*`}, tu^n{tu <- `tu*`})

;; 2-syntax-aux.watsup
def $subst_all_memtype(memtype : memtype, heaptype*) : memtype
  ;; 2-syntax-aux.watsup
  def $subst_all_memtype{mt : memtype, `tu*` : typeuse*, n : n, `i*` : nat*}(mt, (tu : typeuse <: heaptype)^n{tu <- `tu*`}) = $subst_memtype(mt, _IDX_typevar(`%`_typeidx(i))^(i<n){i <- `i*`}, tu^n{tu <- `tu*`})

;; 2-syntax-aux.watsup
def $subst_all_moduletype(moduletype : moduletype, heaptype*) : moduletype
  ;; 2-syntax-aux.watsup
  def $subst_all_moduletype{mmt : moduletype, `tu*` : typeuse*, n : n, `i*` : nat*}(mmt, (tu : typeuse <: heaptype)^n{tu <- `tu*`}) = $subst_moduletype(mmt, _IDX_typevar(`%`_typeidx(i))^(i<n){i <- `i*`}, tu^n{tu <- `tu*`})

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:206.1-206.98
def $subst_all_deftypes(deftype*, heaptype*) : deftype*
  ;; 2-syntax-aux.watsup:207.1-207.40
  def $subst_all_deftypes{`tu*` : typeuse*}([], (tu : typeuse <: heaptype)*{tu <- `tu*`}) = []
  ;; 2-syntax-aux.watsup:208.1-208.101
  def $subst_all_deftypes{dt_1 : deftype, `dt*` : deftype*, `tu*` : typeuse*}([dt_1] ++ dt*{dt <- `dt*`}, (tu : typeuse <: heaptype)*{tu <- `tu*`}) = [$subst_all_deftype(dt_1, (tu : typeuse <: heaptype)*{tu <- `tu*`})] ++ $subst_all_deftypes(dt*{dt <- `dt*`}, (tu : typeuse <: heaptype)*{tu <- `tu*`})
}

;; 2-syntax-aux.watsup
def $rollrt(typeidx : typeidx, rectype : rectype) : rectype
  ;; 2-syntax-aux.watsup
  def $rollrt{x : idx, rectype : rectype, `subtype*` : subtype*, `i*` : nat*, n : n}(x, rectype) = REC_rectype(`%`_list($subst_subtype(subtype, _IDX_typevar(`%`_typeidx((x!`%`_idx.0 + i)))^(i<n){i <- `i*`}, REC_typeuse(i)^(i<n){i <- `i*`})^n{subtype <- `subtype*`}))
    -- if (rectype = REC_rectype(`%`_list(subtype^n{subtype <- `subtype*`})))

;; 2-syntax-aux.watsup
def $unrollrt(rectype : rectype) : rectype
  ;; 2-syntax-aux.watsup
  def $unrollrt{rectype : rectype, `subtype*` : subtype*, `i*` : nat*, n : n}(rectype) = REC_rectype(`%`_list($subst_subtype(subtype, REC_typevar(i)^(i<n){i <- `i*`}, DEF_typeuse(rectype, i)^(i<n){i <- `i*`})^n{subtype <- `subtype*`}))
    -- if (rectype = REC_rectype(`%`_list(subtype^n{subtype <- `subtype*`})))

;; 2-syntax-aux.watsup
def $rolldt(typeidx : typeidx, rectype : rectype) : deftype*
  ;; 2-syntax-aux.watsup
  def $rolldt{x : idx, rectype : rectype, `subtype*` : subtype*, n : n, `i*` : nat*}(x, rectype) = DEF_deftype(REC_rectype(`%`_list(subtype^n{subtype <- `subtype*`})), i)^(i<n){i <- `i*`}
    -- if ($rollrt(x, rectype) = REC_rectype(`%`_list(subtype^n{subtype <- `subtype*`})))

;; 2-syntax-aux.watsup
def $unrolldt(deftype : deftype) : subtype
  ;; 2-syntax-aux.watsup
  def $unrolldt{rectype : rectype, i : n, `subtype*` : subtype*}(DEF_deftype(rectype, i)) = subtype*{subtype <- `subtype*`}[i]
    -- if ($unrollrt(rectype) = REC_rectype(`%`_list(subtype*{subtype <- `subtype*`})))

;; 2-syntax-aux.watsup
def $expanddt(deftype : deftype) : comptype
  ;; 2-syntax-aux.watsup
  def $expanddt{deftype : deftype, comptype : comptype, fin : fin, `typeuse*` : typeuse*}(deftype) = comptype
    -- if ($unrolldt(deftype) = SUB_subtype(fin, typeuse*{typeuse <- `typeuse*`}, comptype))

;; 2-syntax-aux.watsup
relation Expand: `%~~%`(deftype, comptype)
  ;; 2-syntax-aux.watsup
  rule _{deftype : deftype, comptype : comptype, fin : fin, `typeuse*` : typeuse*}:
    `%~~%`(deftype, comptype)
    -- if ($unrolldt(deftype) = SUB_subtype(fin, typeuse*{typeuse <- `typeuse*`}, comptype))

;; 2-syntax-aux.watsup
def $memarg0 : memarg
  ;; 2-syntax-aux.watsup
  def $memarg0 = {ALIGN `%`_u32(0), OFFSET `%`_u32(0)}

;; 2-syntax-aux.watsup
def $const(consttype : consttype, lit_ : lit_((consttype : consttype <: storagetype))) : instr
  ;; 2-syntax-aux.watsup
  def $const{numtype : numtype, c : lit_((numtype : numtype <: storagetype))}((numtype : numtype <: consttype), c) = CONST_instr(numtype, c)
  ;; 2-syntax-aux.watsup
  def $const{vectype : vectype, c : lit_((vectype : vectype <: storagetype))}((vectype : vectype <: consttype), c) = VCONST_instr(vectype, c)

;; 2-syntax-aux.watsup
syntax free =
{
  TYPES{`typeidx*` : typeidx*} typeidx*,
  FUNCS{`funcidx*` : funcidx*} funcidx*,
  GLOBALS{`globalidx*` : globalidx*} globalidx*,
  TABLES{`tableidx*` : tableidx*} tableidx*,
  MEMS{`memidx*` : memidx*} memidx*,
  ELEMS{`elemidx*` : elemidx*} elemidx*,
  DATAS{`dataidx*` : dataidx*} dataidx*,
  LOCALS{`localidx*` : localidx*} localidx*,
  LABELS{`labelidx*` : labelidx*} labelidx*
}

;; 2-syntax-aux.watsup
def $free_opt(free?) : free
  ;; 2-syntax-aux.watsup
  def $free_opt(?()) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup
  def $free_opt{free : free}(?(free)) = free

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:271.1-271.29
def $free_list(free*) : free
  ;; 2-syntax-aux.watsup:276.1-276.25
  def $free_list([]) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:277.1-277.57
  def $free_list{free : free, `free'*` : free*}([free] ++ free'*{free' <- `free'*`}) = free +++ $free_list(free'*{free' <- `free'*`})
}

;; 2-syntax-aux.watsup
def $free_typeidx(typeidx : typeidx) : free
  ;; 2-syntax-aux.watsup
  def $free_typeidx{typeidx : typeidx}(typeidx) = {TYPES [typeidx], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_funcidx(funcidx : funcidx) : free
  ;; 2-syntax-aux.watsup
  def $free_funcidx{funcidx : funcidx}(funcidx) = {TYPES [], FUNCS [funcidx], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_globalidx(globalidx : globalidx) : free
  ;; 2-syntax-aux.watsup
  def $free_globalidx{globalidx : globalidx}(globalidx) = {TYPES [], FUNCS [], GLOBALS [globalidx], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_tableidx(tableidx : tableidx) : free
  ;; 2-syntax-aux.watsup
  def $free_tableidx{tableidx : tableidx}(tableidx) = {TYPES [], FUNCS [], GLOBALS [], TABLES [tableidx], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_memidx(memidx : memidx) : free
  ;; 2-syntax-aux.watsup
  def $free_memidx{memidx : memidx}(memidx) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [memidx], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_elemidx(elemidx : elemidx) : free
  ;; 2-syntax-aux.watsup
  def $free_elemidx{elemidx : elemidx}(elemidx) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [elemidx], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_dataidx(dataidx : dataidx) : free
  ;; 2-syntax-aux.watsup
  def $free_dataidx{dataidx : dataidx}(dataidx) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [dataidx], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_localidx(localidx : localidx) : free
  ;; 2-syntax-aux.watsup
  def $free_localidx{localidx : localidx}(localidx) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [localidx], LABELS []}

;; 2-syntax-aux.watsup
def $free_labelidx(labelidx : labelidx) : free
  ;; 2-syntax-aux.watsup
  def $free_labelidx{labelidx : labelidx}(labelidx) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS [labelidx]}

;; 2-syntax-aux.watsup
def $free_externidx(externidx : externidx) : free
  ;; 2-syntax-aux.watsup
  def $free_externidx{funcidx : funcidx}(FUNC_externidx(funcidx)) = $free_funcidx(funcidx)
  ;; 2-syntax-aux.watsup
  def $free_externidx{globalidx : globalidx}(GLOBAL_externidx(globalidx)) = $free_globalidx(globalidx)
  ;; 2-syntax-aux.watsup
  def $free_externidx{tableidx : tableidx}(TABLE_externidx(tableidx)) = $free_tableidx(tableidx)
  ;; 2-syntax-aux.watsup
  def $free_externidx{memidx : memidx}(MEM_externidx(memidx)) = $free_memidx(memidx)

;; 2-syntax-aux.watsup
def $free_addrtype(numtype : numtype) : free
  ;; 2-syntax-aux.watsup
  def $free_addrtype{addrtype : addrtype}((addrtype : addrtype <: numtype)) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_numtype(numtype : numtype) : free
  ;; 2-syntax-aux.watsup
  def $free_numtype{numtype : numtype}(numtype) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_packtype(packtype : packtype) : free
  ;; 2-syntax-aux.watsup
  def $free_packtype{packtype : packtype}(packtype) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_lanetype(lanetype : lanetype) : free
  ;; 2-syntax-aux.watsup
  def $free_lanetype{numtype : numtype}((numtype : numtype <: lanetype)) = $free_numtype(numtype)
  ;; 2-syntax-aux.watsup
  def $free_lanetype{packtype : packtype}((packtype : packtype <: lanetype)) = $free_packtype(packtype)

;; 2-syntax-aux.watsup
def $free_vectype(vectype : vectype) : free
  ;; 2-syntax-aux.watsup
  def $free_vectype{vectype : vectype}(vectype) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_consttype(consttype : consttype) : free
  ;; 2-syntax-aux.watsup
  def $free_consttype{numtype : numtype}((numtype : numtype <: consttype)) = $free_numtype(numtype)
  ;; 2-syntax-aux.watsup
  def $free_consttype{vectype : vectype}((vectype : vectype <: consttype)) = $free_vectype(vectype)

;; 2-syntax-aux.watsup
def $free_absheaptype(absheaptype : absheaptype) : free
  ;; 2-syntax-aux.watsup
  def $free_absheaptype{absheaptype : absheaptype}(absheaptype) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_typevar(typevar : typevar) : free
  ;; 2-syntax-aux.watsup
  def $free_typevar{typeidx : typeidx}(_IDX_typevar(typeidx)) = $free_typeidx(typeidx)
  ;; 2-syntax-aux.watsup
  def $free_typevar{n : n}(REC_typevar(n)) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:318.1-318.36
def $free_heaptype(heaptype : heaptype) : free
  ;; 2-syntax-aux.watsup:369.1-369.65
  def $free_heaptype{absheaptype : absheaptype}((absheaptype : absheaptype <: heaptype)) = $free_absheaptype(absheaptype)
  ;; 2-syntax-aux.watsup:370.1-370.53
  def $free_heaptype{typeuse : typeuse}((typeuse : typeuse <: heaptype)) = $free_typeuse(typeuse)

;; 2-syntax-aux.watsup:319.1-319.34
def $free_reftype(reftype : reftype) : free
  ;; 2-syntax-aux.watsup:372.1-372.63
  def $free_reftype{nul : nul, heaptype : heaptype}(REF_reftype(nul, heaptype)) = $free_heaptype(heaptype)

;; 2-syntax-aux.watsup:321.1-321.34
def $free_typeuse(typeuse : typeuse) : free
  ;; 2-syntax-aux.watsup:366.1-366.52
  def $free_typeuse{typevar : typevar}((typevar : typevar <: typeuse)) = $free_typevar(typevar)
  ;; 2-syntax-aux.watsup:367.1-367.52
  def $free_typeuse{deftype : deftype}((deftype : deftype <: typeuse)) = $free_deftype(deftype)

;; 2-syntax-aux.watsup:322.1-322.34
def $free_valtype(valtype : valtype) : free
  ;; 2-syntax-aux.watsup:374.1-374.52
  def $free_valtype{numtype : numtype}((numtype : numtype <: valtype)) = $free_numtype(numtype)
  ;; 2-syntax-aux.watsup:375.1-375.52
  def $free_valtype{vectype : vectype}((vectype : vectype <: valtype)) = $free_vectype(vectype)
  ;; 2-syntax-aux.watsup:376.1-376.52
  def $free_valtype{reftype : reftype}((reftype : reftype <: valtype)) = $free_reftype(reftype)
  ;; 2-syntax-aux.watsup:377.1-377.28
  def $free_valtype(BOT_valtype) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup:324.1-324.40
def $free_resulttype(resulttype : resulttype) : free
  ;; 2-syntax-aux.watsup:379.1-379.69
  def $free_resulttype{`valtype*` : valtype*}(`%`_resulttype(valtype*{valtype <- `valtype*`})) = $free_list($free_valtype(valtype)*{valtype <- `valtype*`})

;; 2-syntax-aux.watsup:325.1-325.42
def $free_storagetype(storagetype : storagetype) : free
  ;; 2-syntax-aux.watsup:381.1-381.56
  def $free_storagetype{valtype : valtype}((valtype : valtype <: storagetype)) = $free_valtype(valtype)
  ;; 2-syntax-aux.watsup:382.1-382.59
  def $free_storagetype{packtype : packtype}((packtype : packtype <: storagetype)) = $free_packtype(packtype)

;; 2-syntax-aux.watsup:326.1-326.38
def $free_fieldtype(fieldtype : fieldtype) : free
  ;; 2-syntax-aux.watsup:384.1-384.70
  def $free_fieldtype{mut : mut, storagetype : storagetype}(`%%`_fieldtype(mut, storagetype)) = $free_storagetype(storagetype)

;; 2-syntax-aux.watsup:327.1-327.40
def $free_structtype(structtype : structtype) : free
  ;; 2-syntax-aux.watsup:389.1-389.75
  def $free_structtype{`fieldtype*` : fieldtype*}(`%`_structtype(fieldtype*{fieldtype <- `fieldtype*`})) = $free_list($free_fieldtype(fieldtype)*{fieldtype <- `fieldtype*`})

;; 2-syntax-aux.watsup:328.1-328.38
def $free_arraytype(arraytype : arraytype) : free
  ;; 2-syntax-aux.watsup:391.1-391.60
  def $free_arraytype{fieldtype : fieldtype}(fieldtype) = $free_fieldtype(fieldtype)

;; 2-syntax-aux.watsup:329.1-329.36
def $free_functype(functype : functype) : free
  ;; 2-syntax-aux.watsup:386.1-387.67
  def $free_functype{resulttype_1 : resulttype, resulttype_2 : resulttype}(`%->%`_functype(resulttype_1, resulttype_2)) = $free_resulttype(resulttype_1) +++ $free_resulttype(resulttype_2)

;; 2-syntax-aux.watsup:330.1-330.36
def $free_comptype(comptype : comptype) : free
  ;; 2-syntax-aux.watsup:393.1-393.69
  def $free_comptype{structtype : structtype}(STRUCT_comptype(structtype)) = $free_structtype(structtype)
  ;; 2-syntax-aux.watsup:394.1-394.65
  def $free_comptype{arraytype : arraytype}(ARRAY_comptype(arraytype)) = $free_arraytype(arraytype)
  ;; 2-syntax-aux.watsup:395.1-395.61
  def $free_comptype{functype : functype}(FUNC_comptype(functype)) = $free_functype(functype)

;; 2-syntax-aux.watsup:331.1-331.34
def $free_subtype(subtype : subtype) : free
  ;; 2-syntax-aux.watsup:397.1-398.66
  def $free_subtype{fin : fin, `typeuse*` : typeuse*, comptype : comptype}(SUB_subtype(fin, typeuse*{typeuse <- `typeuse*`}, comptype)) = $free_list($free_typeuse(typeuse)*{typeuse <- `typeuse*`}) +++ $free_comptype(comptype)

;; 2-syntax-aux.watsup:332.1-332.34
def $free_rectype(rectype : rectype) : free
  ;; 2-syntax-aux.watsup:400.1-400.70
  def $free_rectype{`subtype*` : subtype*}(REC_rectype(`%`_list(subtype*{subtype <- `subtype*`}))) = $free_list($free_subtype(subtype)*{subtype <- `subtype*`})

;; 2-syntax-aux.watsup:360.1-360.34
def $free_deftype(deftype : deftype) : free
  ;; 2-syntax-aux.watsup:361.1-361.58
  def $free_deftype{rectype : rectype, n : n}(DEF_deftype(rectype, n)) = $free_rectype(rectype)
}

;; 2-syntax-aux.watsup
def $free_globaltype(globaltype : globaltype) : free
  ;; 2-syntax-aux.watsup
  def $free_globaltype{mut : mut, valtype : valtype}(`%%`_globaltype(mut, valtype)) = $free_valtype(valtype)

;; 2-syntax-aux.watsup
def $free_tabletype(tabletype : tabletype) : free
  ;; 2-syntax-aux.watsup
  def $free_tabletype{addrtype : addrtype, limits : limits, reftype : reftype}(`%%%`_tabletype(addrtype, limits, reftype)) = $free_addrtype((addrtype : addrtype <: numtype)) +++ $free_reftype(reftype)

;; 2-syntax-aux.watsup
def $free_memtype(memtype : memtype) : free
  ;; 2-syntax-aux.watsup
  def $free_memtype{addrtype : addrtype, limits : limits}(`%%PAGE`_memtype(addrtype, limits)) = $free_addrtype((addrtype : addrtype <: numtype))

;; 2-syntax-aux.watsup
def $free_tagtype(tagtype : tagtype) : free
  ;; 2-syntax-aux.watsup
  def $free_tagtype{deftype : deftype}(deftype) = $free_deftype(deftype)

;; 2-syntax-aux.watsup
def $free_elemtype(elemtype : elemtype) : free
  ;; 2-syntax-aux.watsup
  def $free_elemtype{reftype : reftype}(reftype) = $free_reftype(reftype)

;; 2-syntax-aux.watsup
def $free_datatype(datatype : datatype) : free
  ;; 2-syntax-aux.watsup
  def $free_datatype(OK_datatype) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_externtype(externtype : externtype) : free
  ;; 2-syntax-aux.watsup
  def $free_externtype{typeuse : typeuse}(FUNC_externtype(typeuse)) = $free_typeuse(typeuse)
  ;; 2-syntax-aux.watsup
  def $free_externtype{globaltype : globaltype}(GLOBAL_externtype(globaltype)) = $free_globaltype(globaltype)
  ;; 2-syntax-aux.watsup
  def $free_externtype{tabletype : tabletype}(TABLE_externtype(tabletype)) = $free_tabletype(tabletype)
  ;; 2-syntax-aux.watsup
  def $free_externtype{memtype : memtype}(MEM_externtype(memtype)) = $free_memtype(memtype)
  ;; 2-syntax-aux.watsup
  def $free_externtype{tagtype : tagtype}(TAG_externtype((tagtype : deftype <: typeuse))) = $free_tagtype(tagtype)

;; 2-syntax-aux.watsup
def $free_moduletype(moduletype : moduletype) : free
  ;; 2-syntax-aux.watsup
  def $free_moduletype{`externtype_1*` : externtype*, `externtype_2*` : externtype*}(`%->%`_moduletype(externtype_1*{externtype_1 <- `externtype_1*`}, externtype_2*{externtype_2 <- `externtype_2*`})) = $free_list($free_externtype(externtype_1)*{externtype_1 <- `externtype_1*`}) +++ $free_list($free_externtype(externtype_2)*{externtype_2 <- `externtype_2*`})

;; 2-syntax-aux.watsup
def $free_shape(shape : shape) : free
  ;; 2-syntax-aux.watsup
  def $free_shape{lanetype : lanetype, dim : dim}(`%X%`_shape(lanetype, dim)) = $free_lanetype(lanetype)

;; 2-syntax-aux.watsup
def $free_blocktype(blocktype : blocktype) : free
  ;; 2-syntax-aux.watsup
  def $free_blocktype{`valtype?` : valtype?}(_RESULT_blocktype(valtype?{valtype <- `valtype?`})) = $free_opt($free_valtype(valtype)?{valtype <- `valtype?`})
  ;; 2-syntax-aux.watsup
  def $free_blocktype{funcidx : funcidx}(_IDX_blocktype(funcidx)) = $free_funcidx(funcidx)

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:584.1-584.44
def $shift_labelidxs(labelidx*) : labelidx*
  ;; 2-syntax-aux.watsup:585.1-585.32
  def $shift_labelidxs([]) = []
  ;; 2-syntax-aux.watsup:586.1-586.66
  def $shift_labelidxs{`labelidx'*` : labelidx*}([`%`_labelidx(0)] ++ labelidx'*{labelidx' <- `labelidx'*`}) = $shift_labelidxs(labelidx'*{labelidx' <- `labelidx'*`})
  ;; 2-syntax-aux.watsup:587.1-587.91
  def $shift_labelidxs{labelidx : labelidx, `labelidx'*` : labelidx*}([labelidx] ++ labelidx'*{labelidx' <- `labelidx'*`}) = [`%`_labelidx((((labelidx!`%`_labelidx.0 : nat <:> int) - (1 : nat <:> int)) : int <:> nat))] ++ $shift_labelidxs(labelidx'*{labelidx' <- `labelidx'*`})
}

;; 2-syntax-aux.watsup
rec {

;; 2-syntax-aux.watsup:431.1-431.30
def $free_instr(instr : instr) : free
  ;; 2-syntax-aux.watsup:442.1-442.26
  def $free_instr(NOP_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:443.1-443.34
  def $free_instr(UNREACHABLE_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:444.1-444.27
  def $free_instr(DROP_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:445.1-445.86
  def $free_instr{`valtype*?` : valtype*?}(SELECT_instr(valtype*{valtype <- `valtype*`}?{`valtype*` <- `valtype*?`})) = $free_opt($free_list($free_valtype(valtype)*{valtype <- `valtype*`})?{`valtype*` <- `valtype*?`})
  ;; 2-syntax-aux.watsup:447.1-447.92
  def $free_instr{blocktype : blocktype, `instr*` : instr*}(BLOCK_instr(blocktype, instr*{instr <- `instr*`})) = $free_blocktype(blocktype) +++ $free_block(instr*{instr <- `instr*`})
  ;; 2-syntax-aux.watsup:448.1-448.91
  def $free_instr{blocktype : blocktype, `instr*` : instr*}(LOOP_instr(blocktype, instr*{instr <- `instr*`})) = $free_blocktype(blocktype) +++ $free_block(instr*{instr <- `instr*`})
  ;; 2-syntax-aux.watsup:449.1-450.79
  def $free_instr{blocktype : blocktype, `instr_1*` : instr*, `instr_2*` : instr*}(`IF%%ELSE%`_instr(blocktype, instr_1*{instr_1 <- `instr_1*`}, instr_2*{instr_2 <- `instr_2*`})) = $free_blocktype(blocktype) +++ $free_block(instr_1*{instr_1 <- `instr_1*`}) +++ $free_block(instr_2*{instr_2 <- `instr_2*`})
  ;; 2-syntax-aux.watsup:452.1-452.56
  def $free_instr{labelidx : labelidx}(BR_instr(labelidx)) = $free_labelidx(labelidx)
  ;; 2-syntax-aux.watsup:453.1-453.59
  def $free_instr{labelidx : labelidx}(BR_IF_instr(labelidx)) = $free_labelidx(labelidx)
  ;; 2-syntax-aux.watsup:454.1-455.68
  def $free_instr{labelidx : labelidx, labelidx' : labelidx}(BR_TABLE_instr(labelidx*{}, labelidx')) = $free_list($free_labelidx(labelidx)*{}) +++ $free_labelidx(labelidx)
  ;; 2-syntax-aux.watsup:456.1-456.64
  def $free_instr{labelidx : labelidx}(BR_ON_NULL_instr(labelidx)) = $free_labelidx(labelidx)
  ;; 2-syntax-aux.watsup:457.1-457.68
  def $free_instr{labelidx : labelidx}(BR_ON_NON_NULL_instr(labelidx)) = $free_labelidx(labelidx)
  ;; 2-syntax-aux.watsup:458.1-459.83
  def $free_instr{labelidx : labelidx, reftype_1 : reftype, reftype_2 : reftype}(BR_ON_CAST_instr(labelidx, reftype_1, reftype_2)) = $free_labelidx(labelidx) +++ $free_reftype(reftype_1) +++ $free_reftype(reftype_2)
  ;; 2-syntax-aux.watsup:460.1-461.83
  def $free_instr{labelidx : labelidx, reftype_1 : reftype, reftype_2 : reftype}(BR_ON_CAST_FAIL_instr(labelidx, reftype_1, reftype_2)) = $free_labelidx(labelidx) +++ $free_reftype(reftype_1) +++ $free_reftype(reftype_2)
  ;; 2-syntax-aux.watsup:463.1-463.55
  def $free_instr{funcidx : funcidx}(CALL_instr(funcidx)) = $free_funcidx(funcidx)
  ;; 2-syntax-aux.watsup:464.1-464.59
  def $free_instr{typeuse : typeuse}(CALL_REF_instr(typeuse)) = $free_typeuse(typeuse)
  ;; 2-syntax-aux.watsup:465.1-466.53
  def $free_instr{tableidx : tableidx, typeuse : typeuse}(CALL_INDIRECT_instr(tableidx, typeuse)) = $free_tableidx(tableidx) +++ $free_typeuse(typeuse)
  ;; 2-syntax-aux.watsup:467.1-467.29
  def $free_instr(RETURN_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:468.1-468.62
  def $free_instr{funcidx : funcidx}(RETURN_CALL_instr(funcidx)) = $free_funcidx(funcidx)
  ;; 2-syntax-aux.watsup:469.1-469.66
  def $free_instr{typeuse : typeuse}(RETURN_CALL_REF_instr(typeuse)) = $free_typeuse(typeuse)
  ;; 2-syntax-aux.watsup:470.1-471.53
  def $free_instr{tableidx : tableidx, typeuse : typeuse}(RETURN_CALL_INDIRECT_instr(tableidx, typeuse)) = $free_tableidx(tableidx) +++ $free_typeuse(typeuse)
  ;; 2-syntax-aux.watsup:473.1-473.63
  def $free_instr{numtype : numtype, numlit : num_(numtype)}(CONST_instr(numtype, numlit)) = $free_numtype(numtype)
  ;; 2-syntax-aux.watsup:474.1-474.60
  def $free_instr{numtype : numtype, unop : unop_(numtype)}(UNOP_instr(numtype, unop)) = $free_numtype(numtype)
  ;; 2-syntax-aux.watsup:475.1-475.62
  def $free_instr{numtype : numtype, binop : binop_(numtype)}(BINOP_instr(numtype, binop)) = $free_numtype(numtype)
  ;; 2-syntax-aux.watsup:476.1-476.64
  def $free_instr{numtype : numtype, testop : testop_(numtype)}(TESTOP_instr(numtype, testop)) = $free_numtype(numtype)
  ;; 2-syntax-aux.watsup:477.1-477.62
  def $free_instr{numtype : numtype, relop : relop_(numtype)}(RELOP_instr(numtype, relop)) = $free_numtype(numtype)
  ;; 2-syntax-aux.watsup:478.1-479.55
  def $free_instr{numtype_1 : numtype, numtype_2 : numtype, cvtop : cvtop__(numtype_2, numtype_1)}(CVTOP_instr(numtype_1, numtype_2, cvtop)) = $free_numtype(numtype_1) +++ $free_numtype(numtype_2)
  ;; 2-syntax-aux.watsup:481.1-481.64
  def $free_instr{vectype : vectype, veclit : vec_(vectype)}(VCONST_instr(vectype, veclit)) = $free_vectype(vectype)
  ;; 2-syntax-aux.watsup:482.1-482.64
  def $free_instr{vectype : vectype, vvunop : vvunop}(VVUNOP_instr(vectype, vvunop)) = $free_vectype(vectype)
  ;; 2-syntax-aux.watsup:483.1-483.66
  def $free_instr{vectype : vectype, vvbinop : vvbinop}(VVBINOP_instr(vectype, vvbinop)) = $free_vectype(vectype)
  ;; 2-syntax-aux.watsup:484.1-484.68
  def $free_instr{vectype : vectype, vvternop : vvternop}(VVTERNOP_instr(vectype, vvternop)) = $free_vectype(vectype)
  ;; 2-syntax-aux.watsup:485.1-485.68
  def $free_instr{vectype : vectype, vvtestop : vvtestop}(VVTESTOP_instr(vectype, vvtestop)) = $free_vectype(vectype)
  ;; 2-syntax-aux.watsup:486.1-486.56
  def $free_instr{shape : shape, vunop : vunop_(shape)}(VUNOP_instr(shape, vunop)) = $free_shape(shape)
  ;; 2-syntax-aux.watsup:487.1-487.58
  def $free_instr{shape : shape, vbinop : vbinop_(shape)}(VBINOP_instr(shape, vbinop)) = $free_shape(shape)
  ;; 2-syntax-aux.watsup:488.1-488.60
  def $free_instr{shape : shape, vternop : vternop_(shape)}(VTERNOP_instr(shape, vternop)) = $free_shape(shape)
  ;; 2-syntax-aux.watsup:489.1-489.60
  def $free_instr{shape : shape, vtestop : vtestop_(shape)}(VTESTOP_instr(shape, vtestop)) = $free_shape(shape)
  ;; 2-syntax-aux.watsup:490.1-490.58
  def $free_instr{shape : shape, vrelop : vrelop_(shape)}(VRELOP_instr(shape, vrelop)) = $free_shape(shape)
  ;; 2-syntax-aux.watsup:491.1-491.64
  def $free_instr{ishape : ishape, vshiftop : vshiftop_(ishape)}(VSHIFTOP_instr(ishape, vshiftop)) = $free_shape(ishape!`%`_ishape.0)
  ;; 2-syntax-aux.watsup:492.1-492.55
  def $free_instr{ishape : ishape}(VBITMASK_instr(ishape)) = $free_shape(ishape!`%`_ishape.0)
  ;; 2-syntax-aux.watsup:493.1-493.66
  def $free_instr{bshape : bshape, vswizzlop : vswizzlop_(bshape)}(VSWIZZLOP_instr(bshape, vswizzlop)) = $free_shape(bshape!`%`_bshape.0)
  ;; 2-syntax-aux.watsup:494.1-494.64
  def $free_instr{bshape : bshape, `laneidx*` : laneidx*}(VSHUFFLE_instr(bshape, laneidx*{laneidx <- `laneidx*`})) = $free_shape(bshape!`%`_bshape.0)
  ;; 2-syntax-aux.watsup:495.1-496.49
  def $free_instr{ishape_1 : ishape, ishape_2 : ishape, vextunop : vextunop__(ishape_2, ishape_1)}(VEXTUNOP_instr(ishape_1, ishape_2, vextunop)) = $free_shape(ishape_1!`%`_ishape.0) +++ $free_shape(ishape_2!`%`_ishape.0)
  ;; 2-syntax-aux.watsup:497.1-498.49
  def $free_instr{ishape_1 : ishape, ishape_2 : ishape, vextbinop : vextbinop__(ishape_2, ishape_1)}(VEXTBINOP_instr(ishape_1, ishape_2, vextbinop)) = $free_shape(ishape_1!`%`_ishape.0) +++ $free_shape(ishape_2!`%`_ishape.0)
  ;; 2-syntax-aux.watsup:499.1-500.49
  def $free_instr{ishape_1 : ishape, ishape_2 : ishape, sx : sx}(VNARROW_instr(ishape_1, ishape_2, sx)) = $free_shape(ishape_1!`%`_ishape.0) +++ $free_shape(ishape_2!`%`_ishape.0)
  ;; 2-syntax-aux.watsup:501.1-502.47
  def $free_instr{shape_1 : shape, shape_2 : shape, vcvtop : vcvtop__(shape_2, shape_1), `half?` : half__(shape_2, shape_1)?, `zero?` : zero__(shape_2, shape_1)?}(VCVTOP_instr(shape_1, shape_2, vcvtop, half?{half <- `half?`}, zero?{zero <- `zero?`})) = $free_shape(shape_1) +++ $free_shape(shape_2)
  ;; 2-syntax-aux.watsup:503.1-503.51
  def $free_instr{shape : shape}(VSPLAT_instr(shape)) = $free_shape(shape)
  ;; 2-syntax-aux.watsup:504.1-504.70
  def $free_instr{shape : shape, `sx?` : sx?, laneidx : laneidx}(VEXTRACT_LANE_instr(shape, sx?{sx <- `sx?`}, laneidx)) = $free_shape(shape)
  ;; 2-syntax-aux.watsup:505.1-505.66
  def $free_instr{shape : shape, laneidx : laneidx}(VREPLACE_LANE_instr(shape, laneidx)) = $free_shape(shape)
  ;; 2-syntax-aux.watsup:507.1-507.62
  def $free_instr{heaptype : heaptype}(REF.NULL_instr(heaptype)) = $free_heaptype(heaptype)
  ;; 2-syntax-aux.watsup:508.1-508.34
  def $free_instr(REF.IS_NULL_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:509.1-509.38
  def $free_instr(REF.AS_NON_NULL_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:510.1-510.29
  def $free_instr(REF.EQ_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:511.1-511.59
  def $free_instr{reftype : reftype}(REF.TEST_instr(reftype)) = $free_reftype(reftype)
  ;; 2-syntax-aux.watsup:512.1-512.59
  def $free_instr{reftype : reftype}(REF.CAST_instr(reftype)) = $free_reftype(reftype)
  ;; 2-syntax-aux.watsup:513.1-513.59
  def $free_instr{funcidx : funcidx}(REF.FUNC_instr(funcidx)) = $free_funcidx(funcidx)
  ;; 2-syntax-aux.watsup:514.1-514.30
  def $free_instr(REF.I31_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:516.1-516.33
  def $free_instr{sx : sx}(I31.GET_instr(sx)) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:518.1-518.41
  def $free_instr{typeidx : typeidx}(STRUCT.NEW_instr(typeidx)) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:519.1-519.69
  def $free_instr{typeidx : typeidx}(STRUCT.NEW_DEFAULT_instr(typeidx)) = $free_typeidx(typeidx)
  ;; 2-syntax-aux.watsup:520.1-520.69
  def $free_instr{`sx?` : sx?, typeidx : typeidx, u32 : u32}(STRUCT.GET_instr(sx?{sx <- `sx?`}, typeidx, u32)) = $free_typeidx(typeidx)
  ;; 2-syntax-aux.watsup:521.1-521.65
  def $free_instr{typeidx : typeidx, u32 : u32}(STRUCT.SET_instr(typeidx, u32)) = $free_typeidx(typeidx)
  ;; 2-syntax-aux.watsup:523.1-523.60
  def $free_instr{typeidx : typeidx}(ARRAY.NEW_instr(typeidx)) = $free_typeidx(typeidx)
  ;; 2-syntax-aux.watsup:524.1-524.68
  def $free_instr{typeidx : typeidx}(ARRAY.NEW_DEFAULT_instr(typeidx)) = $free_typeidx(typeidx)
  ;; 2-syntax-aux.watsup:525.1-525.70
  def $free_instr{typeidx : typeidx, u32 : u32}(ARRAY.NEW_FIXED_instr(typeidx, u32)) = $free_typeidx(typeidx)
  ;; 2-syntax-aux.watsup:526.1-527.51
  def $free_instr{typeidx : typeidx, dataidx : dataidx}(ARRAY.NEW_DATA_instr(typeidx, dataidx)) = $free_typeidx(typeidx) +++ $free_dataidx(dataidx)
  ;; 2-syntax-aux.watsup:528.1-529.51
  def $free_instr{typeidx : typeidx, elemidx : elemidx}(ARRAY.NEW_ELEM_instr(typeidx, elemidx)) = $free_typeidx(typeidx) +++ $free_elemidx(elemidx)
  ;; 2-syntax-aux.watsup:530.1-530.64
  def $free_instr{`sx?` : sx?, typeidx : typeidx}(ARRAY.GET_instr(sx?{sx <- `sx?`}, typeidx)) = $free_typeidx(typeidx)
  ;; 2-syntax-aux.watsup:531.1-531.60
  def $free_instr{typeidx : typeidx}(ARRAY.SET_instr(typeidx)) = $free_typeidx(typeidx)
  ;; 2-syntax-aux.watsup:532.1-532.32
  def $free_instr(ARRAY.LEN_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:533.1-533.61
  def $free_instr{typeidx : typeidx}(ARRAY.FILL_instr(typeidx)) = $free_typeidx(typeidx)
  ;; 2-syntax-aux.watsup:534.1-535.55
  def $free_instr{typeidx_1 : typeidx, typeidx_2 : typeidx}(ARRAY.COPY_instr(typeidx_1, typeidx_2)) = $free_typeidx(typeidx_1) +++ $free_typeidx(typeidx_2)
  ;; 2-syntax-aux.watsup:536.1-537.51
  def $free_instr{typeidx : typeidx, dataidx : dataidx}(ARRAY.INIT_DATA_instr(typeidx, dataidx)) = $free_typeidx(typeidx) +++ $free_dataidx(dataidx)
  ;; 2-syntax-aux.watsup:538.1-539.51
  def $free_instr{typeidx : typeidx, elemidx : elemidx}(ARRAY.INIT_ELEM_instr(typeidx, elemidx)) = $free_typeidx(typeidx) +++ $free_elemidx(elemidx)
  ;; 2-syntax-aux.watsup:541.1-541.41
  def $free_instr(EXTERN.CONVERT_ANY_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:542.1-542.41
  def $free_instr(ANY.CONVERT_EXTERN_instr) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup:544.1-544.63
  def $free_instr{localidx : localidx}(LOCAL.GET_instr(localidx)) = $free_localidx(localidx)
  ;; 2-syntax-aux.watsup:545.1-545.63
  def $free_instr{localidx : localidx}(LOCAL.SET_instr(localidx)) = $free_localidx(localidx)
  ;; 2-syntax-aux.watsup:546.1-546.63
  def $free_instr{localidx : localidx}(LOCAL.TEE_instr(localidx)) = $free_localidx(localidx)
  ;; 2-syntax-aux.watsup:548.1-548.67
  def $free_instr{globalidx : globalidx}(GLOBAL.GET_instr(globalidx)) = $free_globalidx(globalidx)
  ;; 2-syntax-aux.watsup:549.1-549.67
  def $free_instr{globalidx : globalidx}(GLOBAL.SET_instr(globalidx)) = $free_globalidx(globalidx)
  ;; 2-syntax-aux.watsup:551.1-551.63
  def $free_instr{tableidx : tableidx}(TABLE.GET_instr(tableidx)) = $free_tableidx(tableidx)
  ;; 2-syntax-aux.watsup:552.1-552.63
  def $free_instr{tableidx : tableidx}(TABLE.SET_instr(tableidx)) = $free_tableidx(tableidx)
  ;; 2-syntax-aux.watsup:553.1-553.64
  def $free_instr{tableidx : tableidx}(TABLE.SIZE_instr(tableidx)) = $free_tableidx(tableidx)
  ;; 2-syntax-aux.watsup:554.1-554.64
  def $free_instr{tableidx : tableidx}(TABLE.GROW_instr(tableidx)) = $free_tableidx(tableidx)
  ;; 2-syntax-aux.watsup:555.1-555.64
  def $free_instr{tableidx : tableidx}(TABLE.FILL_instr(tableidx)) = $free_tableidx(tableidx)
  ;; 2-syntax-aux.watsup:556.1-557.59
  def $free_instr{tableidx_1 : tableidx, tableidx_2 : tableidx}(TABLE.COPY_instr(tableidx_1, tableidx_2)) = $free_tableidx(tableidx_1) +++ $free_tableidx(tableidx_2)
  ;; 2-syntax-aux.watsup:558.1-559.53
  def $free_instr{tableidx : tableidx, elemidx : elemidx}(TABLE.INIT_instr(tableidx, elemidx)) = $free_tableidx(tableidx) +++ $free_elemidx(elemidx)
  ;; 2-syntax-aux.watsup:560.1-560.60
  def $free_instr{elemidx : elemidx}(ELEM.DROP_instr(elemidx)) = $free_elemidx(elemidx)
  ;; 2-syntax-aux.watsup:562.1-563.49
  def $free_instr{numtype : numtype, `loadop?` : loadop_(numtype)?, memidx : memidx, memarg : memarg}(LOAD_instr(numtype, loadop?{loadop <- `loadop?`}, memidx, memarg)) = $free_numtype(numtype) +++ $free_memidx(memidx)
  ;; 2-syntax-aux.watsup:564.1-565.49
  def $free_instr{numtype : numtype, `storeop?` : storeop_(numtype)?, memidx : memidx, memarg : memarg}(STORE_instr(numtype, storeop?{storeop <- `storeop?`}, memidx, memarg)) = $free_numtype(numtype) +++ $free_memidx(memidx)
  ;; 2-syntax-aux.watsup:566.1-567.49
  def $free_instr{vectype : vectype, `vloadop?` : vloadop_(vectype)?, memidx : memidx, memarg : memarg}(VLOAD_instr(vectype, vloadop?{vloadop <- `vloadop?`}, memidx, memarg)) = $free_vectype(vectype) +++ $free_memidx(memidx)
  ;; 2-syntax-aux.watsup:568.1-569.49
  def $free_instr{vectype : vectype, sz : sz, memidx : memidx, memarg : memarg, laneidx : laneidx}(VLOAD_LANE_instr(vectype, sz, memidx, memarg, laneidx)) = $free_vectype(vectype) +++ $free_memidx(memidx)
  ;; 2-syntax-aux.watsup:570.1-571.49
  def $free_instr{vectype : vectype, memidx : memidx, memarg : memarg}(VSTORE_instr(vectype, memidx, memarg)) = $free_vectype(vectype) +++ $free_memidx(memidx)
  ;; 2-syntax-aux.watsup:572.1-573.49
  def $free_instr{vectype : vectype, sz : sz, memidx : memidx, memarg : memarg, laneidx : laneidx}(VSTORE_LANE_instr(vectype, sz, memidx, memarg, laneidx)) = $free_vectype(vectype) +++ $free_memidx(memidx)
  ;; 2-syntax-aux.watsup:574.1-574.59
  def $free_instr{memidx : memidx}(MEMORY.SIZE_instr(memidx)) = $free_memidx(memidx)
  ;; 2-syntax-aux.watsup:575.1-575.59
  def $free_instr{memidx : memidx}(MEMORY.GROW_instr(memidx)) = $free_memidx(memidx)
  ;; 2-syntax-aux.watsup:576.1-576.59
  def $free_instr{memidx : memidx}(MEMORY.FILL_instr(memidx)) = $free_memidx(memidx)
  ;; 2-syntax-aux.watsup:577.1-578.51
  def $free_instr{memidx_1 : memidx, memidx_2 : memidx}(MEMORY.COPY_instr(memidx_1, memidx_2)) = $free_memidx(memidx_1) +++ $free_memidx(memidx_2)
  ;; 2-syntax-aux.watsup:579.1-580.49
  def $free_instr{memidx : memidx, dataidx : dataidx}(MEMORY.INIT_instr(memidx, dataidx)) = $free_memidx(memidx) +++ $free_dataidx(dataidx)
  ;; 2-syntax-aux.watsup:581.1-581.60
  def $free_instr{dataidx : dataidx}(DATA.DROP_instr(dataidx)) = $free_dataidx(dataidx)

;; 2-syntax-aux.watsup:432.1-432.31
def $free_block(instr*) : free
  ;; 2-syntax-aux.watsup:589.1-590.47
  def $free_block{`instr*` : instr*, free : free}(instr*{instr <- `instr*`}) = free[LABELS_free = $shift_labelidxs(free.LABELS_free)]
    -- if (free = $free_list($free_instr(instr)*{instr <- `instr*`}))
}

;; 2-syntax-aux.watsup
def $free_expr(expr : expr) : free
  ;; 2-syntax-aux.watsup
  def $free_expr{`instr*` : instr*}(instr*{instr <- `instr*`}) = $free_list($free_instr(instr)*{instr <- `instr*`})

;; 2-syntax-aux.watsup
def $free_type(type : type) : free
  ;; 2-syntax-aux.watsup
  def $free_type{rectype : rectype}(TYPE_type(rectype)) = $free_rectype(rectype)

;; 2-syntax-aux.watsup
def $free_local(local : local) : free
  ;; 2-syntax-aux.watsup
  def $free_local{t : valtype}(LOCAL_local(t)) = $free_valtype(t)

;; 2-syntax-aux.watsup
def $free_func(func : func) : free
  ;; 2-syntax-aux.watsup
  def $free_func{typeidx : typeidx, `local*` : local*, expr : expr}(FUNC_func(typeidx, local*{local <- `local*`}, expr)) = $free_typeidx(typeidx) +++ $free_list($free_local(local)*{local <- `local*`}) +++ $free_block(expr)[LOCALS_free = []]

;; 2-syntax-aux.watsup
def $free_global(global : global) : free
  ;; 2-syntax-aux.watsup
  def $free_global{globaltype : globaltype, expr : expr}(GLOBAL_global(globaltype, expr)) = $free_globaltype(globaltype) +++ $free_expr(expr)

;; 2-syntax-aux.watsup
def $free_table(table : table) : free
  ;; 2-syntax-aux.watsup
  def $free_table{tabletype : tabletype, expr : expr}(TABLE_table(tabletype, expr)) = $free_tabletype(tabletype) +++ $free_expr(expr)

;; 2-syntax-aux.watsup
def $free_mem(mem : mem) : free
  ;; 2-syntax-aux.watsup
  def $free_mem{memtype : memtype}(MEMORY_mem(memtype)) = $free_memtype(memtype)

;; 2-syntax-aux.watsup
def $free_tag(tag : tag) : free
  ;; 2-syntax-aux.watsup
  def $free_tag{typeidx : typeidx}(TAG_tag(typeidx)) = $free_typeidx(typeidx)

;; 2-syntax-aux.watsup
def $free_elemmode(elemmode : elemmode) : free
  ;; 2-syntax-aux.watsup
  def $free_elemmode{tableidx : tableidx, expr : expr}(ACTIVE_elemmode(tableidx, expr)) = $free_tableidx(tableidx) +++ $free_expr(expr)
  ;; 2-syntax-aux.watsup
  def $free_elemmode(PASSIVE_elemmode) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}
  ;; 2-syntax-aux.watsup
  def $free_elemmode(DECLARE_elemmode) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_elem(elem : elem) : free
  ;; 2-syntax-aux.watsup
  def $free_elem{reftype : reftype, `expr*` : expr*, elemmode : elemmode}(ELEM_elem(reftype, expr*{expr <- `expr*`}, elemmode)) = $free_reftype(reftype) +++ $free_list($free_expr(expr)*{expr <- `expr*`}) +++ $free_elemmode(elemmode)

;; 2-syntax-aux.watsup
def $free_datamode(datamode : datamode) : free
  ;; 2-syntax-aux.watsup
  def $free_datamode{memidx : memidx, expr : expr}(ACTIVE_datamode(memidx, expr)) = $free_memidx(memidx) +++ $free_expr(expr)
  ;; 2-syntax-aux.watsup
  def $free_datamode(PASSIVE_datamode) = {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], ELEMS [], DATAS [], LOCALS [], LABELS []}

;; 2-syntax-aux.watsup
def $free_data(data : data) : free
  ;; 2-syntax-aux.watsup
  def $free_data{`byte*` : byte*, datamode : datamode}(DATA_data(byte*{byte <- `byte*`}, datamode)) = $free_datamode(datamode)

;; 2-syntax-aux.watsup
def $free_start(start : start) : free
  ;; 2-syntax-aux.watsup
  def $free_start{funcidx : funcidx}(START_start(funcidx)) = $free_funcidx(funcidx)

;; 2-syntax-aux.watsup
def $free_export(export : export) : free
  ;; 2-syntax-aux.watsup
  def $free_export{name : name, externidx : externidx}(EXPORT_export(name, externidx)) = $free_externidx(externidx)

;; 2-syntax-aux.watsup
def $free_import(import : import) : free
  ;; 2-syntax-aux.watsup
  def $free_import{name_1 : name, name_2 : name, externtype : externtype}(IMPORT_import(name_1, name_2, externtype)) = $free_externtype(externtype)

;; 2-syntax-aux.watsup
def $free_module(module : module) : free
  ;; 2-syntax-aux.watsup
  def $free_module{`type*` : type*, `import*` : import*, `func*` : func*, `global*` : global*, `table*` : table*, `mem*` : mem*, `tag*` : tag*, `elem*` : elem*, `data*` : data*, `start?` : start?, `export*` : export*}(MODULE_module(type*{type <- `type*`}, import*{import <- `import*`}, func*{func <- `func*`}, global*{global <- `global*`}, table*{table <- `table*`}, mem*{mem <- `mem*`}, tag*{tag <- `tag*`}, elem*{elem <- `elem*`}, data*{data <- `data*`}, start?{start <- `start?`}, export*{export <- `export*`})) = $free_list($free_type(type)*{type <- `type*`}) +++ $free_list($free_import(import)*{import <- `import*`}) +++ $free_list($free_func(func)*{func <- `func*`}) +++ $free_list($free_global(global)*{global <- `global*`}) +++ $free_list($free_table(table)*{table <- `table*`}) +++ $free_list($free_mem(mem)*{mem <- `mem*`}) +++ $free_list($free_tag(tag)*{tag <- `tag*`}) +++ $free_list($free_elem(elem)*{elem <- `elem*`}) +++ $free_list($free_data(data)*{data <- `data*`}) +++ $free_opt($free_start(start)?{start <- `start?`}) +++ $free_list($free_export(export)*{export <- `export*`})

;; 2-syntax-aux.watsup
def $funcidx_module(module : module) : funcidx*
  ;; 2-syntax-aux.watsup
  def $funcidx_module{module : module}(module) = $free_module(module).FUNCS_free

;; 2-syntax-aux.watsup
def $dataidx_funcs(func*) : dataidx*
  ;; 2-syntax-aux.watsup
  def $dataidx_funcs{`func*` : func*}(func*{func <- `func*`}) = $free_list($free_func(func)*{func <- `func*`}).DATAS_free

;; 3-typing.watsup
syntax init =
  | SET
  | UNSET

;; 3-typing.watsup
syntax localtype =
  | `%%`{init : init, valtype : valtype}(init : init, valtype : valtype)

;; 3-typing.watsup
syntax instrtype =
  | `%->_%%`{resulttype : resulttype, `localidx*` : localidx*}(resulttype : resulttype, localidx*{localidx <- `localidx*`} : localidx*, resulttype)

;; 3-typing.watsup
syntax context =
{
  TYPES{`deftype*` : deftype*} deftype*,
  RECS{`subtype*` : subtype*} subtype*,
  FUNCS{`deftype*` : deftype*} deftype*,
  GLOBALS{`globaltype*` : globaltype*} globaltype*,
  TABLES{`tabletype*` : tabletype*} tabletype*,
  MEMS{`memtype*` : memtype*} memtype*,
  TAGS{`tagtype*` : tagtype*} tagtype*,
  ELEMS{`elemtype*` : elemtype*} elemtype*,
  DATAS{`datatype*` : datatype*} datatype*,
  LOCALS{`localtype*` : localtype*} localtype*,
  LABELS{`resulttype*` : resulttype*} resulttype*,
  RETURN{`resulttype?` : resulttype?} resulttype?,
  REFS{`funcidx*` : funcidx*} funcidx*
}

;; 3-typing.watsup
rec {

;; 3-typing.watsup:44.1-44.86
def $with_locals(context : context, localidx*, localtype*) : context
  ;; 3-typing.watsup:46.1-46.34
  def $with_locals{C : context}(C, [], []) = C
  ;; 3-typing.watsup:47.1-47.90
  def $with_locals{C : context, x_1 : idx, `x*` : idx*, lct_1 : localtype, `lct*` : localtype*}(C, [x_1] ++ x*{x <- `x*`}, [lct_1] ++ lct*{lct <- `lct*`}) = $with_locals(C[LOCALS_context[x_1!`%`_idx.0] = lct_1], x*{x <- `x*`}, lct*{lct <- `lct*`})
}

;; 3-typing.watsup
rec {

;; 3-typing.watsup:55.1-55.94
def $clos_deftypes(deftype*) : deftype*
  ;; 3-typing.watsup:62.1-62.30
  def $clos_deftypes([]) = []
  ;; 3-typing.watsup:63.1-63.101
  def $clos_deftypes{`dt*` : deftype*, dt_n : deftype, `dt'*` : deftype*}(dt*{dt <- `dt*`} ++ [dt_n]) = dt'*{dt' <- `dt'*`} ++ [$subst_all_deftype(dt_n, (dt' : deftype <: heaptype)*{dt' <- `dt'*`})]
    -- if (dt'*{dt' <- `dt'*`} = $clos_deftypes(dt*{dt <- `dt*`}))
}

;; 3-typing.watsup
def $clos_valtype(context : context, valtype : valtype) : valtype
  ;; 3-typing.watsup
  def $clos_valtype{C : context, t : valtype, `dt*` : deftype*}(C, t) = $subst_all_valtype(t, (dt : deftype <: heaptype)*{dt <- `dt*`})
    -- if (dt*{dt <- `dt*`} = $clos_deftypes(C.TYPES_context))

;; 3-typing.watsup
def $clos_deftype(context : context, deftype : deftype) : deftype
  ;; 3-typing.watsup
  def $clos_deftype{C : context, dt : deftype, `dt'*` : deftype*}(C, dt) = $subst_all_deftype(dt, (dt' : deftype <: heaptype)*{dt' <- `dt'*`})
    -- if (dt'*{dt' <- `dt'*`} = $clos_deftypes(C.TYPES_context))

;; 3-typing.watsup
def $clos_moduletype(context : context, moduletype : moduletype) : moduletype
  ;; 3-typing.watsup
  def $clos_moduletype{C : context, mmt : moduletype, `dt*` : deftype*}(C, mmt) = $subst_all_moduletype(mmt, (dt : deftype <: heaptype)*{dt <- `dt*`})
    -- if (dt*{dt <- `dt*`} = $clos_deftypes(C.TYPES_context))

;; 3-typing.watsup
relation Numtype_ok: `%|-%:OK`(context, numtype)
  ;; 3-typing.watsup
  rule _{C : context, numtype : numtype}:
    `%|-%:OK`(C, numtype)

;; 3-typing.watsup
relation Vectype_ok: `%|-%:OK`(context, vectype)
  ;; 3-typing.watsup
  rule _{C : context, vectype : vectype}:
    `%|-%:OK`(C, vectype)

;; 3-typing.watsup
relation Heaptype_ok: `%|-%:OK`(context, heaptype)
  ;; 3-typing.watsup
  rule abs{C : context, absheaptype : absheaptype}:
    `%|-%:OK`(C, (absheaptype : absheaptype <: heaptype))

  ;; 3-typing.watsup
  rule typeidx{C : context, typeidx : typeidx, dt : deftype}:
    `%|-%:OK`(C, _IDX_heaptype(typeidx))
    -- if (C.TYPES_context[typeidx!`%`_typeidx.0] = dt)

  ;; 3-typing.watsup
  rule rec{C : context, i : n, st : subtype}:
    `%|-%:OK`(C, REC_heaptype(i))
    -- if (C.RECS_context[i] = st)

;; 3-typing.watsup
relation Reftype_ok: `%|-%:OK`(context, reftype)
  ;; 3-typing.watsup
  rule _{C : context, heaptype : heaptype}:
    `%|-%:OK`(C, REF_reftype(NULL_NULL?{}, heaptype))
    -- Heaptype_ok: `%|-%:OK`(C, heaptype)

;; 3-typing.watsup
relation Valtype_ok: `%|-%:OK`(context, valtype)
  ;; 3-typing.watsup
  rule num{C : context, numtype : numtype}:
    `%|-%:OK`(C, (numtype : numtype <: valtype))
    -- Numtype_ok: `%|-%:OK`(C, numtype)

  ;; 3-typing.watsup
  rule vec{C : context, vectype : vectype}:
    `%|-%:OK`(C, (vectype : vectype <: valtype))
    -- Vectype_ok: `%|-%:OK`(C, vectype)

  ;; 3-typing.watsup
  rule ref{C : context, reftype : reftype}:
    `%|-%:OK`(C, (reftype : reftype <: valtype))
    -- Reftype_ok: `%|-%:OK`(C, reftype)

  ;; 3-typing.watsup
  rule bot{C : context}:
    `%|-%:OK`(C, BOT_valtype)

;; 3-typing.watsup
relation Resulttype_ok: `%|-%:OK`(context, resulttype)
  ;; 3-typing.watsup
  rule _{C : context, `t*` : valtype*}:
    `%|-%:OK`(C, `%`_resulttype(t*{t <- `t*`}))
    -- (Valtype_ok: `%|-%:OK`(C, t))*{t <- `t*`}

;; 3-typing.watsup
relation Instrtype_ok: `%|-%:OK`(context, instrtype)
  ;; 3-typing.watsup
  rule _{C : context, `t_1*` : valtype*, `x*` : idx*, `t_2*` : valtype*, `lct*` : localtype*}:
    `%|-%:OK`(C, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), x*{x <- `x*`}, `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Resulttype_ok: `%|-%:OK`(C, `%`_resulttype(t_1*{t_1 <- `t_1*`}))
    -- Resulttype_ok: `%|-%:OK`(C, `%`_resulttype(t_2*{t_2 <- `t_2*`}))
    -- (if (C.LOCALS_context[x!`%`_idx.0] = lct))*{lct <- `lct*`, x <- `x*`}

;; 3-typing.watsup
syntax oktypeidx =
  | OK{typeidx : typeidx}(typeidx : typeidx)

;; 3-typing.watsup
syntax oktypeidxnat =
  | OK{typeidx : typeidx, nat : nat}(typeidx : typeidx, nat : nat)

;; 3-typing.watsup
relation Packtype_ok: `%|-%:OK`(context, packtype)
  ;; 3-typing.watsup
  rule _{C : context, packtype : packtype}:
    `%|-%:OK`(C, packtype)

;; 3-typing.watsup
relation Storagetype_ok: `%|-%:OK`(context, storagetype)
  ;; 3-typing.watsup
  rule val{C : context, valtype : valtype}:
    `%|-%:OK`(C, (valtype : valtype <: storagetype))
    -- Valtype_ok: `%|-%:OK`(C, valtype)

  ;; 3-typing.watsup
  rule pack{C : context, packtype : packtype}:
    `%|-%:OK`(C, (packtype : packtype <: storagetype))
    -- Packtype_ok: `%|-%:OK`(C, packtype)

;; 3-typing.watsup
relation Fieldtype_ok: `%|-%:OK`(context, fieldtype)
  ;; 3-typing.watsup
  rule _{C : context, storagetype : storagetype}:
    `%|-%:OK`(C, `%%`_fieldtype(MUT_MUT?{}, storagetype))
    -- Storagetype_ok: `%|-%:OK`(C, storagetype)

;; 3-typing.watsup
relation Functype_ok: `%|-%:OK`(context, functype)
  ;; 3-typing.watsup
  rule _{C : context, `t_1*` : valtype*, `t_2*` : valtype*}:
    `%|-%:OK`(C, `%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Resulttype_ok: `%|-%:OK`(C, `%`_resulttype(t_1*{t_1 <- `t_1*`}))
    -- Resulttype_ok: `%|-%:OK`(C, `%`_resulttype(t_2*{t_2 <- `t_2*`}))

;; 3-typing.watsup
relation Comptype_ok: `%|-%:OK`(context, comptype)
  ;; 3-typing.watsup
  rule struct{C : context, `fieldtype*` : fieldtype*}:
    `%|-%:OK`(C, STRUCT_comptype(`%`_structtype(fieldtype*{fieldtype <- `fieldtype*`})))
    -- (Fieldtype_ok: `%|-%:OK`(C, fieldtype))*{fieldtype <- `fieldtype*`}

  ;; 3-typing.watsup
  rule array{C : context, fieldtype : fieldtype}:
    `%|-%:OK`(C, ARRAY_comptype(fieldtype))
    -- Fieldtype_ok: `%|-%:OK`(C, fieldtype)

  ;; 3-typing.watsup
  rule func{C : context, functype : functype}:
    `%|-%:OK`(C, FUNC_comptype(functype))
    -- Functype_ok: `%|-%:OK`(C, functype)

;; 3-typing.watsup
relation Packtype_sub: `%|-%<:%`(context, packtype, packtype)
  ;; 3-typing.watsup
  rule _{C : context, packtype : packtype}:
    `%|-%<:%`(C, packtype, packtype)

;; 3-typing.watsup
relation Numtype_sub: `%|-%<:%`(context, numtype, numtype)
  ;; 3-typing.watsup
  rule _{C : context, numtype : numtype}:
    `%|-%<:%`(C, numtype, numtype)

;; 3-typing.watsup
rec {

;; 3-typing.watsup:150.1-150.107
relation Deftype_sub: `%|-%<:%`(context, deftype, deftype)
  ;; 3-typing.watsup:476.1-478.66
  rule refl{C : context, deftype_1 : deftype, deftype_2 : deftype}:
    `%|-%<:%`(C, deftype_1, deftype_2)
    -- if ($clos_deftype(C, deftype_1) = $clos_deftype(C, deftype_2))

  ;; 3-typing.watsup:480.1-483.49
  rule super{C : context, deftype_1 : deftype, deftype_2 : deftype, fin : fin, `typeuse*` : typeuse*, ct : comptype, i : nat}:
    `%|-%<:%`(C, deftype_1, deftype_2)
    -- if ($unrolldt(deftype_1) = SUB_subtype(fin, typeuse*{typeuse <- `typeuse*`}, ct))
    -- Heaptype_sub: `%|-%<:%`(C, (typeuse*{typeuse <- `typeuse*`}[i] : typeuse <: heaptype), (deftype_2 : deftype <: heaptype))

;; 3-typing.watsup:310.1-310.104
relation Heaptype_sub: `%|-%<:%`(context, heaptype, heaptype)
  ;; 3-typing.watsup:321.1-322.28
  rule refl{C : context, heaptype : heaptype}:
    `%|-%<:%`(C, heaptype, heaptype)

  ;; 3-typing.watsup:324.1-328.48
  rule trans{C : context, heaptype_1 : heaptype, heaptype_2 : heaptype, heaptype' : heaptype}:
    `%|-%<:%`(C, heaptype_1, heaptype_2)
    -- Heaptype_ok: `%|-%:OK`(C, heaptype')
    -- Heaptype_sub: `%|-%<:%`(C, heaptype_1, heaptype')
    -- Heaptype_sub: `%|-%<:%`(C, heaptype', heaptype_2)

  ;; 3-typing.watsup:330.1-331.17
  rule `eq-any`{C : context}:
    `%|-%<:%`(C, EQ_heaptype, ANY_heaptype)

  ;; 3-typing.watsup:333.1-334.17
  rule `i31-eq`{C : context}:
    `%|-%<:%`(C, I31_heaptype, EQ_heaptype)

  ;; 3-typing.watsup:336.1-337.20
  rule `struct-eq`{C : context}:
    `%|-%<:%`(C, STRUCT_heaptype, EQ_heaptype)

  ;; 3-typing.watsup:339.1-340.19
  rule `array-eq`{C : context}:
    `%|-%<:%`(C, ARRAY_heaptype, EQ_heaptype)

  ;; 3-typing.watsup:342.1-344.42
  rule struct{C : context, deftype : deftype, `fieldtype*` : fieldtype*}:
    `%|-%<:%`(C, (deftype : deftype <: heaptype), STRUCT_heaptype)
    -- Expand: `%~~%`(deftype, STRUCT_comptype(`%`_structtype(fieldtype*{fieldtype <- `fieldtype*`})))

  ;; 3-typing.watsup:346.1-348.40
  rule array{C : context, deftype : deftype, fieldtype : fieldtype}:
    `%|-%<:%`(C, (deftype : deftype <: heaptype), ARRAY_heaptype)
    -- Expand: `%~~%`(deftype, ARRAY_comptype(fieldtype))

  ;; 3-typing.watsup:350.1-352.38
  rule func{C : context, deftype : deftype, functype : functype}:
    `%|-%<:%`(C, (deftype : deftype <: heaptype), FUNC_heaptype)
    -- Expand: `%~~%`(deftype, FUNC_comptype(functype))

  ;; 3-typing.watsup:354.1-356.46
  rule def{C : context, deftype_1 : deftype, deftype_2 : deftype}:
    `%|-%<:%`(C, (deftype_1 : deftype <: heaptype), (deftype_2 : deftype <: heaptype))
    -- Deftype_sub: `%|-%<:%`(C, deftype_1, deftype_2)

  ;; 3-typing.watsup:358.1-360.53
  rule `typeidx-l`{C : context, typeidx : typeidx, heaptype : heaptype}:
    `%|-%<:%`(C, _IDX_heaptype(typeidx), heaptype)
    -- Heaptype_sub: `%|-%<:%`(C, (C.TYPES_context[typeidx!`%`_typeidx.0] : deftype <: heaptype), heaptype)

  ;; 3-typing.watsup:362.1-364.53
  rule `typeidx-r`{C : context, heaptype : heaptype, typeidx : typeidx}:
    `%|-%<:%`(C, heaptype, _IDX_heaptype(typeidx))
    -- Heaptype_sub: `%|-%<:%`(C, heaptype, (C.TYPES_context[typeidx!`%`_typeidx.0] : deftype <: heaptype))

  ;; 3-typing.watsup:366.1-368.40
  rule rec{C : context, i : n, `typeuse*` : typeuse*, j : nat, fin : fin, ct : comptype}:
    `%|-%<:%`(C, REC_heaptype(i), (typeuse*{typeuse <- `typeuse*`}[j] : typeuse <: heaptype))
    -- if (C.RECS_context[i] = SUB_subtype(fin, typeuse*{typeuse <- `typeuse*`}, ct))

  ;; 3-typing.watsup:370.1-372.40
  rule none{C : context, heaptype : heaptype}:
    `%|-%<:%`(C, NONE_heaptype, heaptype)
    -- Heaptype_sub: `%|-%<:%`(C, heaptype, ANY_heaptype)

  ;; 3-typing.watsup:374.1-376.41
  rule nofunc{C : context, heaptype : heaptype}:
    `%|-%<:%`(C, NOFUNC_heaptype, heaptype)
    -- Heaptype_sub: `%|-%<:%`(C, heaptype, FUNC_heaptype)

  ;; 3-typing.watsup:378.1-380.43
  rule noextern{C : context, heaptype : heaptype}:
    `%|-%<:%`(C, NOEXTERN_heaptype, heaptype)
    -- Heaptype_sub: `%|-%<:%`(C, heaptype, EXTERN_heaptype)

  ;; 3-typing.watsup:382.1-383.23
  rule bot{C : context, heaptype : heaptype}:
    `%|-%<:%`(C, BOT_heaptype, heaptype)
}

;; 3-typing.watsup
relation Reftype_sub: `%|-%<:%`(context, reftype, reftype)
  ;; 3-typing.watsup
  rule nonnull{C : context, ht_1 : heaptype, ht_2 : heaptype}:
    `%|-%<:%`(C, REF_reftype(?(), ht_1), REF_reftype(?(), ht_2))
    -- Heaptype_sub: `%|-%<:%`(C, ht_1, ht_2)

  ;; 3-typing.watsup
  rule null{C : context, ht_1 : heaptype, ht_2 : heaptype}:
    `%|-%<:%`(C, REF_reftype(NULL_NULL?{}, ht_1), REF_reftype(?(NULL_NULL), ht_2))
    -- Heaptype_sub: `%|-%<:%`(C, ht_1, ht_2)

;; 3-typing.watsup
relation Vectype_sub: `%|-%<:%`(context, vectype, vectype)
  ;; 3-typing.watsup
  rule _{C : context, vectype : vectype}:
    `%|-%<:%`(C, vectype, vectype)

;; 3-typing.watsup
relation Valtype_sub: `%|-%<:%`(context, valtype, valtype)
  ;; 3-typing.watsup
  rule num{C : context, numtype_1 : numtype, numtype_2 : numtype}:
    `%|-%<:%`(C, (numtype_1 : numtype <: valtype), (numtype_2 : numtype <: valtype))
    -- Numtype_sub: `%|-%<:%`(C, numtype_1, numtype_2)

  ;; 3-typing.watsup
  rule vec{C : context, vectype_1 : vectype, vectype_2 : vectype}:
    `%|-%<:%`(C, (vectype_1 : vectype <: valtype), (vectype_2 : vectype <: valtype))
    -- Vectype_sub: `%|-%<:%`(C, vectype_1, vectype_2)

  ;; 3-typing.watsup
  rule ref{C : context, reftype_1 : reftype, reftype_2 : reftype}:
    `%|-%<:%`(C, (reftype_1 : reftype <: valtype), (reftype_2 : reftype <: valtype))
    -- Reftype_sub: `%|-%<:%`(C, reftype_1, reftype_2)

  ;; 3-typing.watsup
  rule bot{C : context, valtype : valtype}:
    `%|-%<:%`(C, BOT_valtype, valtype)

;; 3-typing.watsup
relation Storagetype_sub: `%|-%<:%`(context, storagetype, storagetype)
  ;; 3-typing.watsup
  rule val{C : context, valtype_1 : valtype, valtype_2 : valtype}:
    `%|-%<:%`(C, (valtype_1 : valtype <: storagetype), (valtype_2 : valtype <: storagetype))
    -- Valtype_sub: `%|-%<:%`(C, valtype_1, valtype_2)

  ;; 3-typing.watsup
  rule pack{C : context, packtype_1 : packtype, packtype_2 : packtype}:
    `%|-%<:%`(C, (packtype_1 : packtype <: storagetype), (packtype_2 : packtype <: storagetype))
    -- Packtype_sub: `%|-%<:%`(C, packtype_1, packtype_2)

;; 3-typing.watsup
relation Fieldtype_sub: `%|-%<:%`(context, fieldtype, fieldtype)
  ;; 3-typing.watsup
  rule const{C : context, zt_1 : storagetype, zt_2 : storagetype}:
    `%|-%<:%`(C, `%%`_fieldtype(?(), zt_1), `%%`_fieldtype(?(), zt_2))
    -- Storagetype_sub: `%|-%<:%`(C, zt_1, zt_2)

  ;; 3-typing.watsup
  rule var{C : context, zt_1 : storagetype, zt_2 : storagetype}:
    `%|-%<:%`(C, `%%`_fieldtype(?(MUT_MUT), zt_1), `%%`_fieldtype(?(MUT_MUT), zt_2))
    -- Storagetype_sub: `%|-%<:%`(C, zt_1, zt_2)
    -- Storagetype_sub: `%|-%<:%`(C, zt_2, zt_1)

;; 3-typing.watsup
relation Resulttype_sub: `%|-%<:%`(context, resulttype, resulttype)
  ;; 3-typing.watsup
  rule _{C : context, `t_1*` : valtype*, `t_2*` : valtype*}:
    `%|-%<:%`(C, `%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`}))
    -- (Valtype_sub: `%|-%<:%`(C, t_1, t_2))*{t_1 <- `t_1*`, t_2 <- `t_2*`}

;; 3-typing.watsup
relation Functype_sub: `%|-%<:%`(context, functype, functype)
  ;; 3-typing.watsup
  rule _{C : context, `t_11*` : valtype*, `t_12*` : valtype*, `t_21*` : valtype*, `t_22*` : valtype*}:
    `%|-%<:%`(C, `%->%`_functype(`%`_resulttype(t_11*{t_11 <- `t_11*`}), `%`_resulttype(t_12*{t_12 <- `t_12*`})), `%->%`_functype(`%`_resulttype(t_21*{t_21 <- `t_21*`}), `%`_resulttype(t_22*{t_22 <- `t_22*`})))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t_21*{t_21 <- `t_21*`}), `%`_resulttype(t_11*{t_11 <- `t_11*`}))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t_12*{t_12 <- `t_12*`}), `%`_resulttype(t_22*{t_22 <- `t_22*`}))

;; 3-typing.watsup
relation Comptype_sub: `%|-%<:%`(context, comptype, comptype)
  ;; 3-typing.watsup
  rule struct{C : context, `yt_1*` : fieldtype*, yt'_1 : fieldtype, `yt_2*` : fieldtype*}:
    `%|-%<:%`(C, STRUCT_comptype(`%`_structtype(yt_1*{yt_1 <- `yt_1*`} ++ [yt'_1])), STRUCT_comptype(`%`_structtype(yt_2*{yt_2 <- `yt_2*`})))
    -- (Fieldtype_sub: `%|-%<:%`(C, yt_1, yt_2))*{yt_1 <- `yt_1*`, yt_2 <- `yt_2*`}

  ;; 3-typing.watsup
  rule array{C : context, yt_1 : fieldtype, yt_2 : fieldtype}:
    `%|-%<:%`(C, ARRAY_comptype(yt_1), ARRAY_comptype(yt_2))
    -- Fieldtype_sub: `%|-%<:%`(C, yt_1, yt_2)

  ;; 3-typing.watsup
  rule func{C : context, ft_1 : functype, ft_2 : functype}:
    `%|-%<:%`(C, FUNC_comptype(ft_1), FUNC_comptype(ft_2))
    -- Functype_sub: `%|-%<:%`(C, ft_1, ft_2)

;; 3-typing.watsup
relation Subtype_ok: `%|-%:%`(context, subtype, oktypeidx)
  ;; 3-typing.watsup
  rule _{C : context, `x*` : idx*, comptype : comptype, x_0 : idx, `x'**` : idx**, `comptype'*` : comptype*}:
    `%|-%:%`(C, SUB_subtype(FINAL_FINAL?{}, _IDX_typeuse(x)*{x <- `x*`}, comptype), OK_oktypeidx(x_0))
    -- if (|x*{x <- `x*`}| <= 1)
    -- (if (x!`%`_idx.0 < x_0!`%`_idx.0))*{x <- `x*`}
    -- (if ($unrolldt(C.TYPES_context[x!`%`_idx.0]) = SUB_subtype(?(), _IDX_typeuse(x')*{x' <- `x'*`}, comptype')))*{comptype' <- `comptype'*`, x <- `x*`, `x'*` <- `x'**`}
    -- Comptype_ok: `%|-%:OK`(C, comptype)
    -- (Comptype_sub: `%|-%<:%`(C, comptype, comptype'))*{comptype' <- `comptype'*`}

;; 3-typing.watsup
def $before(typeuse : typeuse, typeidx : typeidx, nat : nat) : bool
  ;; 3-typing.watsup
  def $before{deftype : deftype, x : idx, i : nat}((deftype : deftype <: typeuse), x, i) = true
  ;; 3-typing.watsup
  def $before{typeidx : typeidx, x : idx, i : nat}(_IDX_typeuse(typeidx), x, i) = (typeidx!`%`_typeidx.0 < x!`%`_idx.0)
  ;; 3-typing.watsup
  def $before{j : n, x : idx, i : nat}(REC_typeuse(j), x, i) = (j < i)

;; 3-typing.watsup
def $unrollht(context : context, heaptype : heaptype) : subtype
  ;; 3-typing.watsup
  def $unrollht{C : context, deftype : deftype}(C, (deftype : deftype <: heaptype)) = $unrolldt(deftype)
  ;; 3-typing.watsup
  def $unrollht{C : context, typeidx : typeidx}(C, _IDX_heaptype(typeidx)) = $unrolldt(C.TYPES_context[typeidx!`%`_typeidx.0])
  ;; 3-typing.watsup
  def $unrollht{C : context, i : n}(C, REC_heaptype(i)) = C.RECS_context[i]

;; 3-typing.watsup
relation Subtype_ok2: `%|-%:%`(context, subtype, oktypeidxnat)
  ;; 3-typing.watsup
  rule _{C : context, `typeuse*` : typeuse*, compttype : comptype, x : idx, i : nat, `typeuse'**` : typeuse**, `comptype'*` : comptype*, comptype : comptype}:
    `%|-%:%`(C, SUB_subtype(FINAL_FINAL?{}, typeuse*{typeuse <- `typeuse*`}, compttype), OK_oktypeidxnat(x, i))
    -- if (|typeuse*{typeuse <- `typeuse*`}| <= 1)
    -- (if $before(typeuse, x, i))*{typeuse <- `typeuse*`}
    -- (if ($unrollht(C, (typeuse : typeuse <: heaptype)) = SUB_subtype(?(), typeuse'*{typeuse' <- `typeuse'*`}, comptype')))*{comptype' <- `comptype'*`, typeuse <- `typeuse*`, `typeuse'*` <- `typeuse'**`}
    -- Comptype_ok: `%|-%:OK`(C, comptype)
    -- (Comptype_sub: `%|-%<:%`(C, comptype, comptype'))*{comptype' <- `comptype'*`}

;; 3-typing.watsup
rec {

;; 3-typing.watsup:145.1-145.105
relation Rectype_ok2: `%|-%:%`(context, rectype, oktypeidxnat)
  ;; 3-typing.watsup:223.1-224.24
  rule empty{C : context, x : idx, i : nat}:
    `%|-%:%`(C, REC_rectype(`%`_list([])), OK_oktypeidxnat(x, i))

  ;; 3-typing.watsup:226.1-229.55
  rule cons{C : context, subtype_1 : subtype, `subtype*` : subtype*, x : idx, i : nat}:
    `%|-%:%`(C, REC_rectype(`%`_list([subtype_1] ++ subtype*{subtype <- `subtype*`})), OK_oktypeidxnat(x, i))
    -- Subtype_ok2: `%|-%:%`(C, subtype_1, OK_oktypeidxnat(x, i))
    -- Rectype_ok2: `%|-%:%`(C, REC_rectype(`%`_list(subtype*{subtype <- `subtype*`})), OK_oktypeidxnat(`%`_typeidx((x!`%`_idx.0 + 1)), (i + 1)))
}

;; 3-typing.watsup
rec {

;; 3-typing.watsup:143.1-143.124
relation Rectype_ok: `%|-%:%`(context, rectype, oktypeidx)
  ;; 3-typing.watsup:211.1-212.23
  rule empty{C : context, x : idx}:
    `%|-%:%`(C, REC_rectype(`%`_list([])), OK_oktypeidx(x))

  ;; 3-typing.watsup:214.1-217.48
  rule cons{C : context, subtype_1 : subtype, `subtype*` : subtype*, x : idx}:
    `%|-%:%`(C, REC_rectype(`%`_list([subtype_1] ++ subtype*{subtype <- `subtype*`})), OK_oktypeidx(x))
    -- Subtype_ok: `%|-%:%`(C, subtype_1, OK_oktypeidx(x))
    -- Rectype_ok: `%|-%:%`(C, REC_rectype(`%`_list(subtype*{subtype <- `subtype*`})), OK_oktypeidx(`%`_typeidx((x!`%`_idx.0 + 1))))

  ;; 3-typing.watsup:219.1-221.60
  rule _rec2{C : context, `subtype*` : subtype*, x : idx}:
    `%|-%:%`(C, REC_rectype(`%`_list(subtype*{subtype <- `subtype*`})), OK_oktypeidx(x))
    -- Rectype_ok2: `%|-%:%`({TYPES [], RECS subtype*{subtype <- `subtype*`}, FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []} +++ C, REC_rectype(`%`_list(subtype*{subtype <- `subtype*`})), OK_oktypeidxnat(x, 0))
}

;; 3-typing.watsup
relation Deftype_ok: `%|-%:OK`(context, deftype)
  ;; 3-typing.watsup
  rule _{C : context, rectype : rectype, i : n, x : idx, `subtype*` : subtype*, n : n}:
    `%|-%:OK`(C, DEF_deftype(rectype, i))
    -- Rectype_ok: `%|-%:%`(C, rectype, OK_oktypeidx(x))
    -- if (rectype = REC_rectype(`%`_list(subtype^n{subtype <- `subtype*`})))
    -- if (i < n)

;; 3-typing.watsup
relation Limits_ok: `%|-%:%`(context, limits, nat)
  ;; 3-typing.watsup
  rule _{C : context, n : n, m : m, k : nat}:
    `%|-%:%`(C, `[%..%]`_limits(`%`_u64(n), `%`_u64(m)), k)
    -- if ((n <= m) /\ (m <= k))

;; 3-typing.watsup
relation Globaltype_ok: `%|-%:OK`(context, globaltype)
  ;; 3-typing.watsup
  rule _{C : context, t : valtype}:
    `%|-%:OK`(C, `%%`_globaltype(MUT_MUT?{}, t))
    -- Valtype_ok: `%|-%:OK`(C, t)

;; 3-typing.watsup
relation Tabletype_ok: `%|-%:OK`(context, tabletype)
  ;; 3-typing.watsup
  rule _{C : context, addrtype : addrtype, limits : limits, reftype : reftype}:
    `%|-%:OK`(C, `%%%`_tabletype(addrtype, limits, reftype))
    -- Limits_ok: `%|-%:%`(C, limits, ((((2 ^ 32) : nat <:> int) - (1 : nat <:> int)) : int <:> nat))
    -- Reftype_ok: `%|-%:OK`(C, reftype)

;; 3-typing.watsup
relation Memtype_ok: `%|-%:OK`(context, memtype)
  ;; 3-typing.watsup
  rule _{C : context, addrtype : addrtype, limits : limits}:
    `%|-%:OK`(C, `%%PAGE`_memtype(addrtype, limits))
    -- Limits_ok: `%|-%:%`(C, limits, (2 ^ 16))

;; 3-typing.watsup
relation Tagtype_ok: `%|-%:OK`(context, tagtype)
  ;; 3-typing.watsup
  rule _{C : context, deftype : deftype, functype : functype}:
    `%|-%:OK`(C, deftype)
    -- Deftype_ok: `%|-%:OK`(C, deftype)
    -- Expand: `%~~%`(deftype, FUNC_comptype(functype))

;; 3-typing.watsup
relation Externtype_ok: `%|-%:OK`(context, externtype)
  ;; 3-typing.watsup
  rule func{C : context, deftype : deftype, functype : functype}:
    `%|-%:OK`(C, FUNC_externtype((deftype : deftype <: typeuse)))
    -- Deftype_ok: `%|-%:OK`(C, deftype)
    -- Expand: `%~~%`(deftype, FUNC_comptype(functype))

  ;; 3-typing.watsup
  rule global{C : context, globaltype : globaltype}:
    `%|-%:OK`(C, GLOBAL_externtype(globaltype))
    -- Globaltype_ok: `%|-%:OK`(C, globaltype)

  ;; 3-typing.watsup
  rule table{C : context, tabletype : tabletype}:
    `%|-%:OK`(C, TABLE_externtype(tabletype))
    -- Tabletype_ok: `%|-%:OK`(C, tabletype)

  ;; 3-typing.watsup
  rule mem{C : context, memtype : memtype}:
    `%|-%:OK`(C, MEM_externtype(memtype))
    -- Memtype_ok: `%|-%:OK`(C, memtype)

  ;; 3-typing.watsup
  rule tag{C : context, tagtype : tagtype}:
    `%|-%:OK`(C, TAG_externtype((tagtype : deftype <: typeuse)))
    -- Tagtype_ok: `%|-%:OK`(C, tagtype)

;; 3-typing.watsup
relation Instrtype_sub: `%|-%<:%`(context, instrtype, instrtype)
  ;; 3-typing.watsup
  rule _{C : context, `t_11*` : valtype*, `x_1*` : idx*, `t_12*` : valtype*, `t_21*` : valtype*, `x_2*` : idx*, `t_22*` : valtype*, `x*` : idx*, `t*` : valtype*}:
    `%|-%<:%`(C, `%->_%%`_instrtype(`%`_resulttype(t_11*{t_11 <- `t_11*`}), x_1*{x_1 <- `x_1*`}, `%`_resulttype(t_12*{t_12 <- `t_12*`})), `%->_%%`_instrtype(`%`_resulttype(t_21*{t_21 <- `t_21*`}), x_2*{x_2 <- `x_2*`}, `%`_resulttype(t_22*{t_22 <- `t_22*`})))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t_21*{t_21 <- `t_21*`}), `%`_resulttype(t_11*{t_11 <- `t_11*`}))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t_12*{t_12 <- `t_12*`}), `%`_resulttype(t_22*{t_22 <- `t_22*`}))
    -- if (x*{x <- `x*`} = $setminus_(syntax localidx, x_2*{x_2 <- `x_2*`}, x_1*{x_1 <- `x_1*`}))
    -- (if (C.LOCALS_context[x!`%`_idx.0] = `%%`_localtype(SET_init, t)))*{t <- `t*`, x <- `x*`}

;; 3-typing.watsup
relation Limits_sub: `%|-%<:%`(context, limits, limits)
  ;; 3-typing.watsup
  rule _{C : context, n_1 : n, m_1 : m, n_2 : n, m_2 : m}:
    `%|-%<:%`(C, `[%..%]`_limits(`%`_u64(n_1), `%`_u64(m_1)), `[%..%]`_limits(`%`_u64(n_2), `%`_u64(m_2)))
    -- if (n_1 >= n_2)
    -- if (m_1 <= m_2)

;; 3-typing.watsup
relation Globaltype_sub: `%|-%<:%`(context, globaltype, globaltype)
  ;; 3-typing.watsup
  rule const{C : context, valtype_1 : valtype, valtype_2 : valtype}:
    `%|-%<:%`(C, `%%`_globaltype(?(), valtype_1), `%%`_globaltype(?(), valtype_2))
    -- Valtype_sub: `%|-%<:%`(C, valtype_1, valtype_2)

  ;; 3-typing.watsup
  rule var{C : context, valtype_1 : valtype, valtype_2 : valtype}:
    `%|-%<:%`(C, `%%`_globaltype(?(MUT_MUT), valtype_1), `%%`_globaltype(?(MUT_MUT), valtype_2))
    -- Valtype_sub: `%|-%<:%`(C, valtype_1, valtype_2)
    -- Valtype_sub: `%|-%<:%`(C, valtype_2, valtype_1)

;; 3-typing.watsup
relation Tabletype_sub: `%|-%<:%`(context, tabletype, tabletype)
  ;; 3-typing.watsup
  rule _{C : context, addrtype : addrtype, limits_1 : limits, reftype_1 : reftype, limits_2 : limits, reftype_2 : reftype}:
    `%|-%<:%`(C, `%%%`_tabletype(addrtype, limits_1, reftype_1), `%%%`_tabletype(addrtype, limits_2, reftype_2))
    -- Limits_sub: `%|-%<:%`(C, limits_1, limits_2)
    -- Reftype_sub: `%|-%<:%`(C, reftype_1, reftype_2)
    -- Reftype_sub: `%|-%<:%`(C, reftype_2, reftype_1)

;; 3-typing.watsup
relation Memtype_sub: `%|-%<:%`(context, memtype, memtype)
  ;; 3-typing.watsup
  rule _{C : context, addrtype : addrtype, limits_1 : limits, limits_2 : limits}:
    `%|-%<:%`(C, `%%PAGE`_memtype(addrtype, limits_1), `%%PAGE`_memtype(addrtype, limits_2))
    -- Limits_sub: `%|-%<:%`(C, limits_1, limits_2)

;; 3-typing.watsup
relation Tagtype_sub: `%|-%<:%`(context, tagtype, tagtype)
  ;; 3-typing.watsup
  rule _{C : context, deftype_1 : deftype, deftype_2 : deftype}:
    `%|-%<:%`(C, deftype_1, deftype_2)
    -- Deftype_sub: `%|-%<:%`(C, deftype_1, deftype_2)
    -- Deftype_sub: `%|-%<:%`(C, deftype_2, deftype_1)

;; 3-typing.watsup
relation Externtype_sub: `%|-%<:%`(context, externtype, externtype)
  ;; 3-typing.watsup
  rule func{C : context, deftype_1 : deftype, deftype_2 : deftype}:
    `%|-%<:%`(C, FUNC_externtype((deftype_1 : deftype <: typeuse)), FUNC_externtype((deftype_2 : deftype <: typeuse)))
    -- Deftype_sub: `%|-%<:%`(C, deftype_1, deftype_2)

  ;; 3-typing.watsup
  rule global{C : context, globaltype_1 : globaltype, globaltype_2 : globaltype}:
    `%|-%<:%`(C, GLOBAL_externtype(globaltype_1), GLOBAL_externtype(globaltype_2))
    -- Globaltype_sub: `%|-%<:%`(C, globaltype_1, globaltype_2)

  ;; 3-typing.watsup
  rule table{C : context, tabletype_1 : tabletype, tabletype_2 : tabletype}:
    `%|-%<:%`(C, TABLE_externtype(tabletype_1), TABLE_externtype(tabletype_2))
    -- Tabletype_sub: `%|-%<:%`(C, tabletype_1, tabletype_2)

  ;; 3-typing.watsup
  rule mem{C : context, memtype_1 : memtype, memtype_2 : memtype}:
    `%|-%<:%`(C, MEM_externtype(memtype_1), MEM_externtype(memtype_2))
    -- Memtype_sub: `%|-%<:%`(C, memtype_1, memtype_2)

  ;; 3-typing.watsup
  rule tag{C : context, tagtype_1 : tagtype, tagtype_2 : tagtype}:
    `%|-%<:%`(C, TAG_externtype((tagtype_1 : deftype <: typeuse)), TAG_externtype((tagtype_2 : deftype <: typeuse)))
    -- Tagtype_sub: `%|-%<:%`(C, tagtype_1, tagtype_2)

;; 3-typing.watsup
relation Blocktype_ok: `%|-%:%`(context, blocktype, instrtype)
  ;; 3-typing.watsup
  rule valtype{C : context, `valtype?` : valtype?}:
    `%|-%:%`(C, _RESULT_blocktype(valtype?{valtype <- `valtype?`}), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype(lift(valtype?{valtype <- `valtype?`}))))
    -- (Valtype_ok: `%|-%:OK`(C, valtype))?{valtype <- `valtype?`}

  ;; 3-typing.watsup
  rule typeidx{C : context, typeidx : typeidx, `t_1*` : valtype*, `t_2*` : valtype*}:
    `%|-%:%`(C, _IDX_blocktype(typeidx), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Expand: `%~~%`(C.TYPES_context[typeidx!`%`_typeidx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`}))))

;; 3-typing.watsup
relation Catch_ok: `%|-%:OK`(context, catch)
  ;; 3-typing.watsup
  rule catch{C : context, x : idx, l : labelidx, `t*` : valtype*}:
    `%|-%:OK`(C, CATCH_catch(x, l))
    -- Expand: `%~~%`(C.TAGS_context[x!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t*{t <- `t*`}), `%`_resulttype([]))))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t*{t <- `t*`}), C.LABELS_context[l!`%`_labelidx.0])

  ;; 3-typing.watsup
  rule catch_ref{C : context, x : idx, l : labelidx, `t*` : valtype*}:
    `%|-%:OK`(C, CATCH_REF_catch(x, l))
    -- Expand: `%~~%`(C.TAGS_context[x!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t*{t <- `t*`}), `%`_resulttype([]))))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t*{t <- `t*`} ++ [REF_valtype(?(), EXN_heaptype)]), C.LABELS_context[l!`%`_labelidx.0])

  ;; 3-typing.watsup
  rule catch_all{C : context, l : labelidx}:
    `%|-%:OK`(C, CATCH_ALL_catch(l))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype([]), C.LABELS_context[l!`%`_labelidx.0])

  ;; 3-typing.watsup
  rule catch_all_ref{C : context, l : labelidx}:
    `%|-%:OK`(C, CATCH_ALL_REF_catch(l))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype([REF_valtype(?(), EXN_heaptype)]), C.LABELS_context[l!`%`_labelidx.0])

;; 6-runtime-aux.watsup
def $default_(valtype : valtype) : val?
  ;; 6-runtime-aux.watsup
  def $default_{Inn : Inn}((Inn : Inn <: valtype)) = ?(CONST_val((Inn : Inn <: numtype), `%`_num_(0)))
  ;; 6-runtime-aux.watsup
  def $default_{Fnn : Fnn}((Fnn : Fnn <: valtype)) = ?(CONST_val((Fnn : Fnn <: numtype), $fzero($size((Fnn : Fnn <: numtype)))))
  ;; 6-runtime-aux.watsup
  def $default_{Vnn : Vnn}((Vnn : Vnn <: valtype)) = ?(VCONST_val(Vnn, `%`_vec_(0)))
  ;; 6-runtime-aux.watsup
  def $default_{ht : heaptype}(REF_valtype(?(NULL_NULL), ht)) = ?(REF.NULL_val(ht))
  ;; 6-runtime-aux.watsup
  def $default_{ht : heaptype}(REF_valtype(?(), ht)) = ?()

;; 3-typing.watsup
relation Defaultable: `|-%DEFAULTABLE`(valtype)
  ;; 6-runtime-aux.watsup
  rule _{t : valtype}:
    `|-%DEFAULTABLE`(t)
    -- if ($default_(t) =/= ?())

;; 3-typing.watsup
rec {

;; 3-typing.watsup:557.1-557.95
relation Instr_ok: `%|-%:%`(context, instr, instrtype)
  ;; 3-typing.watsup:570.1-571.24
  rule nop{C : context}:
    `%|-%:%`(C, NOP_instr, `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([])))

  ;; 3-typing.watsup:573.1-575.42
  rule unreachable{C : context, `t_1*` : valtype*, `t_2*` : valtype*}:
    `%|-%:%`(C, UNREACHABLE_instr, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Instrtype_ok: `%|-%:OK`(C, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))

  ;; 3-typing.watsup:577.1-579.29
  rule drop{C : context, t : valtype}:
    `%|-%:%`(C, DROP_instr, `%->_%%`_instrtype(`%`_resulttype([t]), [], `%`_resulttype([])))
    -- Valtype_ok: `%|-%:OK`(C, t)

  ;; 3-typing.watsup:582.1-584.29
  rule `select-expl`{C : context, t : valtype}:
    `%|-%:%`(C, SELECT_instr(?([t])), `%->_%%`_instrtype(`%`_resulttype([t t I32_valtype]), [], `%`_resulttype([t])))
    -- Valtype_ok: `%|-%:OK`(C, t)

  ;; 3-typing.watsup:586.1-590.37
  rule `select-impl`{C : context, t : valtype, t' : valtype, numtype : numtype, vectype : vectype}:
    `%|-%:%`(C, SELECT_instr(?()), `%->_%%`_instrtype(`%`_resulttype([t t I32_valtype]), [], `%`_resulttype([t])))
    -- Valtype_ok: `%|-%:OK`(C, t)
    -- Valtype_sub: `%|-%<:%`(C, t, t')
    -- if ((t' = (numtype : numtype <: valtype)) \/ (t' = (vectype : vectype <: valtype)))

  ;; 3-typing.watsup:606.1-609.67
  rule block{C : context, bt : blocktype, `instr*` : instr*, `t_1*` : valtype*, `t_2*` : valtype*, `x*` : idx*}:
    `%|-%:%`(C, BLOCK_instr(bt, instr*{instr <- `instr*`}), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Blocktype_ok: `%|-%:%`(C, bt, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Instrs_ok: `%|-%:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [`%`_resulttype(t_2*{t_2 <- `t_2*`})], RETURN ?(), REFS []} +++ C, instr*{instr <- `instr*`}, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), x*{x <- `x*`}, `%`_resulttype(t_2*{t_2 <- `t_2*`})))

  ;; 3-typing.watsup:611.1-614.67
  rule loop{C : context, bt : blocktype, `instr*` : instr*, `t_1*` : valtype*, `t_2*` : valtype*, `x*` : idx*}:
    `%|-%:%`(C, LOOP_instr(bt, instr*{instr <- `instr*`}), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Blocktype_ok: `%|-%:%`(C, bt, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Instrs_ok: `%|-%:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [`%`_resulttype(t_1*{t_1 <- `t_1*`})], RETURN ?(), REFS []} +++ C, instr*{instr <- `instr*`}, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), x*{x <- `x*`}, `%`_resulttype(t_2*{t_2 <- `t_2*`})))

  ;; 3-typing.watsup:616.1-620.71
  rule if{C : context, bt : blocktype, `instr_1*` : instr*, `instr_2*` : instr*, `t_1*` : valtype*, `t_2*` : valtype*, `x_1*` : idx*, `x_2*` : idx*}:
    `%|-%:%`(C, `IF%%ELSE%`_instr(bt, instr_1*{instr_1 <- `instr_1*`}, instr_2*{instr_2 <- `instr_2*`}), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`} ++ [I32_valtype]), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Blocktype_ok: `%|-%:%`(C, bt, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Instrs_ok: `%|-%:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [`%`_resulttype(t_2*{t_2 <- `t_2*`})], RETURN ?(), REFS []} +++ C, instr_1*{instr_1 <- `instr_1*`}, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), x_1*{x_1 <- `x_1*`}, `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Instrs_ok: `%|-%:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [`%`_resulttype(t_2*{t_2 <- `t_2*`})], RETURN ?(), REFS []} +++ C, instr_2*{instr_2 <- `instr_2*`}, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), x_2*{x_2 <- `x_2*`}, `%`_resulttype(t_2*{t_2 <- `t_2*`})))

  ;; 3-typing.watsup:625.1-628.42
  rule br{C : context, l : labelidx, `t_1*` : valtype*, `t*` : valtype*, `t_2*` : valtype*}:
    `%|-%:%`(C, BR_instr(l), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`} ++ t*{t <- `t*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- if (C.LABELS_context[l!`%`_labelidx.0]!`%`_resulttype.0 = t*{t <- `t*`})
    -- Instrtype_ok: `%|-%:OK`(C, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))

  ;; 3-typing.watsup:630.1-632.25
  rule br_if{C : context, l : labelidx, `t*` : valtype*}:
    `%|-%:%`(C, BR_IF_instr(l), `%->_%%`_instrtype(`%`_resulttype(t*{t <- `t*`} ++ [I32_valtype]), [], `%`_resulttype(t*{t <- `t*`})))
    -- if (C.LABELS_context[l!`%`_labelidx.0]!`%`_resulttype.0 = t*{t <- `t*`})

  ;; 3-typing.watsup:634.1-638.42
  rule br_table{C : context, `l*` : labelidx*, l' : labelidx, `t_1*` : valtype*, `t*` : valtype*, `t_2*` : valtype*}:
    `%|-%:%`(C, BR_TABLE_instr(l*{l <- `l*`}, l'), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`} ++ t*{t <- `t*`} ++ [I32_valtype]), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- (Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t*{t <- `t*`}), C.LABELS_context[l!`%`_labelidx.0]))*{l <- `l*`}
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t*{t <- `t*`}), C.LABELS_context[l'!`%`_labelidx.0])
    -- Instrtype_ok: `%|-%:OK`(C, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))

  ;; 3-typing.watsup:640.1-643.31
  rule br_on_null{C : context, l : labelidx, `t*` : valtype*, ht : heaptype}:
    `%|-%:%`(C, BR_ON_NULL_instr(l), `%->_%%`_instrtype(`%`_resulttype(t*{t <- `t*`} ++ [REF_valtype(?(NULL_NULL), ht)]), [], `%`_resulttype(t*{t <- `t*`} ++ [REF_valtype(?(), ht)])))
    -- if (C.LABELS_context[l!`%`_labelidx.0]!`%`_resulttype.0 = t*{t <- `t*`})
    -- Heaptype_ok: `%|-%:OK`(C, ht)

  ;; 3-typing.watsup:645.1-647.34
  rule br_on_non_null{C : context, l : labelidx, `t*` : valtype*, ht : heaptype}:
    `%|-%:%`(C, BR_ON_NON_NULL_instr(l), `%->_%%`_instrtype(`%`_resulttype(t*{t <- `t*`} ++ [REF_valtype(?(NULL_NULL), ht)]), [], `%`_resulttype(t*{t <- `t*`})))
    -- if (C.LABELS_context[l!`%`_labelidx.0] = `%`_resulttype(t*{t <- `t*`} ++ [REF_valtype(?(), ht)]))

  ;; 3-typing.watsup:649.1-655.34
  rule br_on_cast{C : context, l : labelidx, rt_1 : reftype, rt_2 : reftype, `t*` : valtype*, rt : reftype}:
    `%|-%:%`(C, BR_ON_CAST_instr(l, rt_1, rt_2), `%->_%%`_instrtype(`%`_resulttype(t*{t <- `t*`} ++ [(rt_1 : reftype <: valtype)]), [], `%`_resulttype(t*{t <- `t*`} ++ [($diffrt(rt_1, rt_2) : reftype <: valtype)])))
    -- if (C.LABELS_context[l!`%`_labelidx.0] = `%`_resulttype(t*{t <- `t*`} ++ [(rt : reftype <: valtype)]))
    -- Reftype_ok: `%|-%:OK`(C, rt_1)
    -- Reftype_ok: `%|-%:OK`(C, rt_2)
    -- Reftype_sub: `%|-%<:%`(C, rt_2, rt_1)
    -- Reftype_sub: `%|-%<:%`(C, rt_2, rt)

  ;; 3-typing.watsup:657.1-663.49
  rule br_on_cast_fail{C : context, l : labelidx, rt_1 : reftype, rt_2 : reftype, `t*` : valtype*, rt : reftype}:
    `%|-%:%`(C, BR_ON_CAST_FAIL_instr(l, rt_1, rt_2), `%->_%%`_instrtype(`%`_resulttype(t*{t <- `t*`} ++ [(rt_1 : reftype <: valtype)]), [], `%`_resulttype(t*{t <- `t*`} ++ [(rt_2 : reftype <: valtype)])))
    -- if (C.LABELS_context[l!`%`_labelidx.0] = `%`_resulttype(t*{t <- `t*`} ++ [(rt : reftype <: valtype)]))
    -- Reftype_ok: `%|-%:OK`(C, rt_1)
    -- Reftype_ok: `%|-%:OK`(C, rt_2)
    -- Reftype_sub: `%|-%<:%`(C, rt_2, rt_1)
    -- Reftype_sub: `%|-%<:%`(C, $diffrt(rt_1, rt_2), rt)

  ;; 3-typing.watsup:668.1-670.47
  rule call{C : context, x : idx, `t_1*` : valtype*, `t_2*` : valtype*}:
    `%|-%:%`(C, CALL_instr(x), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Expand: `%~~%`(C.FUNCS_context[x!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`}))))

  ;; 3-typing.watsup:672.1-674.47
  rule call_ref{C : context, x : idx, `t_1*` : valtype*, `t_2*` : valtype*}:
    `%|-%:%`(C, CALL_REF_instr(_IDX_typeuse(x)), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`} ++ [REF_valtype(?(NULL_NULL), _IDX_heaptype(x))]), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`}))))

  ;; 3-typing.watsup:676.1-680.47
  rule call_indirect{C : context, x : idx, y : idx, `t_1*` : valtype*, at : addrtype, `t_2*` : valtype*, lim : limits, rt : reftype}:
    `%|-%:%`(C, CALL_INDIRECT_instr(x, _IDX_typeuse(y)), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`} ++ [(at : addrtype <: valtype)]), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- if (C.TABLES_context[x!`%`_idx.0] = `%%%`_tabletype(at, lim, rt))
    -- Reftype_sub: `%|-%<:%`(C, rt, REF_reftype(?(NULL_NULL), FUNC_heaptype))
    -- Expand: `%~~%`(C.TYPES_context[y!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`}))))

  ;; 3-typing.watsup:682.1-685.42
  rule return{C : context, `t_1*` : valtype*, `t*` : valtype*, `t_2*` : valtype*}:
    `%|-%:%`(C, RETURN_instr, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`} ++ t*{t <- `t*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- if (C.RETURN_context = ?(`%`_resulttype(t*{t <- `t*`})))
    -- Instrtype_ok: `%|-%:OK`(C, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))

  ;; 3-typing.watsup:688.1-693.42
  rule return_call{C : context, x : idx, `t_3*` : valtype*, `t_1*` : valtype*, `t_4*` : valtype*, `t_2*` : valtype*, `t'_2*` : valtype*}:
    `%|-%:%`(C, RETURN_CALL_instr(x), `%->_%%`_instrtype(`%`_resulttype(t_3*{t_3 <- `t_3*`} ++ t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_4*{t_4 <- `t_4*`})))
    -- Expand: `%~~%`(C.FUNCS_context[x!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`}))))
    -- if (C.RETURN_context = ?(`%`_resulttype(t'_2*{t'_2 <- `t'_2*`})))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t_2*{t_2 <- `t_2*`}), `%`_resulttype(t'_2*{t'_2 <- `t'_2*`}))
    -- Instrtype_ok: `%|-%:OK`(C, `%->_%%`_instrtype(`%`_resulttype(t_3*{t_3 <- `t_3*`}), [], `%`_resulttype(t_4*{t_4 <- `t_4*`})))

  ;; 3-typing.watsup:696.1-701.42
  rule return_call_ref{C : context, x : idx, `t_3*` : valtype*, `t_1*` : valtype*, `t_4*` : valtype*, `t_2*` : valtype*, `t'_2*` : valtype*}:
    `%|-%:%`(C, RETURN_CALL_REF_instr(_IDX_typeuse(x)), `%->_%%`_instrtype(`%`_resulttype(t_3*{t_3 <- `t_3*`} ++ t_1*{t_1 <- `t_1*`} ++ [REF_valtype(?(NULL_NULL), _IDX_heaptype(x))]), [], `%`_resulttype(t_4*{t_4 <- `t_4*`})))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`}))))
    -- if (C.RETURN_context = ?(`%`_resulttype(t'_2*{t'_2 <- `t'_2*`})))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t_2*{t_2 <- `t_2*`}), `%`_resulttype(t'_2*{t'_2 <- `t'_2*`}))
    -- Instrtype_ok: `%|-%:OK`(C, `%->_%%`_instrtype(`%`_resulttype(t_3*{t_3 <- `t_3*`}), [], `%`_resulttype(t_4*{t_4 <- `t_4*`})))

  ;; 3-typing.watsup:704.1-712.42
  rule return_call_indirect{C : context, x : idx, y : idx, `t_3*` : valtype*, `t_1*` : valtype*, at : addrtype, `t_4*` : valtype*, lim : limits, rt : reftype, `t_2*` : valtype*, `t'_2*` : valtype*}:
    `%|-%:%`(C, RETURN_CALL_INDIRECT_instr(x, _IDX_typeuse(y)), `%->_%%`_instrtype(`%`_resulttype(t_3*{t_3 <- `t_3*`} ++ t_1*{t_1 <- `t_1*`} ++ [(at : addrtype <: valtype)]), [], `%`_resulttype(t_4*{t_4 <- `t_4*`})))
    -- if (C.TABLES_context[x!`%`_idx.0] = `%%%`_tabletype(at, lim, rt))
    -- Reftype_sub: `%|-%<:%`(C, rt, REF_reftype(?(NULL_NULL), FUNC_heaptype))
    -- Expand: `%~~%`(C.TYPES_context[y!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`}))))
    -- if (C.RETURN_context = ?(`%`_resulttype(t'_2*{t'_2 <- `t'_2*`})))
    -- Resulttype_sub: `%|-%<:%`(C, `%`_resulttype(t_2*{t_2 <- `t_2*`}), `%`_resulttype(t'_2*{t'_2 <- `t'_2*`}))
    -- Instrtype_ok: `%|-%:OK`(C, `%->_%%`_instrtype(`%`_resulttype(t_3*{t_3 <- `t_3*`}), [], `%`_resulttype(t_4*{t_4 <- `t_4*`})))

  ;; 3-typing.watsup:719.1-722.42
  rule throw{C : context, x : idx, `t_1*` : valtype*, `t*` : valtype*, `t_2*` : valtype*}:
    `%|-%:%`(C, THROW_instr(x), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`} ++ t*{t <- `t*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Expand: `%~~%`(C.TAGS_context[x!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t*{t <- `t*`}), `%`_resulttype([]))))
    -- Instrtype_ok: `%|-%:OK`(C, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))

  ;; 3-typing.watsup:724.1-726.42
  rule throw_ref{C : context, `t_1*` : valtype*, `t_2*` : valtype*}:
    `%|-%:%`(C, THROW_REF_instr, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`} ++ [REF_valtype(?(NULL_NULL), EXN_heaptype)]), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Instrtype_ok: `%|-%:OK`(C, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))

  ;; 3-typing.watsup:728.1-732.34
  rule try_table{C : context, bt : blocktype, `catch*` : catch*, `instr*` : instr*, `t_1*` : valtype*, `t_2*` : valtype*, `x*` : idx*}:
    `%|-%:%`(C, TRY_TABLE_instr(bt, `%`_list(catch*{catch <- `catch*`}), instr*{instr <- `instr*`}), `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Blocktype_ok: `%|-%:%`(C, bt, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Instrs_ok: `%|-%:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [`%`_resulttype(t_2*{t_2 <- `t_2*`})], RETURN ?(), REFS []} +++ C, instr*{instr <- `instr*`}, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), x*{x <- `x*`}, `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- (Catch_ok: `%|-%:OK`(C, catch))*{catch <- `catch*`}

  ;; 3-typing.watsup:755.1-756.33
  rule const{C : context, nt : numtype, c_nt : num_(nt)}:
    `%|-%:%`(C, CONST_instr(nt, c_nt), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([(nt : numtype <: valtype)])))

  ;; 3-typing.watsup:758.1-759.34
  rule unop{C : context, nt : numtype, unop_nt : unop_(nt)}:
    `%|-%:%`(C, UNOP_instr(nt, unop_nt), `%->_%%`_instrtype(`%`_resulttype([(nt : numtype <: valtype)]), [], `%`_resulttype([(nt : numtype <: valtype)])))

  ;; 3-typing.watsup:761.1-762.39
  rule binop{C : context, nt : numtype, binop_nt : binop_(nt)}:
    `%|-%:%`(C, BINOP_instr(nt, binop_nt), `%->_%%`_instrtype(`%`_resulttype([(nt : numtype <: valtype) (nt : numtype <: valtype)]), [], `%`_resulttype([(nt : numtype <: valtype)])))

  ;; 3-typing.watsup:764.1-765.39
  rule testop{C : context, nt : numtype, testop_nt : testop_(nt)}:
    `%|-%:%`(C, TESTOP_instr(nt, testop_nt), `%->_%%`_instrtype(`%`_resulttype([(nt : numtype <: valtype)]), [], `%`_resulttype([I32_valtype])))

  ;; 3-typing.watsup:767.1-768.40
  rule relop{C : context, nt : numtype, relop_nt : relop_(nt)}:
    `%|-%:%`(C, RELOP_instr(nt, relop_nt), `%->_%%`_instrtype(`%`_resulttype([(nt : numtype <: valtype) (nt : numtype <: valtype)]), [], `%`_resulttype([I32_valtype])))

  ;; 3-typing.watsup:770.1-771.44
  rule cvtop{C : context, nt_1 : numtype, nt_2 : numtype, cvtop : cvtop__(nt_2, nt_1)}:
    `%|-%:%`(C, CVTOP_instr(nt_1, nt_2, cvtop), `%->_%%`_instrtype(`%`_resulttype([(nt_2 : numtype <: valtype)]), [], `%`_resulttype([(nt_1 : numtype <: valtype)])))

  ;; 3-typing.watsup:776.1-778.31
  rule ref.null{C : context, ht : heaptype}:
    `%|-%:%`(C, REF.NULL_instr(ht), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([REF_valtype(?(NULL_NULL), ht)])))
    -- Heaptype_ok: `%|-%:OK`(C, ht)

  ;; 3-typing.watsup:780.1-783.20
  rule ref.func{C : context, x : idx, dt : deftype}:
    `%|-%:%`(C, REF.FUNC_instr(x), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([REF_valtype(?(), (dt : deftype <: heaptype))])))
    -- if (C.FUNCS_context[x!`%`_idx.0] = dt)
    -- if x <- C.REFS_context

  ;; 3-typing.watsup:785.1-786.34
  rule ref.i31{C : context}:
    `%|-%:%`(C, REF.I31_instr, `%->_%%`_instrtype(`%`_resulttype([I32_valtype]), [], `%`_resulttype([REF_valtype(?(), I31_heaptype)])))

  ;; 3-typing.watsup:788.1-790.31
  rule ref.is_null{C : context, ht : heaptype}:
    `%|-%:%`(C, REF.IS_NULL_instr, `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), ht)]), [], `%`_resulttype([I32_valtype])))
    -- Heaptype_ok: `%|-%:OK`(C, ht)

  ;; 3-typing.watsup:792.1-794.31
  rule ref.as_non_null{C : context, ht : heaptype}:
    `%|-%:%`(C, REF.AS_NON_NULL_instr, `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), ht)]), [], `%`_resulttype([REF_valtype(?(), ht)])))
    -- Heaptype_ok: `%|-%:OK`(C, ht)

  ;; 3-typing.watsup:796.1-797.51
  rule ref.eq{C : context}:
    `%|-%:%`(C, REF.EQ_instr, `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), EQ_heaptype) REF_valtype(?(NULL_NULL), EQ_heaptype)]), [], `%`_resulttype([I32_valtype])))

  ;; 3-typing.watsup:799.1-803.33
  rule ref.test{C : context, rt : reftype, rt' : reftype}:
    `%|-%:%`(C, REF.TEST_instr(rt), `%->_%%`_instrtype(`%`_resulttype([(rt' : reftype <: valtype)]), [], `%`_resulttype([I32_valtype])))
    -- Reftype_ok: `%|-%:OK`(C, rt)
    -- Reftype_ok: `%|-%:OK`(C, rt')
    -- Reftype_sub: `%|-%<:%`(C, rt, rt')

  ;; 3-typing.watsup:805.1-809.33
  rule ref.cast{C : context, rt : reftype, rt' : reftype}:
    `%|-%:%`(C, REF.CAST_instr(rt), `%->_%%`_instrtype(`%`_resulttype([(rt' : reftype <: valtype)]), [], `%`_resulttype([(rt : reftype <: valtype)])))
    -- Reftype_ok: `%|-%:OK`(C, rt)
    -- Reftype_ok: `%|-%:OK`(C, rt')
    -- Reftype_sub: `%|-%<:%`(C, rt, rt')

  ;; 3-typing.watsup:814.1-815.42
  rule i31.get{C : context, sx : sx}:
    `%|-%:%`(C, I31.GET_instr(sx), `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), I31_heaptype)]), [], `%`_resulttype([I32_valtype])))

  ;; 3-typing.watsup:820.1-822.44
  rule struct.new{C : context, x : idx, `zt*` : storagetype*, `mut*` : mut*}:
    `%|-%:%`(C, STRUCT.NEW_instr(x), `%->_%%`_instrtype(`%`_resulttype($unpack(zt)*{zt <- `zt*`}), [], `%`_resulttype([REF_valtype(?(), _IDX_heaptype(x))])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], STRUCT_comptype(`%`_structtype(`%%`_fieldtype(mut, zt)*{mut <- `mut*`, zt <- `zt*`})))

  ;; 3-typing.watsup:824.1-827.48
  rule struct.new_default{C : context, x : idx, `mut*` : mut*, `zt*` : storagetype*}:
    `%|-%:%`(C, STRUCT.NEW_DEFAULT_instr(x), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([REF_valtype(?(), _IDX_heaptype(x))])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], STRUCT_comptype(`%`_structtype(`%%`_fieldtype(mut, zt)*{mut <- `mut*`, zt <- `zt*`})))
    -- (Defaultable: `|-%DEFAULTABLE`($unpack(zt)))*{zt <- `zt*`}

  ;; 3-typing.watsup:829.1-833.39
  rule struct.get{C : context, `sx?` : sx?, x : idx, i : u32, zt : storagetype, `yt*` : fieldtype*, mut : mut}:
    `%|-%:%`(C, STRUCT.GET_instr(sx?{sx <- `sx?`}, x, i), `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), _IDX_heaptype(x))]), [], `%`_resulttype([$unpack(zt)])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], STRUCT_comptype(`%`_structtype(yt*{yt <- `yt*`})))
    -- if (yt*{yt <- `yt*`}[i!`%`_u32.0] = `%%`_fieldtype(mut, zt))
    -- if ((sx?{sx <- `sx?`} = ?()) <=> (zt = ($unpack(zt) : valtype <: storagetype)))

  ;; 3-typing.watsup:835.1-838.24
  rule struct.set{C : context, x : idx, i : u32, zt : storagetype, `yt*` : fieldtype*}:
    `%|-%:%`(C, STRUCT.SET_instr(x, i), `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), _IDX_heaptype(x)) $unpack(zt)]), [], `%`_resulttype([])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], STRUCT_comptype(`%`_structtype(yt*{yt <- `yt*`})))
    -- if (yt*{yt <- `yt*`}[i!`%`_u32.0] = `%%`_fieldtype(?(MUT_MUT), zt))

  ;; 3-typing.watsup:843.1-845.42
  rule array.new{C : context, x : idx, zt : storagetype, mut : mut}:
    `%|-%:%`(C, ARRAY.NEW_instr(x), `%->_%%`_instrtype(`%`_resulttype([$unpack(zt) I32_valtype]), [], `%`_resulttype([REF_valtype(?(), _IDX_heaptype(x))])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(mut, zt)))

  ;; 3-typing.watsup:847.1-850.45
  rule array.new_default{C : context, x : idx, mut : mut, zt : storagetype}:
    `%|-%:%`(C, ARRAY.NEW_DEFAULT_instr(x), `%->_%%`_instrtype(`%`_resulttype([I32_valtype]), [], `%`_resulttype([REF_valtype(?(), _IDX_heaptype(x))])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(mut, zt)))
    -- Defaultable: `|-%DEFAULTABLE`($unpack(zt))

  ;; 3-typing.watsup:852.1-854.42
  rule array.new_fixed{C : context, x : idx, n : n, zt : storagetype, mut : mut}:
    `%|-%:%`(C, ARRAY.NEW_FIXED_instr(x, `%`_u32(n)), `%->_%%`_instrtype(`%`_resulttype($unpack(zt)^n{}), [], `%`_resulttype([REF_valtype(?(), _IDX_heaptype(x))])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(mut, zt)))

  ;; 3-typing.watsup:856.1-859.40
  rule array.new_elem{C : context, x : idx, y : idx, mut : mut, rt : reftype}:
    `%|-%:%`(C, ARRAY.NEW_ELEM_instr(x, y), `%->_%%`_instrtype(`%`_resulttype([I32_valtype I32_valtype]), [], `%`_resulttype([REF_valtype(?(), _IDX_heaptype(x))])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(mut, (rt : reftype <: storagetype))))
    -- Reftype_sub: `%|-%<:%`(C, C.ELEMS_context[y!`%`_idx.0], rt)

  ;; 3-typing.watsup:861.1-865.24
  rule array.new_data{C : context, x : idx, y : idx, mut : mut, zt : storagetype, numtype : numtype, vectype : vectype}:
    `%|-%:%`(C, ARRAY.NEW_DATA_instr(x, y), `%->_%%`_instrtype(`%`_resulttype([I32_valtype I32_valtype]), [], `%`_resulttype([REF_valtype(?(), _IDX_heaptype(x))])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(mut, zt)))
    -- if (($unpack(zt) = (numtype : numtype <: valtype)) \/ ($unpack(zt) = (vectype : vectype <: valtype)))
    -- if (C.DATAS_context[y!`%`_idx.0] = OK_datatype)

  ;; 3-typing.watsup:867.1-870.39
  rule array.get{C : context, `sx?` : sx?, x : idx, zt : storagetype, mut : mut}:
    `%|-%:%`(C, ARRAY.GET_instr(sx?{sx <- `sx?`}, x), `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), _IDX_heaptype(x)) I32_valtype]), [], `%`_resulttype([$unpack(zt)])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(mut, zt)))
    -- if ((sx?{sx <- `sx?`} = ?()) <=> (zt = ($unpack(zt) : valtype <: storagetype)))

  ;; 3-typing.watsup:872.1-874.42
  rule array.set{C : context, x : idx, zt : storagetype}:
    `%|-%:%`(C, ARRAY.SET_instr(x), `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), _IDX_heaptype(x)) I32_valtype $unpack(zt)]), [], `%`_resulttype([])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(?(MUT_MUT), zt)))

  ;; 3-typing.watsup:876.1-877.43
  rule array.len{C : context}:
    `%|-%:%`(C, ARRAY.LEN_instr, `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), ARRAY_heaptype)]), [], `%`_resulttype([I32_valtype])))

  ;; 3-typing.watsup:879.1-881.42
  rule array.fill{C : context, x : idx, zt : storagetype}:
    `%|-%:%`(C, ARRAY.FILL_instr(x), `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), _IDX_heaptype(x)) I32_valtype $unpack(zt) I32_valtype]), [], `%`_resulttype([])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(?(MUT_MUT), zt)))

  ;; 3-typing.watsup:883.1-887.40
  rule array.copy{C : context, x_1 : idx, x_2 : idx, zt_1 : storagetype, mut : mut, zt_2 : storagetype}:
    `%|-%:%`(C, ARRAY.COPY_instr(x_1, x_2), `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), _IDX_heaptype(x_1)) I32_valtype REF_valtype(?(NULL_NULL), _IDX_heaptype(x_2)) I32_valtype I32_valtype]), [], `%`_resulttype([])))
    -- Expand: `%~~%`(C.TYPES_context[x_1!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(?(MUT_MUT), zt_1)))
    -- Expand: `%~~%`(C.TYPES_context[x_2!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(mut, zt_2)))
    -- Storagetype_sub: `%|-%<:%`(C, zt_2, zt_1)

  ;; 3-typing.watsup:889.1-892.44
  rule array.init_elem{C : context, x : idx, y : idx, zt : storagetype}:
    `%|-%:%`(C, ARRAY.INIT_ELEM_instr(x, y), `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), _IDX_heaptype(x)) I32_valtype I32_valtype I32_valtype]), [], `%`_resulttype([])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(?(MUT_MUT), zt)))
    -- Storagetype_sub: `%|-%<:%`(C, (C.ELEMS_context[y!`%`_idx.0] : reftype <: storagetype), zt)

  ;; 3-typing.watsup:894.1-898.24
  rule array.init_data{C : context, x : idx, y : idx, zt : storagetype, numtype : numtype, vectype : vectype}:
    `%|-%:%`(C, ARRAY.INIT_DATA_instr(x, y), `%->_%%`_instrtype(`%`_resulttype([REF_valtype(?(NULL_NULL), _IDX_heaptype(x)) I32_valtype I32_valtype I32_valtype]), [], `%`_resulttype([])))
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], ARRAY_comptype(`%%`_arraytype(?(MUT_MUT), zt)))
    -- if (($unpack(zt) = (numtype : numtype <: valtype)) \/ ($unpack(zt) = (vectype : vectype <: valtype)))
    -- if (C.DATAS_context[y!`%`_idx.0] = OK_datatype)

  ;; 3-typing.watsup:903.1-905.20
  rule extern.convert_any{C : context, nul1 : nul1, nul2 : nul2}:
    `%|-%:%`(C, EXTERN.CONVERT_ANY_instr, `%->_%%`_instrtype(`%`_resulttype([REF_valtype(nul1, ANY_heaptype)]), [], `%`_resulttype([REF_valtype(nul2, EXTERN_heaptype)])))
    -- if (nul1 = nul2)

  ;; 3-typing.watsup:907.1-909.20
  rule any.convert_extern{C : context, nul1 : nul1, nul2 : nul2}:
    `%|-%:%`(C, ANY.CONVERT_EXTERN_instr, `%->_%%`_instrtype(`%`_resulttype([REF_valtype(nul1, EXTERN_heaptype)]), [], `%`_resulttype([REF_valtype(nul2, ANY_heaptype)])))
    -- if (nul1 = nul2)

  ;; 3-typing.watsup:914.1-915.35
  rule vconst{C : context, c : vec_(V128_Vnn)}:
    `%|-%:%`(C, VCONST_instr(V128_vectype, c), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:917.1-918.41
  rule vvunop{C : context, vvunop : vvunop}:
    `%|-%:%`(C, VVUNOP_instr(V128_vectype, vvunop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:920.1-921.48
  rule vvbinop{C : context, vvbinop : vvbinop}:
    `%|-%:%`(C, VVBINOP_instr(V128_vectype, vvbinop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:923.1-924.55
  rule vvternop{C : context, vvternop : vvternop}:
    `%|-%:%`(C, VVTERNOP_instr(V128_vectype, vvternop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype V128_valtype V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:926.1-927.44
  rule vvtestop{C : context, vvtestop : vvtestop}:
    `%|-%:%`(C, VVTESTOP_instr(V128_vectype, vvtestop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype]), [], `%`_resulttype([I32_valtype])))

  ;; 3-typing.watsup:929.1-930.37
  rule vunop{C : context, sh : shape, vunop : vunop_(sh)}:
    `%|-%:%`(C, VUNOP_instr(sh, vunop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:932.1-933.44
  rule vbinop{C : context, sh : shape, vbinop : vbinop_(sh)}:
    `%|-%:%`(C, VBINOP_instr(sh, vbinop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:935.1-936.51
  rule vternop{C : context, sh : shape, vternop : vternop_(sh)}:
    `%|-%:%`(C, VTERNOP_instr(sh, vternop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype V128_valtype V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:938.1-939.40
  rule vtestop{C : context, sh : shape, vtestop : vtestop_(sh)}:
    `%|-%:%`(C, VTESTOP_instr(sh, vtestop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype]), [], `%`_resulttype([I32_valtype])))

  ;; 3-typing.watsup:941.1-942.44
  rule vrelop{C : context, sh : shape, vrelop : vrelop_(sh)}:
    `%|-%:%`(C, VRELOP_instr(sh, vrelop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:944.1-945.47
  rule vshiftop{C : context, sh : ishape, vshiftop : vshiftop_(sh)}:
    `%|-%:%`(C, VSHIFTOP_instr(sh, vshiftop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype I32_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:947.1-948.33
  rule vbitmask{C : context, sh : ishape}:
    `%|-%:%`(C, VBITMASK_instr(sh), `%->_%%`_instrtype(`%`_resulttype([V128_valtype]), [], `%`_resulttype([I32_valtype])))

  ;; 3-typing.watsup:950.1-951.50
  rule vswizzlop{C : context, sh : bshape, vswizzlop : vswizzlop_(sh)}:
    `%|-%:%`(C, VSWIZZLOP_instr(sh, vswizzlop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:953.1-955.29
  rule vshuffle{C : context, sh : bshape, `i*` : laneidx*}:
    `%|-%:%`(C, VSHUFFLE_instr(sh, i*{i <- `i*`}), `%->_%%`_instrtype(`%`_resulttype([V128_valtype V128_valtype]), [], `%`_resulttype([V128_valtype])))
    -- (if (i!`%`_laneidx.0 < (2 * $dim(sh!`%`_bshape.0)!`%`_dim.0)))*{i <- `i*`}

  ;; 3-typing.watsup:957.1-958.44
  rule vsplat{C : context, sh : shape}:
    `%|-%:%`(C, VSPLAT_instr(sh), `%->_%%`_instrtype(`%`_resulttype([($unpackshape(sh) : numtype <: valtype)]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:960.1-962.21
  rule vextract_lane{C : context, sh : shape, `sx?` : sx?, i : laneidx}:
    `%|-%:%`(C, VEXTRACT_LANE_instr(sh, sx?{sx <- `sx?`}, i), `%->_%%`_instrtype(`%`_resulttype([V128_valtype]), [], `%`_resulttype([($unpackshape(sh) : numtype <: valtype)])))
    -- if (i!`%`_laneidx.0 < $dim(sh)!`%`_dim.0)

  ;; 3-typing.watsup:964.1-966.21
  rule vreplace_lane{C : context, sh : shape, i : laneidx}:
    `%|-%:%`(C, VREPLACE_LANE_instr(sh, i), `%->_%%`_instrtype(`%`_resulttype([V128_valtype ($unpackshape(sh) : numtype <: valtype)]), [], `%`_resulttype([V128_valtype])))
    -- if (i!`%`_laneidx.0 < $dim(sh)!`%`_dim.0)

  ;; 3-typing.watsup:968.1-969.50
  rule vextunop{C : context, sh_1 : ishape, sh_2 : ishape, vextunop : vextunop__(sh_2, sh_1)}:
    `%|-%:%`(C, VEXTUNOP_instr(sh_1, sh_2, vextunop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:971.1-972.57
  rule vextbinop{C : context, sh_1 : ishape, sh_2 : ishape, vextbinop : vextbinop__(sh_2, sh_1)}:
    `%|-%:%`(C, VEXTBINOP_instr(sh_1, sh_2, vextbinop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:974.1-975.64
  rule vextternop{C : context, sh_1 : ishape, sh_2 : ishape, vextternop : vextternop__(sh_2, sh_1)}:
    `%|-%:%`(C, VEXTTERNOP_instr(sh_1, sh_2, vextternop), `%->_%%`_instrtype(`%`_resulttype([V128_valtype V128_valtype V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:977.1-978.48
  rule vnarrow{C : context, sh_1 : ishape, sh_2 : ishape, sx : sx}:
    `%|-%:%`(C, VNARROW_instr(sh_1, sh_2, sx), `%->_%%`_instrtype(`%`_resulttype([V128_valtype V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:980.1-981.58
  rule vcvtop{C : context, sh_1 : shape, sh_2 : shape, vcvtop : vcvtop__(sh_2, sh_1), `half?` : half__(sh_2, sh_1)?, `zero?` : zero__(sh_2, sh_1)?}:
    `%|-%:%`(C, VCVTOP_instr(sh_1, sh_2, vcvtop, half?{half <- `half?`}, zero?{zero <- `zero?`}), `%->_%%`_instrtype(`%`_resulttype([V128_valtype]), [], `%`_resulttype([V128_valtype])))

  ;; 3-typing.watsup:986.1-988.28
  rule local.get{C : context, x : idx, t : valtype}:
    `%|-%:%`(C, LOCAL.GET_instr(x), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([t])))
    -- if (C.LOCALS_context[x!`%`_idx.0] = `%%`_localtype(SET_init, t))

  ;; 3-typing.watsup:990.1-992.29
  rule local.set{C : context, x : idx, t : valtype, init : init}:
    `%|-%:%`(C, LOCAL.SET_instr(x), `%->_%%`_instrtype(`%`_resulttype([t]), [x], `%`_resulttype([])))
    -- if (C.LOCALS_context[x!`%`_idx.0] = `%%`_localtype(init, t))

  ;; 3-typing.watsup:994.1-996.29
  rule local.tee{C : context, x : idx, t : valtype, init : init}:
    `%|-%:%`(C, LOCAL.TEE_instr(x), `%->_%%`_instrtype(`%`_resulttype([t]), [x], `%`_resulttype([t])))
    -- if (C.LOCALS_context[x!`%`_idx.0] = `%%`_localtype(init, t))

  ;; 3-typing.watsup:1001.1-1003.29
  rule global.get{C : context, x : idx, t : valtype, mut : mut}:
    `%|-%:%`(C, GLOBAL.GET_instr(x), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([t])))
    -- if (C.GLOBALS_context[x!`%`_idx.0] = `%%`_globaltype(mut, t))

  ;; 3-typing.watsup:1005.1-1007.29
  rule global.set{C : context, x : idx, t : valtype}:
    `%|-%:%`(C, GLOBAL.SET_instr(x), `%->_%%`_instrtype(`%`_resulttype([t]), [], `%`_resulttype([])))
    -- if (C.GLOBALS_context[x!`%`_idx.0] = `%%`_globaltype(?(MUT_MUT), t))

  ;; 3-typing.watsup:1012.1-1014.32
  rule table.get{C : context, x : idx, at : addrtype, rt : reftype, lim : limits}:
    `%|-%:%`(C, TABLE.GET_instr(x), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype)]), [], `%`_resulttype([(rt : reftype <: valtype)])))
    -- if (C.TABLES_context[x!`%`_idx.0] = `%%%`_tabletype(at, lim, rt))

  ;; 3-typing.watsup:1016.1-1018.32
  rule table.set{C : context, x : idx, at : addrtype, rt : reftype, lim : limits}:
    `%|-%:%`(C, TABLE.SET_instr(x), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype) (rt : reftype <: valtype)]), [], `%`_resulttype([])))
    -- if (C.TABLES_context[x!`%`_idx.0] = `%%%`_tabletype(at, lim, rt))

  ;; 3-typing.watsup:1020.1-1022.32
  rule table.size{C : context, x : idx, at : addrtype, lim : limits, rt : reftype}:
    `%|-%:%`(C, TABLE.SIZE_instr(x), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([(at : addrtype <: valtype)])))
    -- if (C.TABLES_context[x!`%`_idx.0] = `%%%`_tabletype(at, lim, rt))

  ;; 3-typing.watsup:1024.1-1026.32
  rule table.grow{C : context, x : idx, rt : reftype, at : addrtype, lim : limits}:
    `%|-%:%`(C, TABLE.GROW_instr(x), `%->_%%`_instrtype(`%`_resulttype([(rt : reftype <: valtype) (at : addrtype <: valtype)]), [], `%`_resulttype([(at : addrtype <: valtype)])))
    -- if (C.TABLES_context[x!`%`_idx.0] = `%%%`_tabletype(at, lim, rt))

  ;; 3-typing.watsup:1028.1-1030.32
  rule table.fill{C : context, x : idx, at : addrtype, rt : reftype, lim : limits}:
    `%|-%:%`(C, TABLE.FILL_instr(x), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype) (rt : reftype <: valtype) (at : addrtype <: valtype)]), [], `%`_resulttype([])))
    -- if (C.TABLES_context[x!`%`_idx.0] = `%%%`_tabletype(at, lim, rt))

  ;; 3-typing.watsup:1032.1-1036.36
  rule table.copy{C : context, x_1 : idx, x_2 : idx, at_1 : addrtype, at_2 : addrtype, lim_1 : limits, rt_1 : reftype, lim_2 : limits, rt_2 : reftype}:
    `%|-%:%`(C, TABLE.COPY_instr(x_1, x_2), `%->_%%`_instrtype(`%`_resulttype([(at_1 : addrtype <: valtype) (at_2 : addrtype <: valtype) ($minat(at_1, at_2) : addrtype <: valtype)]), [], `%`_resulttype([])))
    -- if (C.TABLES_context[x_1!`%`_idx.0] = `%%%`_tabletype(at_1, lim_1, rt_1))
    -- if (C.TABLES_context[x_2!`%`_idx.0] = `%%%`_tabletype(at_2, lim_2, rt_2))
    -- Reftype_sub: `%|-%<:%`(C, rt_2, rt_1)

  ;; 3-typing.watsup:1038.1-1042.36
  rule table.init{C : context, x : idx, y : idx, at : addrtype, lim : limits, rt_1 : reftype, rt_2 : reftype}:
    `%|-%:%`(C, TABLE.INIT_instr(x, y), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype) I32_valtype I32_valtype]), [], `%`_resulttype([])))
    -- if (C.TABLES_context[x!`%`_idx.0] = `%%%`_tabletype(at, lim, rt_1))
    -- if (C.ELEMS_context[y!`%`_idx.0] = rt_2)
    -- Reftype_sub: `%|-%<:%`(C, rt_2, rt_1)

  ;; 3-typing.watsup:1044.1-1046.24
  rule elem.drop{C : context, x : idx, rt : reftype}:
    `%|-%:%`(C, ELEM.DROP_instr(x), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([])))
    -- if (C.ELEMS_context[x!`%`_idx.0] = rt)

  ;; 3-typing.watsup:1051.1-1053.32
  rule memory.size{C : context, x : idx, at : addrtype, lim : limits}:
    `%|-%:%`(C, MEMORY.SIZE_instr(x), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([(at : addrtype <: valtype)])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))

  ;; 3-typing.watsup:1055.1-1057.32
  rule memory.grow{C : context, x : idx, at : addrtype, lim : limits}:
    `%|-%:%`(C, MEMORY.GROW_instr(x), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype)]), [], `%`_resulttype([(at : addrtype <: valtype)])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))

  ;; 3-typing.watsup:1059.1-1061.32
  rule memory.fill{C : context, x : idx, at : addrtype, lim : limits}:
    `%|-%:%`(C, MEMORY.FILL_instr(x), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype) I32_valtype (at : addrtype <: valtype)]), [], `%`_resulttype([])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))

  ;; 3-typing.watsup:1063.1-1066.38
  rule memory.copy{C : context, x_1 : idx, x_2 : idx, at_1 : addrtype, at_2 : addrtype, lim_1 : limits, lim_2 : limits}:
    `%|-%:%`(C, MEMORY.COPY_instr(x_1, x_2), `%->_%%`_instrtype(`%`_resulttype([(at_1 : addrtype <: valtype) (at_2 : addrtype <: valtype) ($minat(at_1, at_2) : addrtype <: valtype)]), [], `%`_resulttype([])))
    -- if (C.MEMS_context[x_1!`%`_idx.0] = `%%PAGE`_memtype(at_1, lim_1))
    -- if (C.MEMS_context[x_2!`%`_idx.0] = `%%PAGE`_memtype(at_2, lim_2))

  ;; 3-typing.watsup:1068.1-1071.24
  rule memory.init{C : context, x : idx, y : idx, at : addrtype, lim : limits}:
    `%|-%:%`(C, MEMORY.INIT_instr(x, y), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype) I32_valtype I32_valtype]), [], `%`_resulttype([])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (C.DATAS_context[y!`%`_idx.0] = OK_datatype)

  ;; 3-typing.watsup:1073.1-1075.24
  rule data.drop{C : context, x : idx}:
    `%|-%:%`(C, DATA.DROP_instr(x), `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([])))
    -- if (C.DATAS_context[x!`%`_idx.0] = OK_datatype)

  ;; 3-typing.watsup:1086.1-1089.43
  rule `load-val`{C : context, nt : numtype, x : idx, memarg : memarg, at : addrtype, lim : limits}:
    `%|-%:%`(C, LOAD_instr(nt, ?(), x, memarg), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype)]), [], `%`_resulttype([(nt : numtype <: valtype)])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= (($size(nt) : nat <:> rat) / (8 : nat <:> rat)))

  ;; 3-typing.watsup:1091.1-1094.35
  rule `load-pack`{C : context, Inn : Inn, M : M, sx : sx, x : idx, memarg : memarg, at : addrtype, lim : limits}:
    `%|-%:%`(C, LOAD_instr((Inn : Inn <: numtype), ?(`%_%`_loadop_(`%`_sz(M), sx)), x, memarg), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype)]), [], `%`_resulttype([(Inn : Inn <: valtype)])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= ((M : nat <:> rat) / (8 : nat <:> rat)))

  ;; 3-typing.watsup:1105.1-1108.43
  rule `store-val`{C : context, nt : numtype, x : idx, memarg : memarg, at : addrtype, lim : limits}:
    `%|-%:%`(C, STORE_instr(nt, ?(), x, memarg), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype) (nt : numtype <: valtype)]), [], `%`_resulttype([])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= (($size(nt) : nat <:> rat) / (8 : nat <:> rat)))

  ;; 3-typing.watsup:1110.1-1113.35
  rule `store-pack`{C : context, Inn : Inn, M : M, x : idx, memarg : memarg, at : addrtype, lim : limits}:
    `%|-%:%`(C, STORE_instr((Inn : Inn <: numtype), ?(`%`_storeop_(`%`_sz(M))), x, memarg), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype) (Inn : Inn <: valtype)]), [], `%`_resulttype([])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= ((M : nat <:> rat) / (8 : nat <:> rat)))

  ;; 3-typing.watsup:1115.1-1118.46
  rule `vload-val`{C : context, x : idx, memarg : memarg, at : addrtype, lim : limits}:
    `%|-%:%`(C, VLOAD_instr(V128_vectype, ?(), x, memarg), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype)]), [], `%`_resulttype([V128_valtype])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= (($vsize(V128_vectype) : nat <:> rat) / (8 : nat <:> rat)))

  ;; 3-typing.watsup:1120.1-1123.39
  rule `vload-pack`{C : context, M : M, N : N, sx : sx, x : idx, memarg : memarg, at : addrtype, lim : limits}:
    `%|-%:%`(C, VLOAD_instr(V128_vectype, ?(`SHAPE%X%_%`_vloadop_(`%`_sz(M), N, sx)), x, memarg), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype)]), [], `%`_resulttype([V128_valtype])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= (((M : nat <:> rat) / (8 : nat <:> rat)) * (N : nat <:> rat)))

  ;; 3-typing.watsup:1125.1-1128.35
  rule `vload-splat`{C : context, N : N, x : idx, memarg : memarg, at : addrtype, lim : limits}:
    `%|-%:%`(C, VLOAD_instr(V128_vectype, ?(SPLAT_vloadop_(`%`_sz(N))), x, memarg), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype)]), [], `%`_resulttype([V128_valtype])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= ((N : nat <:> rat) / (8 : nat <:> rat)))

  ;; 3-typing.watsup:1130.1-1133.35
  rule `vload-zero`{C : context, N : N, x : idx, memarg : memarg, at : addrtype, lim : limits}:
    `%|-%:%`(C, VLOAD_instr(V128_vectype, ?(ZERO_vloadop_(`%`_sz(N))), x, memarg), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype)]), [], `%`_resulttype([V128_valtype])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= ((N : nat <:> rat) / (8 : nat <:> rat)))

  ;; 3-typing.watsup:1135.1-1139.21
  rule vload_lane{C : context, N : N, x : idx, memarg : memarg, i : laneidx, at : addrtype, lim : limits}:
    `%|-%:%`(C, VLOAD_LANE_instr(V128_vectype, `%`_sz(N), x, memarg, i), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype) V128_valtype]), [], `%`_resulttype([V128_valtype])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= ((N : nat <:> rat) / (8 : nat <:> rat)))
    -- if ((i!`%`_laneidx.0 : nat <:> rat) < ((128 : nat <:> rat) / (N : nat <:> rat)))

  ;; 3-typing.watsup:1141.1-1144.46
  rule vstore{C : context, x : idx, memarg : memarg, at : addrtype, lim : limits}:
    `%|-%:%`(C, VSTORE_instr(V128_vectype, x, memarg), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype) V128_valtype]), [], `%`_resulttype([])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= (($vsize(V128_vectype) : nat <:> rat) / (8 : nat <:> rat)))

  ;; 3-typing.watsup:1146.1-1150.21
  rule vstore_lane{C : context, N : N, x : idx, memarg : memarg, i : laneidx, at : addrtype, lim : limits}:
    `%|-%:%`(C, VSTORE_LANE_instr(V128_vectype, `%`_sz(N), x, memarg, i), `%->_%%`_instrtype(`%`_resulttype([(at : addrtype <: valtype) V128_valtype]), [], `%`_resulttype([])))
    -- if (C.MEMS_context[x!`%`_idx.0] = `%%PAGE`_memtype(at, lim))
    -- if (((2 ^ memarg.ALIGN_memarg!`%`_u32.0) : nat <:> rat) <= ((N : nat <:> rat) / (8 : nat <:> rat)))
    -- if ((i!`%`_laneidx.0 : nat <:> rat) < ((128 : nat <:> rat) / (N : nat <:> rat)))

;; 3-typing.watsup:558.1-558.96
relation Instrs_ok: `%|-%:%`(context, instr*, instrtype)
  ;; 3-typing.watsup:1155.1-1156.24
  rule empty{C : context}:
    `%|-%:%`(C, [], `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype([])))

  ;; 3-typing.watsup:1159.1-1163.82
  rule seq{C : context, instr_1 : instr, `instr_2*` : instr*, `t_1*` : valtype*, `x_1*` : idx*, `x_2*` : idx*, `t_3*` : valtype*, `t_2*` : valtype*, `init*` : init*, `t*` : valtype*}:
    `%|-%:%`(C, [instr_1] ++ instr_2*{instr_2 <- `instr_2*`}, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), x_1*{x_1 <- `x_1*`} ++ x_2*{x_2 <- `x_2*`}, `%`_resulttype(t_3*{t_3 <- `t_3*`})))
    -- Instr_ok: `%|-%:%`(C, instr_1, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), x_1*{x_1 <- `x_1*`}, `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- (if (C.LOCALS_context[x_1!`%`_idx.0] = `%%`_localtype(init, t)))*{init <- `init*`, t <- `t*`, x_1 <- `x_1*`}
    -- Instrs_ok: `%|-%:%`($with_locals(C, x_1*{x_1 <- `x_1*`}, `%%`_localtype(SET_init, t)*{t <- `t*`}), instr_2*{instr_2 <- `instr_2*`}, `%->_%%`_instrtype(`%`_resulttype(t_2*{t_2 <- `t_2*`}), x_2*{x_2 <- `x_2*`}, `%`_resulttype(t_3*{t_3 <- `t_3*`})))

  ;; 3-typing.watsup:1165.1-1169.33
  rule sub{C : context, `instr*` : instr*, it' : instrtype, it : instrtype}:
    `%|-%:%`(C, instr*{instr <- `instr*`}, it')
    -- Instrs_ok: `%|-%:%`(C, instr*{instr <- `instr*`}, it)
    -- Instrtype_sub: `%|-%<:%`(C, it, it')
    -- Instrtype_ok: `%|-%:OK`(C, it')

  ;; 3-typing.watsup:1172.1-1175.33
  rule frame{C : context, `instr*` : instr*, `t*` : valtype*, `t_1*` : valtype*, `x*` : idx*, `t_2*` : valtype*}:
    `%|-%:%`(C, instr*{instr <- `instr*`}, `%->_%%`_instrtype(`%`_resulttype(t*{t <- `t*`} ++ t_1*{t_1 <- `t_1*`}), x*{x <- `x*`}, `%`_resulttype(t*{t <- `t*`} ++ t_2*{t_2 <- `t_2*`})))
    -- Instrs_ok: `%|-%:%`(C, instr*{instr <- `instr*`}, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), x*{x <- `x*`}, `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Resulttype_ok: `%|-%:OK`(C, `%`_resulttype(t*{t <- `t*`}))
}

;; 3-typing.watsup
relation Expr_ok: `%|-%:%`(context, expr, resulttype)
  ;; 3-typing.watsup
  rule _{C : context, `instr*` : instr*, `t*` : valtype*}:
    `%|-%:%`(C, instr*{instr <- `instr*`}, `%`_resulttype(t*{t <- `t*`}))
    -- Instrs_ok: `%|-%:%`(C, instr*{instr <- `instr*`}, `%->_%%`_instrtype(`%`_resulttype([]), [], `%`_resulttype(t*{t <- `t*`})))

;; 3-typing.watsup
relation Nondefaultable: `|-%NONDEFAULTABLE`(valtype)
  ;; 6-runtime-aux.watsup
  rule _{t : valtype}:
    `|-%NONDEFAULTABLE`(t)
    -- if ($default_(t) = ?())

;; 3-typing.watsup
relation Instr_const: `%|-%CONST`(context, instr)
  ;; 3-typing.watsup
  rule const{C : context, nt : numtype, c_nt : num_(nt)}:
    `%|-%CONST`(C, CONST_instr(nt, c_nt))

  ;; 3-typing.watsup
  rule vconst{C : context, vt : vectype, c_vt : vec_(vt)}:
    `%|-%CONST`(C, VCONST_instr(vt, c_vt))

  ;; 3-typing.watsup
  rule ref.null{C : context, ht : heaptype}:
    `%|-%CONST`(C, REF.NULL_instr(ht))

  ;; 3-typing.watsup
  rule ref.i31{C : context}:
    `%|-%CONST`(C, REF.I31_instr)

  ;; 3-typing.watsup
  rule ref.func{C : context, x : idx}:
    `%|-%CONST`(C, REF.FUNC_instr(x))

  ;; 3-typing.watsup
  rule struct.new{C : context, x : idx}:
    `%|-%CONST`(C, STRUCT.NEW_instr(x))

  ;; 3-typing.watsup
  rule struct.new_default{C : context, x : idx}:
    `%|-%CONST`(C, STRUCT.NEW_DEFAULT_instr(x))

  ;; 3-typing.watsup
  rule array.new{C : context, x : idx}:
    `%|-%CONST`(C, ARRAY.NEW_instr(x))

  ;; 3-typing.watsup
  rule array.new_default{C : context, x : idx}:
    `%|-%CONST`(C, ARRAY.NEW_DEFAULT_instr(x))

  ;; 3-typing.watsup
  rule array.new_fixed{C : context, x : idx, n : n}:
    `%|-%CONST`(C, ARRAY.NEW_FIXED_instr(x, `%`_u32(n)))

  ;; 3-typing.watsup
  rule any.convert_extern{C : context}:
    `%|-%CONST`(C, ANY.CONVERT_EXTERN_instr)

  ;; 3-typing.watsup
  rule extern.convert_any{C : context}:
    `%|-%CONST`(C, EXTERN.CONVERT_ANY_instr)

  ;; 3-typing.watsup
  rule global.get{C : context, x : idx, t : valtype}:
    `%|-%CONST`(C, GLOBAL.GET_instr(x))
    -- if (C.GLOBALS_context[x!`%`_idx.0] = `%%`_globaltype(?(), t))

  ;; 3-typing.watsup
  rule binop{C : context, Inn : Inn, binop : binop_((Inn : Inn <: numtype))}:
    `%|-%CONST`(C, BINOP_instr((Inn : Inn <: numtype), binop))
    -- if Inn <- [I32_Inn I64_Inn]
    -- if binop <- [ADD_binop_ SUB_binop_ MUL_binop_]

;; 3-typing.watsup
relation Expr_const: `%|-%CONST`(context, expr)
  ;; 3-typing.watsup
  rule _{C : context, `instr*` : instr*}:
    `%|-%CONST`(C, instr*{instr <- `instr*`})
    -- (Instr_const: `%|-%CONST`(C, instr))*{instr <- `instr*`}

;; 3-typing.watsup
relation Expr_ok_const: `%|-%:%CONST`(context, expr, valtype)
  ;; 3-typing.watsup
  rule _{C : context, expr : expr, t : valtype}:
    `%|-%:%CONST`(C, expr, t)
    -- Expr_ok: `%|-%:%`(C, expr, `%`_resulttype([t]))
    -- Expr_const: `%|-%CONST`(C, expr)

;; 3-typing.watsup
relation Type_ok: `%|-%:%`(context, type, deftype*)
  ;; 3-typing.watsup
  rule _{C : context, rectype : rectype, `dt*` : deftype*, x : idx}:
    `%|-%:%`(C, TYPE_type(rectype), dt*{dt <- `dt*`})
    -- if (x!`%`_idx.0 = |C.TYPES_context|)
    -- if (dt*{dt <- `dt*`} = $rolldt(x, rectype))
    -- Rectype_ok: `%|-%:%`(C +++ {TYPES dt*{dt <- `dt*`}, RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, rectype, OK_oktypeidx(x))

;; 3-typing.watsup
relation Local_ok: `%|-%:%`(context, local, localtype)
  ;; 3-typing.watsup
  rule set{C : context, t : valtype}:
    `%|-%:%`(C, LOCAL_local(t), `%%`_localtype(SET_init, t))
    -- Defaultable: `|-%DEFAULTABLE`(t)

  ;; 3-typing.watsup
  rule unset{C : context, t : valtype}:
    `%|-%:%`(C, LOCAL_local(t), `%%`_localtype(UNSET_init, t))
    -- Nondefaultable: `|-%NONDEFAULTABLE`(t)

;; 3-typing.watsup
relation Func_ok: `%|-%:%`(context, func, deftype)
  ;; 3-typing.watsup
  rule _{C : context, x : idx, `local*` : local*, expr : expr, `t_1*` : valtype*, `t_2*` : valtype*, `lct*` : localtype*}:
    `%|-%:%`(C, FUNC_func(x, local*{local <- `local*`}, expr), C.TYPES_context[x!`%`_idx.0])
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`}))))
    -- (Local_ok: `%|-%:%`(C, local, lct))*{lct <- `lct*`, local <- `local*`}
    -- Expr_ok: `%|-%:%`(C +++ {TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS `%%`_localtype(SET_init, t_1)*{t_1 <- `t_1*`} ++ lct*{lct <- `lct*`}, LABELS [`%`_resulttype(t_2*{t_2 <- `t_2*`})], RETURN ?(`%`_resulttype(t_2*{t_2 <- `t_2*`})), REFS []}, expr, `%`_resulttype(t_2*{t_2 <- `t_2*`}))

;; 3-typing.watsup
relation Global_ok: `%|-%:%`(context, global, globaltype)
  ;; 3-typing.watsup
  rule _{C : context, globaltype : globaltype, expr : expr, gt : globaltype, mut : mut, t : valtype}:
    `%|-%:%`(C, GLOBAL_global(globaltype, expr), globaltype)
    -- Globaltype_ok: `%|-%:OK`(C, gt)
    -- if (globaltype = `%%`_globaltype(mut, t))
    -- Expr_ok_const: `%|-%:%CONST`(C, expr, t)

;; 3-typing.watsup
relation Table_ok: `%|-%:%`(context, table, tabletype)
  ;; 3-typing.watsup
  rule _{C : context, tabletype : tabletype, expr : expr, at : addrtype, lim : limits, rt : reftype}:
    `%|-%:%`(C, TABLE_table(tabletype, expr), tabletype)
    -- Tabletype_ok: `%|-%:OK`(C, tabletype)
    -- if (tabletype = `%%%`_tabletype(at, lim, rt))
    -- Expr_ok_const: `%|-%:%CONST`(C, expr, (rt : reftype <: valtype))

;; 3-typing.watsup
relation Mem_ok: `%|-%:%`(context, mem, memtype)
  ;; 3-typing.watsup
  rule _{C : context, memtype : memtype}:
    `%|-%:%`(C, MEMORY_mem(memtype), memtype)
    -- Memtype_ok: `%|-%:OK`(C, memtype)

;; 3-typing.watsup
relation Tag_ok: `%|-%:%`(context, tag, tagtype)
  ;; 3-typing.watsup
  rule _{C : context, x : idx, functype : functype}:
    `%|-%:%`(C, TAG_tag(x), C.TYPES_context[x!`%`_idx.0])
    -- Expand: `%~~%`(C.TYPES_context[x!`%`_idx.0], FUNC_comptype(functype))

;; 3-typing.watsup
relation Elemmode_ok: `%|-%:%`(context, elemmode, elemtype)
  ;; 3-typing.watsup
  rule active{C : context, x : idx, expr : expr, rt : reftype, at : addrtype, lim : limits, rt' : reftype}:
    `%|-%:%`(C, ACTIVE_elemmode(x, expr), rt)
    -- if (C.TABLES_context[x!`%`_idx.0] = `%%%`_tabletype(at, lim, rt'))
    -- Reftype_sub: `%|-%<:%`(C, rt, rt')
    -- Expr_ok_const: `%|-%:%CONST`(C, expr, I32_valtype)

  ;; 3-typing.watsup
  rule passive{C : context, rt : reftype}:
    `%|-%:%`(C, PASSIVE_elemmode, rt)

  ;; 3-typing.watsup
  rule declare{C : context, rt : reftype}:
    `%|-%:%`(C, DECLARE_elemmode, rt)

;; 3-typing.watsup
relation Elem_ok: `%|-%:%`(context, elem, elemtype)
  ;; 3-typing.watsup
  rule _{C : context, elemtype : elemtype, `expr*` : expr*, elemmode : elemmode}:
    `%|-%:%`(C, ELEM_elem(elemtype, expr*{expr <- `expr*`}, elemmode), elemtype)
    -- Reftype_ok: `%|-%:OK`(C, elemtype)
    -- (Expr_ok_const: `%|-%:%CONST`(C, expr, (elemtype : reftype <: valtype)))*{expr <- `expr*`}
    -- Elemmode_ok: `%|-%:%`(C, elemmode, elemtype)

;; 3-typing.watsup
relation Datamode_ok: `%|-%:%`(context, datamode, datatype)
  ;; 3-typing.watsup
  rule active{C : context, x : idx, expr : expr, mt : memtype}:
    `%|-%:%`(C, ACTIVE_datamode(x, expr), OK_datatype)
    -- if (C.MEMS_context[x!`%`_idx.0] = mt)
    -- Expr_ok_const: `%|-%:%CONST`(C, expr, I32_valtype)

  ;; 3-typing.watsup
  rule passive{C : context}:
    `%|-%:%`(C, PASSIVE_datamode, OK_datatype)

;; 3-typing.watsup
relation Data_ok: `%|-%:%`(context, data, datatype)
  ;; 3-typing.watsup
  rule _{C : context, `b*` : byte*, datamode : datamode}:
    `%|-%:%`(C, DATA_data(b*{b <- `b*`}, datamode), OK_datatype)
    -- Datamode_ok: `%|-%:%`(C, datamode, OK_datatype)

;; 3-typing.watsup
relation Start_ok: `%|-%:OK`(context, start)
  ;; 3-typing.watsup
  rule _{C : context, x : idx}:
    `%|-%:OK`(C, START_start(x))
    -- Expand: `%~~%`(C.FUNCS_context[x!`%`_idx.0], FUNC_comptype(`%->%`_functype(`%`_resulttype([]), `%`_resulttype([]))))

;; 3-typing.watsup
relation Import_ok: `%|-%:%`(context, import, externtype)
  ;; 3-typing.watsup
  rule _{C : context, name_1 : name, name_2 : name, xt : externtype}:
    `%|-%:%`(C, IMPORT_import(name_1, name_2, xt), xt)
    -- Externtype_ok: `%|-%:OK`(C, xt)

;; 3-typing.watsup
relation Externidx_ok: `%|-%:%`(context, externidx, externtype)
  ;; 3-typing.watsup
  rule func{C : context, x : idx, dt : deftype}:
    `%|-%:%`(C, FUNC_externidx(x), FUNC_externtype((dt : deftype <: typeuse)))
    -- if (C.FUNCS_context[x!`%`_idx.0] = dt)

  ;; 3-typing.watsup
  rule global{C : context, x : idx, gt : globaltype}:
    `%|-%:%`(C, GLOBAL_externidx(x), GLOBAL_externtype(gt))
    -- if (C.GLOBALS_context[x!`%`_idx.0] = gt)

  ;; 3-typing.watsup
  rule table{C : context, x : idx, tt : tabletype}:
    `%|-%:%`(C, TABLE_externidx(x), TABLE_externtype(tt))
    -- if (C.TABLES_context[x!`%`_idx.0] = tt)

  ;; 3-typing.watsup
  rule mem{C : context, x : idx, mt : memtype}:
    `%|-%:%`(C, MEM_externidx(x), MEM_externtype(mt))
    -- if (C.MEMS_context[x!`%`_idx.0] = mt)

  ;; 3-typing.watsup
  rule tag{C : context, x : idx, jt : tagtype}:
    `%|-%:%`(C, TAG_externidx(x), TAG_externtype((jt : deftype <: typeuse)))
    -- if (C.TAGS_context[x!`%`_idx.0] = jt)

;; 3-typing.watsup
relation Export_ok: `%|-%:%%`(context, export, name, externtype)
  ;; 3-typing.watsup
  rule _{C : context, name : name, externidx : externidx, xt : externtype}:
    `%|-%:%%`(C, EXPORT_export(name, externidx), name, xt)
    -- Externidx_ok: `%|-%:%`(C, externidx, xt)

;; 3-typing.watsup
rec {

;; 3-typing.watsup:1382.1-1382.100
relation Globals_ok: `%|-%:%`(context, global*, globaltype*)
  ;; 3-typing.watsup:1426.1-1427.17
  rule empty{C : context}:
    `%|-%:%`(C, [], [])

  ;; 3-typing.watsup:1429.1-1432.54
  rule cons{C : context, global_1 : global, `global*` : global*, gt_1 : globaltype, `gt*` : globaltype*}:
    `%|-%:%`(C, [global_1] ++ global*{global <- `global*`}, [gt_1] ++ gt*{gt <- `gt*`})
    -- Global_ok: `%|-%:%`(C, global_1, gt_1)
    -- Globals_ok: `%|-%:%`(C +++ {TYPES [], RECS [], FUNCS [], GLOBALS [gt_1], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, global*{global <- `global*`}, gt*{gt <- `gt*`})
}

;; 3-typing.watsup
rec {

;; 3-typing.watsup:1381.1-1381.98
relation Types_ok: `%|-%:%`(context, type*, deftype*)
  ;; 3-typing.watsup:1418.1-1419.17
  rule empty{C : context}:
    `%|-%:%`(C, [], [])

  ;; 3-typing.watsup:1421.1-1424.49
  rule cons{C : context, type_1 : type, `type*` : type*, `dt_1*` : deftype*, `dt*` : deftype*}:
    `%|-%:%`(C, [type_1] ++ type*{type <- `type*`}, dt_1*{dt_1 <- `dt_1*`} ++ dt*{dt <- `dt*`})
    -- Type_ok: `%|-%:%`(C, type_1, dt_1*{dt_1 <- `dt_1*`})
    -- Types_ok: `%|-%:%`(C +++ {TYPES dt_1*{dt_1 <- `dt_1*`}, RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, type*{type <- `type*`}, dt*{dt <- `dt*`})
}

;; 3-typing.watsup
syntax nonfuncs =
  | `%%%%%`{`global*` : global*, `table*` : table*, `mem*` : mem*, `elem*` : elem*, `data*` : data*}(global*{global <- `global*`} : global*, table*{table <- `table*`} : table*, mem*{mem <- `mem*`} : mem*, elem*{elem <- `elem*`} : elem*, data*{data <- `data*`} : data*)

;; 3-typing.watsup
def $funcidx_nonfuncs(nonfuncs : nonfuncs) : funcidx*
  ;; 3-typing.watsup
  def $funcidx_nonfuncs{`global*` : global*, `table*` : table*, `mem*` : mem*, `elem*` : elem*, `data*` : data*}(`%%%%%`_nonfuncs(global*{global <- `global*`}, table*{table <- `table*`}, mem*{mem <- `mem*`}, elem*{elem <- `elem*`}, data*{data <- `data*`})) = $funcidx_module(MODULE_module([], [], [], global*{global <- `global*`}, table*{table <- `table*`}, mem*{mem <- `mem*`}, [], elem*{elem <- `elem*`}, data*{data <- `data*`}, ?(), []))

;; 3-typing.watsup
relation Module_ok: `|-%:%`(module, moduletype)
  ;; 3-typing.watsup
  rule _{`type*` : type*, `import*` : import*, `func*` : func*, `global*` : global*, `table*` : table*, `mem*` : mem*, `tag*` : tag*, `elem*` : elem*, `data*` : data*, `start?` : start?, `export*` : export*, C : context, `xt_I*` : externtype*, `xt_E*` : externtype*, `dt'*` : deftype*, C' : context, `gt*` : globaltype*, `tt*` : tabletype*, `mt*` : memtype*, `jt*` : tagtype*, `dt*` : deftype*, `rt*` : reftype*, `ok*` : datatype*, `nm*` : name*, `tt_I*` : tabletype*, `mt_I*` : memtype*, `jt_I*` : tagtype*, `dt_I*` : deftype*, `gt_I*` : globaltype*, `x*` : idx*}:
    `|-%:%`(MODULE_module(type*{type <- `type*`}, import*{import <- `import*`}, func*{func <- `func*`}, global*{global <- `global*`}, table*{table <- `table*`}, mem*{mem <- `mem*`}, tag*{tag <- `tag*`}, elem*{elem <- `elem*`}, data*{data <- `data*`}, start?{start <- `start?`}, export*{export <- `export*`}), $clos_moduletype(C, `%->%`_moduletype(xt_I*{xt_I <- `xt_I*`}, xt_E*{xt_E <- `xt_E*`})))
    -- Types_ok: `%|-%:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, type*{type <- `type*`}, dt'*{dt' <- `dt'*`})
    -- (Import_ok: `%|-%:%`({TYPES dt'*{dt' <- `dt'*`}, RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, import, xt_I))*{import <- `import*`, xt_I <- `xt_I*`}
    -- Globals_ok: `%|-%:%`(C', global*{global <- `global*`}, gt*{gt <- `gt*`})
    -- (Table_ok: `%|-%:%`(C', table, tt))*{table <- `table*`, tt <- `tt*`}
    -- (Mem_ok: `%|-%:%`(C', mem, mt))*{mem <- `mem*`, mt <- `mt*`}
    -- (Tag_ok: `%|-%:%`(C', tag, jt))*{jt <- `jt*`, tag <- `tag*`}
    -- (Func_ok: `%|-%:%`(C, func, dt))*{dt <- `dt*`, func <- `func*`}
    -- (Elem_ok: `%|-%:%`(C, elem, rt))*{elem <- `elem*`, rt <- `rt*`}
    -- (Data_ok: `%|-%:%`(C, data, ok))*{data <- `data*`, ok <- `ok*`}
    -- (Start_ok: `%|-%:OK`(C, start))?{start <- `start?`}
    -- (Export_ok: `%|-%:%%`(C, export, nm, xt_E))*{export <- `export*`, nm <- `nm*`, xt_E <- `xt_E*`}
    -- if $disjoint_(syntax name, nm*{nm <- `nm*`})
    -- if (C = C' +++ {TYPES [], RECS [], FUNCS [], GLOBALS gt*{gt <- `gt*`}, TABLES tt_I*{tt_I <- `tt_I*`} ++ tt*{tt <- `tt*`}, MEMS mt_I*{mt_I <- `mt_I*`} ++ mt*{mt <- `mt*`}, TAGS jt_I*{jt_I <- `jt_I*`} ++ jt*{jt <- `jt*`}, ELEMS rt*{rt <- `rt*`}, DATAS ok*{ok <- `ok*`}, LOCALS [], LABELS [], RETURN ?(), REFS []})
    -- if (C' = {TYPES dt'*{dt' <- `dt'*`}, RECS [], FUNCS dt_I*{dt_I <- `dt_I*`} ++ dt*{dt <- `dt*`}, GLOBALS gt_I*{gt_I <- `gt_I*`}, TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS x*{x <- `x*`}})
    -- if (x*{x <- `x*`} = $funcidx_nonfuncs(`%%%%%`_nonfuncs(global*{global <- `global*`}, table*{table <- `table*`}, mem*{mem <- `mem*`}, elem*{elem <- `elem*`}, data*{data <- `data*`})))
    -- if (dt_I*{dt_I <- `dt_I*`} = $funcsxt(xt_I*{xt_I <- `xt_I*`}))
    -- if (gt_I*{gt_I <- `gt_I*`} = $globalsxt(xt_I*{xt_I <- `xt_I*`}))
    -- if (tt_I*{tt_I <- `tt_I*`} = $tablesxt(xt_I*{xt_I <- `xt_I*`}))
    -- if (mt_I*{mt_I <- `mt_I*`} = $memsxt(xt_I*{xt_I <- `xt_I*`}))
    -- if (jt_I*{jt_I <- `jt_I*`} = $tagsxt(xt_I*{xt_I <- `xt_I*`}))

;; 4-numerics.watsup
syntax relaxed2 =
  | `%`{i : nat}(i : nat)
    -- if ((i = 0) \/ (i = 1))

;; 4-numerics.watsup
syntax relaxed4 =
  | `%`{i : nat}(i : nat)
    -- if ((((i = 0) \/ (i = 1)) \/ (i = 2)) \/ (i = 3))

;; 4-numerics.watsup
def $relaxed2(relaxed2 : relaxed2, syntax X, X : X, X : X) : X
  ;; 4-numerics.watsup
  def $relaxed2{i : relaxed2, syntax X, X_1 : X, X_2 : X}(i, syntax X, X_1, X_2) = [X_1 X_2][i!`%`_relaxed2.0]
    -- if $ND
  ;; 4-numerics.watsup
  def $relaxed2{i : relaxed2, syntax X, X_1 : X, X_2 : X}(i, syntax X, X_1, X_2) = [X_1 X_2][0]
    -- otherwise

;; 4-numerics.watsup
def $relaxed4(relaxed4 : relaxed4, syntax X, X : X, X : X, X : X, X : X) : X
  ;; 4-numerics.watsup
  def $relaxed4{i : relaxed4, syntax X, X_1 : X, X_2 : X, X_3 : X, X_4 : X}(i, syntax X, X_1, X_2, X_3, X_4) = [X_1 X_2 X_3 X_4][i!`%`_relaxed4.0]
    -- if $ND
  ;; 4-numerics.watsup
  def $relaxed4{i : relaxed4, syntax X, X_1 : X, X_2 : X, X_3 : X, X_4 : X}(i, syntax X, X_1, X_2, X_3, X_4) = [X_1 X_2 X_3 X_4][0]
    -- otherwise

;; 4-numerics.watsup
def $R_fmadd : relaxed2

;; 4-numerics.watsup
def $R_fmin : relaxed4

;; 4-numerics.watsup
def $R_fmax : relaxed4

;; 4-numerics.watsup
def $R_idot : relaxed2

;; 4-numerics.watsup
def $R_iq15mulr : relaxed2

;; 4-numerics.watsup
def $R_trunc_u : relaxed4

;; 4-numerics.watsup
def $R_trunc_s : relaxed2

;; 4-numerics.watsup
def $R_swizzle : relaxed2

;; 4-numerics.watsup
def $R_laneselect : relaxed2

;; 4-numerics.watsup
def $s33_to_u32(s33 : s33) : u32

;; 4-numerics.watsup
def $ibits_(N : N, iN : iN(N)) : bit*

;; 4-numerics.watsup
def $fbits_(N : N, fN : fN(N)) : bit*

;; 4-numerics.watsup
def $ibytes_(N : N, iN : iN(N)) : byte*

;; 4-numerics.watsup
def $fbytes_(N : N, fN : fN(N)) : byte*

;; 4-numerics.watsup
def $nbytes_(numtype : numtype, num_ : num_(numtype)) : byte*

;; 4-numerics.watsup
def $vbytes_(vectype : vectype, vec_ : vec_(vectype)) : byte*

;; 4-numerics.watsup
def $zbytes_(storagetype : storagetype, lit_ : lit_(storagetype)) : byte*

;; 4-numerics.watsup
def $cbytes_(Cnn : Cnn, lit_ : lit_((Cnn : Cnn <: storagetype))) : byte*

;; 4-numerics.watsup
def $invibytes_(N : N, byte*) : iN(N)
  ;; 4-numerics.watsup
  def $invibytes_{N : N, `b*` : byte*, n : n}(N, b*{b <- `b*`}) = `%`_iN(n)
    -- if ($ibytes_(N, `%`_iN(n)) = b*{b <- `b*`})

;; 4-numerics.watsup
def $invfbytes_(N : N, byte*) : fN(N)
  ;; 4-numerics.watsup
  def $invfbytes_{N : N, `b*` : byte*, p : fN(N)}(N, b*{b <- `b*`}) = p
    -- if ($fbytes_(N, p) = b*{b <- `b*`})

;; 4-numerics.watsup
def $signed_(N : N, nat : nat) : int
  ;; 4-numerics.watsup
  def $signed_{N : N, i : nat}(N, i) = (i : nat <:> int)
    -- if (i < (2 ^ (((N : nat <:> int) - (1 : nat <:> int)) : int <:> nat)))
  ;; 4-numerics.watsup
  def $signed_{N : N, i : nat}(N, i) = ((i : nat <:> int) - ((2 ^ N) : nat <:> int))
    -- if (((2 ^ (((N : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) <= i) /\ (i < (2 ^ N)))

;; 4-numerics.watsup
def $invsigned_(N : N, int : int) : nat
  ;; 4-numerics.watsup
  def $invsigned_{N : N, i : int, j : nat}(N, i) = j
    -- if ($signed_(N, j) = i)

;; 4-numerics.watsup
def $sx(storagetype : storagetype) : sx?
  ;; 4-numerics.watsup
  def $sx{consttype : consttype}((consttype : consttype <: storagetype)) = ?()
  ;; 4-numerics.watsup
  def $sx{packtype : packtype}((packtype : packtype <: storagetype)) = ?(S_sx)

;; 4-numerics.watsup
def $zero(lanetype : lanetype) : lane_(lanetype)
  ;; 4-numerics.watsup
  def $zero{Jnn : Jnn}((Jnn : Jnn <: lanetype)) = `%`_lane_(0)
  ;; 4-numerics.watsup
  def $zero{Fnn : Fnn}((Fnn : Fnn <: lanetype)) = $fzero($size((Fnn : Fnn <: numtype)))

;; 4-numerics.watsup
def $bool(bool : bool) : nat
  ;; 4-numerics.watsup
  def $bool(false) = 0
  ;; 4-numerics.watsup
  def $bool(true) = 1

;; 4-numerics.watsup
def $int(rat : rat) : int

;; 4-numerics.watsup
def $sat_u_(N : N, int : int) : nat
  ;; 4-numerics.watsup
  def $sat_u_{N : N, i : int}(N, i) = 0
    -- if (i < (0 : nat <:> int))
  ;; 4-numerics.watsup
  def $sat_u_{N : N, i : int}(N, i) = ((((2 ^ N) : nat <:> int) - (1 : nat <:> int)) : int <:> nat)
    -- if (i > (((2 ^ N) : nat <:> int) - (1 : nat <:> int)))
  ;; 4-numerics.watsup
  def $sat_u_{N : N, i : int}(N, i) = (i : int <:> nat)
    -- otherwise

;; 4-numerics.watsup
def $sat_s_(N : N, int : int) : int
  ;; 4-numerics.watsup
  def $sat_s_{N : N, i : int}(N, i) = - ((2 ^ (((N : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) : nat <:> int)
    -- if (i < - ((2 ^ (((N : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) : nat <:> int))
  ;; 4-numerics.watsup
  def $sat_s_{N : N, i : int}(N, i) = (((2 ^ (((N : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) : nat <:> int) - (1 : nat <:> int))
    -- if (i > (((2 ^ (((N : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) : nat <:> int) - (1 : nat <:> int)))
  ;; 4-numerics.watsup
  def $sat_s_{N : N, i : int}(N, i) = i
    -- otherwise

;; 4-numerics.watsup
def $ineg_(N : N, iN : iN(N)) : iN(N)
  ;; 4-numerics.watsup
  def $ineg_{N : N, i_1 : iN(N)}(N, i_1) = `%`_iN($invsigned_(N, - $signed_(N, i_1!`%`_iN.0)))

;; 4-numerics.watsup
def $iabs_(N : N, iN : iN(N)) : iN(N)
  ;; 4-numerics.watsup
  def $iabs_{N : N, i_1 : iN(N)}(N, i_1) = i_1
    -- if ($signed_(N, i_1!`%`_iN.0) >= (0 : nat <:> int))
  ;; 4-numerics.watsup
  def $iabs_{N : N, i_1 : iN(N)}(N, i_1) = $ineg_(N, i_1)
    -- otherwise

;; 4-numerics.watsup
def $iclz_(N : N, iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $ictz_(N : N, iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $ipopcnt_(N : N, iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $iextend_(N : N, M : M, sx : sx, iN : iN(N)) : iN(N)
  ;; 4-numerics.watsup
  def $iextend_{N : N, M : M, i : iN(N)}(N, M, U_sx, i) = `%`_iN((i!`%`_iN.0 \ (2 ^ M)))
  ;; 4-numerics.watsup
  def $iextend_{N : N, M : M, i : iN(N)}(N, M, S_sx, i) = `%`_iN($invsigned_(N, $signed_(M, (i!`%`_iN.0 \ (2 ^ M)))))

;; 4-numerics.watsup
def $iadd_(N : N, iN : iN(N), iN : iN(N)) : iN(N)
  ;; 4-numerics.watsup
  def $iadd_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, i_1, i_2) = `%`_iN(((i_1!`%`_iN.0 + i_2!`%`_iN.0) \ (2 ^ N)))

;; 4-numerics.watsup
def $isub_(N : N, iN : iN(N), iN : iN(N)) : iN(N)
  ;; 4-numerics.watsup
  def $isub_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, i_1, i_2) = `%`_iN(((((((2 ^ N) + i_1!`%`_iN.0) : nat <:> int) - (i_2!`%`_iN.0 : nat <:> int)) \ ((2 ^ N) : nat <:> int)) : int <:> nat))

;; 4-numerics.watsup
def $imul_(N : N, iN : iN(N), iN : iN(N)) : iN(N)
  ;; 4-numerics.watsup
  def $imul_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, i_1, i_2) = `%`_iN(((i_1!`%`_iN.0 * i_2!`%`_iN.0) \ (2 ^ N)))

;; 4-numerics.watsup
def $idiv_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)?

;; 4-numerics.watsup
def $irem_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)?

;; 4-numerics.watsup
def $imin_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $imax_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $iadd_sat_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)
  ;; 4-numerics.watsup
  def $iadd_sat_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, U_sx, i_1, i_2) = `%`_iN($sat_u_(N, ((i_1!`%`_iN.0 + i_2!`%`_iN.0) : nat <:> int)))
  ;; 4-numerics.watsup
  def $iadd_sat_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, S_sx, i_1, i_2) = `%`_iN($invsigned_(N, $sat_s_(N, ($signed_(N, i_1!`%`_iN.0) + $signed_(N, i_2!`%`_iN.0)))))

;; 4-numerics.watsup
def $isub_sat_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)
  ;; 4-numerics.watsup
  def $isub_sat_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, U_sx, i_1, i_2) = `%`_iN($sat_u_(N, ((i_1!`%`_iN.0 : nat <:> int) - (i_2!`%`_iN.0 : nat <:> int))))
  ;; 4-numerics.watsup
  def $isub_sat_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, S_sx, i_1, i_2) = `%`_iN($invsigned_(N, $sat_s_(N, ($signed_(N, i_1!`%`_iN.0) - $signed_(N, i_2!`%`_iN.0)))))

;; 4-numerics.watsup
def $iq15mulr_sat_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $irelaxed_q15mulr_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)*

;; 4-numerics.watsup
def $iavgr_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $inot_(N : N, iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $irev_(N : N, iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $iand_(N : N, iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $iandnot_(N : N, iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $ior_(N : N, iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $ixor_(N : N, iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $ishl_(N : N, iN : iN(N), u32 : u32) : iN(N)

;; 4-numerics.watsup
def $ishr_(N : N, sx : sx, iN : iN(N), u32 : u32) : iN(N)

;; 4-numerics.watsup
def $irotl_(N : N, iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $irotr_(N : N, iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $ibitselect_(N : N, iN : iN(N), iN : iN(N), iN : iN(N)) : iN(N)

;; 4-numerics.watsup
def $irelaxed_laneselect_(N : N, iN : iN(N), iN : iN(N), iN : iN(N)) : iN(N)*

;; 4-numerics.watsup
def $ieqz_(N : N, iN : iN(N)) : u32
  ;; 4-numerics.watsup
  def $ieqz_{N : N, i_1 : iN(N)}(N, i_1) = `%`_u32($bool((i_1!`%`_iN.0 = 0)))

;; 4-numerics.watsup
def $inez_(N : N, iN : iN(N)) : u32
  ;; 4-numerics.watsup
  def $inez_{N : N, i_1 : iN(N)}(N, i_1) = `%`_u32($bool((i_1!`%`_iN.0 =/= 0)))

;; 4-numerics.watsup
def $ieq_(N : N, iN : iN(N), iN : iN(N)) : u32
  ;; 4-numerics.watsup
  def $ieq_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, i_1, i_2) = `%`_u32($bool((i_1 = i_2)))

;; 4-numerics.watsup
def $ine_(N : N, iN : iN(N), iN : iN(N)) : u32
  ;; 4-numerics.watsup
  def $ine_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, i_1, i_2) = `%`_u32($bool((i_1 =/= i_2)))

;; 4-numerics.watsup
def $ilt_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : u32
  ;; 4-numerics.watsup
  def $ilt_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, U_sx, i_1, i_2) = `%`_u32($bool((i_1!`%`_iN.0 < i_2!`%`_iN.0)))
  ;; 4-numerics.watsup
  def $ilt_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, S_sx, i_1, i_2) = `%`_u32($bool(($signed_(N, i_1!`%`_iN.0) < $signed_(N, i_2!`%`_iN.0))))

;; 4-numerics.watsup
def $igt_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : u32
  ;; 4-numerics.watsup
  def $igt_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, U_sx, i_1, i_2) = `%`_u32($bool((i_1!`%`_iN.0 > i_2!`%`_iN.0)))
  ;; 4-numerics.watsup
  def $igt_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, S_sx, i_1, i_2) = `%`_u32($bool(($signed_(N, i_1!`%`_iN.0) > $signed_(N, i_2!`%`_iN.0))))

;; 4-numerics.watsup
def $ile_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : u32
  ;; 4-numerics.watsup
  def $ile_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, U_sx, i_1, i_2) = `%`_u32($bool((i_1!`%`_iN.0 <= i_2!`%`_iN.0)))
  ;; 4-numerics.watsup
  def $ile_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, S_sx, i_1, i_2) = `%`_u32($bool(($signed_(N, i_1!`%`_iN.0) <= $signed_(N, i_2!`%`_iN.0))))

;; 4-numerics.watsup
def $ige_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : u32
  ;; 4-numerics.watsup
  def $ige_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, U_sx, i_1, i_2) = `%`_u32($bool((i_1!`%`_iN.0 >= i_2!`%`_iN.0)))
  ;; 4-numerics.watsup
  def $ige_{N : N, i_1 : iN(N), i_2 : iN(N)}(N, S_sx, i_1, i_2) = `%`_u32($bool(($signed_(N, i_1!`%`_iN.0) >= $signed_(N, i_2!`%`_iN.0))))

;; 4-numerics.watsup
def $fabs_(N : N, fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fneg_(N : N, fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fsqrt_(N : N, fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fceil_(N : N, fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $ffloor_(N : N, fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $ftrunc_(N : N, fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fnearest_(N : N, fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fadd_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fsub_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fmul_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fdiv_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fmin_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fmax_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fpmin_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fpmax_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $frelaxed_min_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $frelaxed_max_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $fcopysign_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $feq_(N : N, fN : fN(N), fN : fN(N)) : u32

;; 4-numerics.watsup
def $fne_(N : N, fN : fN(N), fN : fN(N)) : u32

;; 4-numerics.watsup
def $flt_(N : N, fN : fN(N), fN : fN(N)) : u32

;; 4-numerics.watsup
def $fgt_(N : N, fN : fN(N), fN : fN(N)) : u32

;; 4-numerics.watsup
def $fle_(N : N, fN : fN(N), fN : fN(N)) : u32

;; 4-numerics.watsup
def $fge_(N : N, fN : fN(N), fN : fN(N)) : u32

;; 4-numerics.watsup
def $frelaxed_madd_(N : N, fN : fN(N), fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $frelaxed_nmadd_(N : N, fN : fN(N), fN : fN(N), fN : fN(N)) : fN(N)*

;; 4-numerics.watsup
def $wrap__(M : M, N : N, iN : iN(M)) : iN(N)

;; 4-numerics.watsup
def $extend__(M : M, N : N, sx : sx, iN : iN(M)) : iN(N)

;; 4-numerics.watsup
def $trunc__(M : M, N : N, sx : sx, fN : fN(M)) : iN(N)?

;; 4-numerics.watsup
def $trunc_sat__(M : M, N : N, sx : sx, fN : fN(M)) : iN(N)?

;; 4-numerics.watsup
def $relaxed_trunc__(M : M, N : N, sx : sx, fN : fN(M)) : iN(N)?

;; 4-numerics.watsup
def $demote__(M : M, N : N, fN : fN(M)) : fN(N)*

;; 4-numerics.watsup
def $promote__(M : M, N : N, fN : fN(M)) : fN(N)*

;; 4-numerics.watsup
def $convert__(M : M, N : N, sx : sx, iN : iN(M)) : fN(N)

;; 4-numerics.watsup
def $narrow__(M : M, N : N, sx : sx, iN : iN(M)) : iN(N)

;; 4-numerics.watsup
def $reinterpret__(numtype_1 : numtype, numtype_2 : numtype, num_ : num_(numtype_1)) : num_(numtype_2)

;; 4-numerics.watsup
def $lpacknum_(lanetype : lanetype, num_ : num_($lunpack(lanetype))) : lane_(lanetype)
  ;; 4-numerics.watsup
  def $lpacknum_{numtype : numtype, c : num_($lunpack((numtype : numtype <: lanetype)))}((numtype : numtype <: lanetype), c) = c
  ;; 4-numerics.watsup
  def $lpacknum_{packtype : packtype, c : num_($lunpack((packtype : packtype <: lanetype)))}((packtype : packtype <: lanetype), c) = $wrap__($size($lunpack((packtype : packtype <: lanetype))), $psize(packtype), c)

;; 4-numerics.watsup
def $lunpacknum_(lanetype : lanetype, lane_ : lane_(lanetype)) : num_($lunpack(lanetype))
  ;; 4-numerics.watsup
  def $lunpacknum_{numtype : numtype, c : lane_((numtype : numtype <: lanetype))}((numtype : numtype <: lanetype), c) = c
  ;; 4-numerics.watsup
  def $lunpacknum_{packtype : packtype, c : lane_((packtype : packtype <: lanetype))}((packtype : packtype <: lanetype), c) = $extend__($psize(packtype), $size($lunpack((packtype : packtype <: lanetype))), U_sx, c)

;; 4-numerics.watsup
def $cpacknum_(storagetype : storagetype, lit_ : lit_(($cunpack(storagetype) : consttype <: storagetype))) : lit_(storagetype)
  ;; 4-numerics.watsup
  def $cpacknum_{consttype : consttype, c : lit_(($cunpack((consttype : consttype <: storagetype)) : consttype <: storagetype))}((consttype : consttype <: storagetype), c) = c
  ;; 4-numerics.watsup
  def $cpacknum_{packtype : packtype, c : lit_(($cunpack((packtype : packtype <: storagetype)) : consttype <: storagetype))}((packtype : packtype <: storagetype), c) = $wrap__($size($lunpack((packtype : packtype <: lanetype))), $psize(packtype), c)

;; 4-numerics.watsup
def $cunpacknum_(storagetype : storagetype, lit_ : lit_(storagetype)) : lit_(($cunpack(storagetype) : consttype <: storagetype))
  ;; 4-numerics.watsup
  def $cunpacknum_{consttype : consttype, c : lit_((consttype : consttype <: storagetype))}((consttype : consttype <: storagetype), c) = c
  ;; 4-numerics.watsup
  def $cunpacknum_{packtype : packtype, c : lit_((packtype : packtype <: storagetype))}((packtype : packtype <: storagetype), c) = $extend__($psize(packtype), $size($lunpack((packtype : packtype <: lanetype))), U_sx, c)

;; 4-numerics.watsup
def $unop_(numtype : numtype, unop_ : unop_(numtype), num_ : num_(numtype)) : num_(numtype)*
  ;; 4-numerics.watsup
  def $unop_{Inn : Inn, i : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), CLZ_unop_, i) = [$iclz_($sizenn((Inn : Inn <: numtype)), i)]
  ;; 4-numerics.watsup
  def $unop_{Inn : Inn, i : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), CTZ_unop_, i) = [$ictz_($sizenn((Inn : Inn <: numtype)), i)]
  ;; 4-numerics.watsup
  def $unop_{Inn : Inn, i : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), POPCNT_unop_, i) = [$ipopcnt_($sizenn((Inn : Inn <: numtype)), i)]
  ;; 4-numerics.watsup
  def $unop_{Inn : Inn, M : M, i : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), EXTEND_unop_(`%`_sz(M)), i) = [$iextend_($sizenn((Inn : Inn <: numtype)), M, S_sx, i)]
  ;; 4-numerics.watsup
  def $unop_{Fnn : Fnn, f : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), ABS_unop_, f) = $fabs_($sizenn((Fnn : Fnn <: numtype)), f)
  ;; 4-numerics.watsup
  def $unop_{Fnn : Fnn, f : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), NEG_unop_, f) = $fneg_($sizenn((Fnn : Fnn <: numtype)), f)
  ;; 4-numerics.watsup
  def $unop_{Fnn : Fnn, f : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), SQRT_unop_, f) = $fsqrt_($sizenn((Fnn : Fnn <: numtype)), f)
  ;; 4-numerics.watsup
  def $unop_{Fnn : Fnn, f : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), CEIL_unop_, f) = $fceil_($sizenn((Fnn : Fnn <: numtype)), f)
  ;; 4-numerics.watsup
  def $unop_{Fnn : Fnn, f : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), FLOOR_unop_, f) = $ffloor_($sizenn((Fnn : Fnn <: numtype)), f)
  ;; 4-numerics.watsup
  def $unop_{Fnn : Fnn, f : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), TRUNC_unop_, f) = $ftrunc_($sizenn((Fnn : Fnn <: numtype)), f)
  ;; 4-numerics.watsup
  def $unop_{Fnn : Fnn, f : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), NEAREST_unop_, f) = $fnearest_($sizenn((Fnn : Fnn <: numtype)), f)

;; 4-numerics.watsup
def $binop_(numtype : numtype, binop_ : binop_(numtype), num_ : num_(numtype), num_ : num_(numtype)) : num_(numtype)*
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), ADD_binop_, i_1, i_2) = [$iadd_($sizenn((Inn : Inn <: numtype)), i_1, i_2)]
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), SUB_binop_, i_1, i_2) = [$isub_($sizenn((Inn : Inn <: numtype)), i_1, i_2)]
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), MUL_binop_, i_1, i_2) = [$imul_($sizenn((Inn : Inn <: numtype)), i_1, i_2)]
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, sx : sx, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), DIV_binop_(sx), i_1, i_2) = lift($idiv_($sizenn((Inn : Inn <: numtype)), sx, i_1, i_2))
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, sx : sx, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), REM_binop_(sx), i_1, i_2) = lift($irem_($sizenn((Inn : Inn <: numtype)), sx, i_1, i_2))
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), AND_binop_, i_1, i_2) = [$iand_($sizenn((Inn : Inn <: numtype)), i_1, i_2)]
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), OR_binop_, i_1, i_2) = [$ior_($sizenn((Inn : Inn <: numtype)), i_1, i_2)]
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), XOR_binop_, i_1, i_2) = [$ixor_($sizenn((Inn : Inn <: numtype)), i_1, i_2)]
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), SHL_binop_, i_1, i_2) = [$ishl_($sizenn((Inn : Inn <: numtype)), i_1, `%`_u32(i_2!`%`_num_.0))]
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, sx : sx, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), SHR_binop_(sx), i_1, i_2) = [$ishr_($sizenn((Inn : Inn <: numtype)), sx, i_1, `%`_u32(i_2!`%`_num_.0))]
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), ROTL_binop_, i_1, i_2) = [$irotl_($sizenn((Inn : Inn <: numtype)), i_1, i_2)]
  ;; 4-numerics.watsup
  def $binop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), ROTR_binop_, i_1, i_2) = [$irotr_($sizenn((Inn : Inn <: numtype)), i_1, i_2)]
  ;; 4-numerics.watsup
  def $binop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), ADD_binop_, f_1, f_2) = $fadd_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $binop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), SUB_binop_, f_1, f_2) = $fsub_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $binop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), MUL_binop_, f_1, f_2) = $fmul_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $binop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), DIV_binop_, f_1, f_2) = $fdiv_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $binop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), MIN_binop_, f_1, f_2) = $fmin_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $binop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), MAX_binop_, f_1, f_2) = $fmax_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $binop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), COPYSIGN_binop_, f_1, f_2) = $fcopysign_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)

;; 4-numerics.watsup
def $testop_(numtype : numtype, testop_ : testop_(numtype), num_ : num_(numtype)) : u32
  ;; 4-numerics.watsup
  def $testop_{Inn : Inn, i : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), EQZ_testop_, i) = $ieqz_($sizenn((Inn : Inn <: numtype)), i)

;; 4-numerics.watsup
def $relop_(numtype : numtype, relop_ : relop_(numtype), num_ : num_(numtype), num_ : num_(numtype)) : u32
  ;; 4-numerics.watsup
  def $relop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), EQ_relop_, i_1, i_2) = $ieq_($sizenn((Inn : Inn <: numtype)), i_1, i_2)
  ;; 4-numerics.watsup
  def $relop_{Inn : Inn, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), NE_relop_, i_1, i_2) = $ine_($sizenn((Inn : Inn <: numtype)), i_1, i_2)
  ;; 4-numerics.watsup
  def $relop_{Inn : Inn, sx : sx, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), LT_relop_(sx), i_1, i_2) = $ilt_($sizenn((Inn : Inn <: numtype)), sx, i_1, i_2)
  ;; 4-numerics.watsup
  def $relop_{Inn : Inn, sx : sx, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), GT_relop_(sx), i_1, i_2) = $igt_($sizenn((Inn : Inn <: numtype)), sx, i_1, i_2)
  ;; 4-numerics.watsup
  def $relop_{Inn : Inn, sx : sx, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), LE_relop_(sx), i_1, i_2) = $ile_($sizenn((Inn : Inn <: numtype)), sx, i_1, i_2)
  ;; 4-numerics.watsup
  def $relop_{Inn : Inn, sx : sx, i_1 : num_((Inn : Inn <: numtype)), i_2 : num_((Inn : Inn <: numtype))}((Inn : Inn <: numtype), GE_relop_(sx), i_1, i_2) = $ige_($sizenn((Inn : Inn <: numtype)), sx, i_1, i_2)
  ;; 4-numerics.watsup
  def $relop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), EQ_relop_, f_1, f_2) = $feq_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $relop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), NE_relop_, f_1, f_2) = $fne_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $relop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), LT_relop_, f_1, f_2) = $flt_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $relop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), GT_relop_, f_1, f_2) = $fgt_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $relop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), LE_relop_, f_1, f_2) = $fle_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)
  ;; 4-numerics.watsup
  def $relop_{Fnn : Fnn, f_1 : num_((Fnn : Fnn <: numtype)), f_2 : num_((Fnn : Fnn <: numtype))}((Fnn : Fnn <: numtype), GE_relop_, f_1, f_2) = $fge_($sizenn((Fnn : Fnn <: numtype)), f_1, f_2)

;; 4-numerics.watsup
def $cvtop__(numtype_1 : numtype, numtype_2 : numtype, cvtop__ : cvtop__(numtype_1, numtype_2), num_ : num_(numtype_1)) : num_(numtype_2)*
  ;; 4-numerics.watsup
  def $cvtop__{Inn_1 : Inn, Inn_2 : Inn, sx : sx, i_1 : num_((Inn_1 : Inn <: numtype))}((Inn_1 : Inn <: numtype), (Inn_2 : Inn <: numtype), EXTEND_cvtop__(sx), i_1) = [$extend__($sizenn1((Inn_1 : Inn <: numtype)), $sizenn2((Inn_2 : Inn <: numtype)), sx, i_1)]
  ;; 4-numerics.watsup
  def $cvtop__{Inn_1 : Inn, Inn_2 : Inn, i_1 : num_((Inn_1 : Inn <: numtype))}((Inn_1 : Inn <: numtype), (Inn_2 : Inn <: numtype), WRAP_cvtop__, i_1) = [$wrap__($sizenn1((Inn_1 : Inn <: numtype)), $sizenn2((Inn_2 : Inn <: numtype)), i_1)]
  ;; 4-numerics.watsup
  def $cvtop__{Fnn_1 : Fnn, Inn_2 : Inn, sx : sx, f_1 : num_((Fnn_1 : Fnn <: numtype))}((Fnn_1 : Fnn <: numtype), (Inn_2 : Inn <: numtype), TRUNC_cvtop__(sx), f_1) = lift($trunc__($sizenn1((Fnn_1 : Fnn <: numtype)), $sizenn2((Inn_2 : Inn <: numtype)), sx, f_1))
  ;; 4-numerics.watsup
  def $cvtop__{Fnn_1 : Fnn, Inn_2 : Inn, sx : sx, f_1 : num_((Fnn_1 : Fnn <: numtype))}((Fnn_1 : Fnn <: numtype), (Inn_2 : Inn <: numtype), TRUNC_SAT_cvtop__(sx), f_1) = lift($trunc_sat__($sizenn1((Fnn_1 : Fnn <: numtype)), $sizenn2((Inn_2 : Inn <: numtype)), sx, f_1))
  ;; 4-numerics.watsup
  def $cvtop__{Inn_1 : Inn, Fnn_2 : Fnn, sx : sx, i_1 : num_((Inn_1 : Inn <: numtype))}((Inn_1 : Inn <: numtype), (Fnn_2 : Fnn <: numtype), CONVERT_cvtop__(sx), i_1) = [$convert__($sizenn1((Inn_1 : Inn <: numtype)), $sizenn2((Fnn_2 : Fnn <: numtype)), sx, i_1)]
  ;; 4-numerics.watsup
  def $cvtop__{Fnn_1 : Fnn, Fnn_2 : Fnn, f_1 : num_((Fnn_1 : Fnn <: numtype))}((Fnn_1 : Fnn <: numtype), (Fnn_2 : Fnn <: numtype), PROMOTE_cvtop__, f_1) = $promote__($sizenn1((Fnn_1 : Fnn <: numtype)), $sizenn2((Fnn_2 : Fnn <: numtype)), f_1)
  ;; 4-numerics.watsup
  def $cvtop__{Fnn_1 : Fnn, Fnn_2 : Fnn, f_1 : num_((Fnn_1 : Fnn <: numtype))}((Fnn_1 : Fnn <: numtype), (Fnn_2 : Fnn <: numtype), DEMOTE_cvtop__, f_1) = $demote__($sizenn1((Fnn_1 : Fnn <: numtype)), $sizenn2((Fnn_2 : Fnn <: numtype)), f_1)
  ;; 4-numerics.watsup
  def $cvtop__{Inn_1 : Inn, Fnn_2 : Fnn, i_1 : num_((Inn_1 : Inn <: numtype))}((Inn_1 : Inn <: numtype), (Fnn_2 : Fnn <: numtype), REINTERPRET_cvtop__, i_1) = [$reinterpret__((Inn_1 : Inn <: numtype), (Fnn_2 : Fnn <: numtype), i_1)]
    -- if ($size((Inn_1 : Inn <: numtype)) = $size((Fnn_2 : Fnn <: numtype)))
  ;; 4-numerics.watsup
  def $cvtop__{Fnn_1 : Fnn, Inn_2 : Inn, f_1 : num_((Fnn_1 : Fnn <: numtype))}((Fnn_1 : Fnn <: numtype), (Inn_2 : Inn <: numtype), REINTERPRET_cvtop__, f_1) = [$reinterpret__((Fnn_1 : Fnn <: numtype), (Inn_2 : Inn <: numtype), f_1)]
    -- if ($size((Fnn_1 : Fnn <: numtype)) = $size((Inn_2 : Inn <: numtype)))

;; 4-numerics.watsup
def $lanes_(shape : shape, vec_ : vec_(V128_Vnn)) : lane_($lanetype(shape))*

;; 4-numerics.watsup
def $invlanes_(shape : shape, lane_($lanetype(shape))*) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $invlanes_{sh : shape, `c*` : lane_($lanetype(sh))*, vc : vec_(V128_Vnn)}(sh, c*{c <- `c*`}) = vc
    -- if (c*{c <- `c*`} = $lanes_(sh, vc))

;; 4-numerics.watsup
def $half__(shape_1 : shape, shape_2 : shape, half__ : half__(shape_1, shape_2), nat : nat, nat : nat) : nat
  ;; 4-numerics.watsup
  def $half__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, i : nat, j : nat}(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), LOW_half__, i, j) = i
  ;; 4-numerics.watsup
  def $half__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, i : nat, j : nat}(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), HIGH_half__, i, j) = j
  ;; 4-numerics.watsup
  def $half__{Lnn_1 : Lnn, M_1 : M, Fnn_2 : Fnn, M_2 : M, i : nat, j : nat}(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape((Fnn_2 : Fnn <: lanetype), `%`_dim(M_2)), LOW_half__, i, j) = i

;; 4-numerics.watsup
def $iswizzle_lane_(N : N, iN(N)*, iN : iN(N)) : iN(N)
  ;; 4-numerics.watsup
  def $iswizzle_lane_{N : N, `c*` : iN(N)*, i : iN(N)}(N, c*{c <- `c*`}, i) = c*{c <- `c*`}[i!`%`_iN.0]
    -- if (i!`%`_iN.0 < |c*{c <- `c*`}|)
  ;; 4-numerics.watsup
  def $iswizzle_lane_{N : N, `c*` : iN(N)*, i : iN(N)}(N, c*{c <- `c*`}, i) = `%`_iN(0)
    -- otherwise

;; 4-numerics.watsup
def $irelaxed_swizzle_lane_(N : N, iN(N)*, iN : iN(N)) : iN(N)
  ;; 4-numerics.watsup
  def $irelaxed_swizzle_lane_{N : N, `c*` : iN(N)*, i : iN(N)}(N, c*{c <- `c*`}, i) = c*{c <- `c*`}[i!`%`_iN.0]
    -- if (i!`%`_iN.0 < |c*{c <- `c*`}|)
  ;; 4-numerics.watsup
  def $irelaxed_swizzle_lane_{N : N, `c*` : iN(N)*, i : iN(N)}(N, c*{c <- `c*`}, i) = `%`_iN(0)
    -- if ($signed_(N, i!`%`_iN.0) < (0 : nat <:> int))
  ;; 4-numerics.watsup
  def $irelaxed_swizzle_lane_{N : N, `c*` : iN(N)*, i : iN(N)}(N, c*{c <- `c*`}, i) = $relaxed2($R_swizzle, syntax iN(N), `%`_iN(0), c*{c <- `c*`}[(i!`%`_iN.0 \ |c*{c <- `c*`}|)])
    -- otherwise

;; 4-numerics.watsup
def $ivunop_(shape : shape, def $f_(N : N, iN : iN(N)) : iN(N), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $ivunop_{Jnn : Jnn, M : M, def $f_(N : N, iN : iN(N)) : iN(N), v_1 : vec_(V128_Vnn), `c*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, v_1) = [$invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})]
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c*{c <- `c*`} = $f_($lsizenn((Jnn : Jnn <: lanetype)), c_1)*{c_1 <- `c_1*`})

;; 4-numerics.watsup
def $fvunop_(shape : shape, def $f_(N : N, fN : fN(N)) : fN(N)*, vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $fvunop_{Fnn : Fnn, M : M, def $f_(N : N, fN : fN(N)) : fN(N)*, v_1 : vec_(V128_Vnn), `c**` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))**, `c_1*` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $f_, v_1) = $invlanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})*{`c*` <- `c**`}
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c*{c <- `c*`}*{`c*` <- `c**`} = $setproduct_(syntax lane_((Fnn : Fnn <: lanetype)), $f_($sizenn((Fnn : Fnn <: numtype)), c_1)*{c_1 <- `c_1*`}))

;; 4-numerics.watsup
def $ivbinop_(shape : shape, def $f_(N : N, iN : iN(N), iN : iN(N)) : iN(N), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $ivbinop_{Jnn : Jnn, M : M, def $f_(N : N, iN : iN(N), iN : iN(N)) : iN(N), v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), `c*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, v_1, v_2) = [$invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})]
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_2))
    -- if (c*{c <- `c*`} = $f_($lsizenn((Jnn : Jnn <: lanetype)), c_1, c_2)*{c_1 <- `c_1*`, c_2 <- `c_2*`})

;; 4-numerics.watsup
def $ivbinopsx_(shape : shape, def $f_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N), sx : sx, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $ivbinopsx_{Jnn : Jnn, M : M, def $f_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N), sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), `c*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, sx, v_1, v_2) = [$invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})]
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_2))
    -- if (c*{c <- `c*`} = $f_($lsizenn((Jnn : Jnn <: lanetype)), sx, c_1, c_2)*{c_1 <- `c_1*`, c_2 <- `c_2*`})

;; 4-numerics.watsup
def $ivbinopsxnd_(shape : shape, def $f_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)*, sx : sx, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $ivbinopsxnd_{Jnn : Jnn, M : M, def $f_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : iN(N)*, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), `c**` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))**, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, sx, v_1, v_2) = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})*{`c*` <- `c**`}
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_2))
    -- if (c*{c <- `c*`}*{`c*` <- `c**`} = $setproduct_(syntax lane_((Jnn : Jnn <: lanetype)), $f_($lsizenn((Jnn : Jnn <: lanetype)), sx, c_1, c_2)*{c_1 <- `c_1*`, c_2 <- `c_2*`}))

;; 4-numerics.watsup
def $fvbinop_(shape : shape, def $f_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $fvbinop_{Fnn : Fnn, M : M, def $f_(N : N, fN : fN(N), fN : fN(N)) : fN(N)*, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), `c**` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))**, `c_1*` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $f_, v_1, v_2) = $invlanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})*{`c*` <- `c**`}
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), v_2))
    -- if (c*{c <- `c*`}*{`c*` <- `c**`} = $setproduct_(syntax lane_((Fnn : Fnn <: lanetype)), $f_($sizenn((Fnn : Fnn <: numtype)), c_1, c_2)*{c_1 <- `c_1*`, c_2 <- `c_2*`}))

;; 4-numerics.watsup
def $ivternopnd_(shape : shape, def $f_(N : N, iN : iN(N), iN : iN(N), iN : iN(N)) : iN(N)*, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $ivternopnd_{Jnn : Jnn, M : M, def $f_(N : N, iN : iN(N), iN : iN(N), iN : iN(N)) : iN(N)*, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), v_3 : vec_(V128_Vnn), `c**` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))**, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_3*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, v_1, v_2, v_3) = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})*{`c*` <- `c**`}
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_2))
    -- if (c_3*{c_3 <- `c_3*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_3))
    -- if (c*{c <- `c*`}*{`c*` <- `c**`} = $setproduct_(syntax lane_((Jnn : Jnn <: lanetype)), $f_($lsizenn((Jnn : Jnn <: lanetype)), c_1, c_2, c_3)*{c_1 <- `c_1*`, c_2 <- `c_2*`, c_3 <- `c_3*`}))

;; 4-numerics.watsup
def $fvternop_(shape : shape, def $f_(N : N, fN : fN(N), fN : fN(N), fN : fN(N)) : fN(N)*, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $fvternop_{Fnn : Fnn, M : M, def $f_(N : N, fN : fN(N), fN : fN(N), fN : fN(N)) : fN(N)*, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), v_3 : vec_(V128_Vnn), `c**` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))**, `c_1*` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))*, `c_3*` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $f_, v_1, v_2, v_3) = $invlanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})*{`c*` <- `c**`}
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), v_2))
    -- if (c_3*{c_3 <- `c_3*`} = $lanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), v_3))
    -- if (c*{c <- `c*`}*{`c*` <- `c**`} = $setproduct_(syntax lane_((Fnn : Fnn <: lanetype)), $f_($sizenn((Fnn : Fnn <: numtype)), c_1, c_2, c_3)*{c_1 <- `c_1*`, c_2 <- `c_2*`, c_3 <- `c_3*`}))

;; 4-numerics.watsup
def $ivtestop_(shape : shape, def $f_(N : N, iN : iN(N)) : u32, vec_ : vec_(V128_Vnn)) : u32
  ;; 4-numerics.watsup
  def $ivtestop_{Jnn : Jnn, M : M, def $f_(N : N, iN : iN(N)) : u32, v_1 : vec_(V128_Vnn), `c*` : nat*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, v_1) = `%`_u32($prod(c*{c <- `c*`}))
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (`%`_u32(c)*{c <- `c*`} = $f_($lsizenn((Jnn : Jnn <: lanetype)), c_1)*{c_1 <- `c_1*`})

;; 4-numerics.watsup
def $fvtestop_(shape : shape, def $f_(N : N, fN : fN(N)) : u32, vec_ : vec_(V128_Vnn)) : u32
  ;; 4-numerics.watsup
  def $fvtestop_{Fnn : Fnn, M : M, def $f_(N : N, fN : fN(N)) : u32, v_1 : vec_(V128_Vnn), `c*` : nat*, `c_1*` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $f_, v_1) = `%`_u32($prod(c*{c <- `c*`}))
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), v_1))
    -- if (`%`_u32(c)*{c <- `c*`} = $f_($sizenn((Fnn : Fnn <: numtype)), c_1)*{c_1 <- `c_1*`})

;; 4-numerics.watsup
def $ivrelop_(shape : shape, def $f_(N : N, iN : iN(N), iN : iN(N)) : u32, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $ivrelop_{Jnn : Jnn, M : M, def $f_(N : N, iN : iN(N), iN : iN(N)) : u32, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), `c*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, v_1, v_2) = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_2))
    -- if (c*{c <- `c*`} = $extend__(1, $lsizenn((Jnn : Jnn <: lanetype)), S_sx, `%`_iN($f_($lsizenn((Jnn : Jnn <: lanetype)), c_1, c_2)!`%`_u32.0))*{c_1 <- `c_1*`, c_2 <- `c_2*`})

;; 4-numerics.watsup
def $ivrelopsx_(shape : shape, def $f_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : u32, sx : sx, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $ivrelopsx_{Jnn : Jnn, M : M, def $f_(N : N, sx : sx, iN : iN(N), iN : iN(N)) : u32, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), `c*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, sx, v_1, v_2) = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_2))
    -- if (c*{c <- `c*`} = $extend__(1, $lsizenn((Jnn : Jnn <: lanetype)), S_sx, `%`_iN($f_($lsizenn((Jnn : Jnn <: lanetype)), sx, c_1, c_2)!`%`_u32.0))*{c_1 <- `c_1*`, c_2 <- `c_2*`})

;; 4-numerics.watsup
def $fvrelop_(shape : shape, def $f_(N : N, fN : fN(N), fN : fN(N)) : u32, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $fvrelop_{Fnn : Fnn, M : M, def $f_(N : N, fN : fN(N), fN : fN(N)) : u32, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), Inn : Inn, `c*` : lane_($lanetype(`%X%`_shape((Inn : Inn <: lanetype), `%`_dim(M))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $f_, v_1, v_2) = $invlanes_(`%X%`_shape((Inn : Inn <: lanetype), `%`_dim(M)), c*{c <- `c*`})
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), v_2))
    -- if (`%`_iN(c!`%`_lane_.0)*{c <- `c*`} = $extend__(1, $sizenn((Fnn : Fnn <: numtype)), S_sx, `%`_iN($f_($sizenn((Fnn : Fnn <: numtype)), c_1, c_2)!`%`_u32.0))*{c_1 <- `c_1*`, c_2 <- `c_2*`})
    -- if ($size((Inn : Inn <: numtype)) = $size((Fnn : Fnn <: numtype)))

;; 4-numerics.watsup
def $ivshiftop_(shape : shape, def $f_(N : N, iN : iN(N), u32 : u32) : iN(N), vec_ : vec_(V128_Vnn), u32 : u32) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $ivshiftop_{Jnn : Jnn, M : M, def $f_(N : N, iN : iN(N), u32 : u32) : iN(N), v_1 : vec_(V128_Vnn), i : u32, `c*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, v_1, i) = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c*{c <- `c*`} = $f_($lsizenn((Jnn : Jnn <: lanetype)), c_1, i)*{c_1 <- `c_1*`})

;; 4-numerics.watsup
def $ivshiftopsx_(shape : shape, def $f_(N : N, sx : sx, iN : iN(N), u32 : u32) : iN(N), sx : sx, vec_ : vec_(V128_Vnn), u32 : u32) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $ivshiftopsx_{Jnn : Jnn, M : M, def $f_(N : N, sx : sx, iN : iN(N), u32 : u32) : iN(N), sx : sx, v_1 : vec_(V128_Vnn), i : u32, `c*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, sx, v_1, i) = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c*{c <- `c*`} = $f_($lsizenn((Jnn : Jnn <: lanetype)), sx, c_1, i)*{c_1 <- `c_1*`})

;; 4-numerics.watsup
def $ivbitmaskop_(shape : shape, vec_ : vec_(V128_Vnn)) : u32
  ;; 4-numerics.watsup
  def $ivbitmaskop_{Jnn : Jnn, M : M, v_1 : vec_(V128_Vnn), c : iN(32), `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1) = $irev_(32, c)
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if ($ibits_(32, c) = `%`_bit($ilt_($lsizenn((Jnn : Jnn <: lanetype)), S_sx, c_1, `%`_iN(0))!`%`_u32.0)*{c_1 <- `c_1*`} ++ `%`_bit(0)^(((32 : nat <:> int) - (M : nat <:> int)) : int <:> nat){})

;; 4-numerics.watsup
def $ivswizzlop_(shape : shape, def $f_(N : N, iN(N)*, iN : iN(N)) : iN(N), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $ivswizzlop_{Jnn : Jnn, M : M, def $f_(N : N, iN(N)*, iN : iN(N)) : iN(N), v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), `c*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $f_, v_1, v_2) = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_2))
    -- if (c*{c <- `c*`} = $f_($lsizenn((Jnn : Jnn <: lanetype)), c_1*{c_1 <- `c_1*`}, c_2)*{c_2 <- `c_2*`})

;; 4-numerics.watsup
def $ivshufflop_(shape : shape, laneidx*, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $ivshufflop_{Jnn : Jnn, M : M, `i*` : laneidx*, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), `c*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))))*}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), i*{i <- `i*`}, v_1, v_2) = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c*{c <- `c*`})
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v_2))
    -- if (c*{c <- `c*`} = c_1*{c_1 <- `c_1*`} ++ c_2*{c_2 <- `c_2*`}[i!`%`_laneidx.0]*{i <- `i*`})

;; 4-numerics.watsup
def $vvunop_(vectype : vectype, vvunop : vvunop, vec_ : vec_(vectype)) : vec_(vectype)*
  ;; 4-numerics.watsup
  def $vvunop_{Vnn : Vnn, v : vec_(Vnn)}(Vnn, NOT_vvunop, v) = [$inot_($vsizenn(Vnn), v)]

;; 4-numerics.watsup
def $vvbinop_(vectype : vectype, vvbinop : vvbinop, vec_ : vec_(vectype), vec_ : vec_(vectype)) : vec_(vectype)*
  ;; 4-numerics.watsup
  def $vvbinop_{Vnn : Vnn, v_1 : vec_(Vnn), v_2 : vec_(Vnn)}(Vnn, AND_vvbinop, v_1, v_2) = [$iand_($vsizenn(Vnn), v_1, v_2)]
  ;; 4-numerics.watsup
  def $vvbinop_{Vnn : Vnn, v_1 : vec_(Vnn), v_2 : vec_(Vnn)}(Vnn, ANDNOT_vvbinop, v_1, v_2) = [$iandnot_($vsizenn(Vnn), v_1, v_2)]
  ;; 4-numerics.watsup
  def $vvbinop_{Vnn : Vnn, v_1 : vec_(Vnn), v_2 : vec_(Vnn)}(Vnn, OR_vvbinop, v_1, v_2) = [$ior_($vsizenn(Vnn), v_1, v_2)]
  ;; 4-numerics.watsup
  def $vvbinop_{Vnn : Vnn, v_1 : vec_(Vnn), v_2 : vec_(Vnn)}(Vnn, XOR_vvbinop, v_1, v_2) = [$ixor_($vsizenn(Vnn), v_1, v_2)]

;; 4-numerics.watsup
def $vvternop_(vectype : vectype, vvternop : vvternop, vec_ : vec_(vectype), vec_ : vec_(vectype), vec_ : vec_(vectype)) : vec_(vectype)*
  ;; 4-numerics.watsup
  def $vvternop_{Vnn : Vnn, v_1 : vec_(Vnn), v_2 : vec_(Vnn), v_3 : vec_(Vnn)}(Vnn, BITSELECT_vvternop, v_1, v_2, v_3) = [$ibitselect_($vsizenn(Vnn), v_1, v_2, v_3)]

;; 4-numerics.watsup
def $vunop_(shape : shape, vunop_ : vunop_(shape), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $vunop_{Fnn : Fnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), ABS_vunop_, v) = $fvunop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fabs_, v)
  ;; 4-numerics.watsup
  def $vunop_{Fnn : Fnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), NEG_vunop_, v) = $fvunop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fneg_, v)
  ;; 4-numerics.watsup
  def $vunop_{Fnn : Fnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), SQRT_vunop_, v) = $fvunop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fsqrt_, v)
  ;; 4-numerics.watsup
  def $vunop_{Fnn : Fnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), CEIL_vunop_, v) = $fvunop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fceil_, v)
  ;; 4-numerics.watsup
  def $vunop_{Fnn : Fnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), FLOOR_vunop_, v) = $fvunop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $ffloor_, v)
  ;; 4-numerics.watsup
  def $vunop_{Fnn : Fnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), TRUNC_vunop_, v) = $fvunop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $ftrunc_, v)
  ;; 4-numerics.watsup
  def $vunop_{Fnn : Fnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), NEAREST_vunop_, v) = $fvunop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fnearest_, v)
  ;; 4-numerics.watsup
  def $vunop_{Jnn : Jnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), ABS_vunop_, v) = $ivunop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $iabs_, v)
  ;; 4-numerics.watsup
  def $vunop_{Jnn : Jnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), NEG_vunop_, v) = $ivunop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $ineg_, v)
  ;; 4-numerics.watsup
  def $vunop_{Jnn : Jnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), POPCNT_vunop_, v) = $ivunop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $ipopcnt_, v)

;; 4-numerics.watsup
def $vbinop_(shape : shape, vbinop_ : vbinop_(shape), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $vbinop_{Jnn : Jnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), ADD_vbinop_, v_1, v_2) = $ivbinop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $iadd_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Jnn : Jnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), SUB_vbinop_, v_1, v_2) = $ivbinop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $isub_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Jnn : Jnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), MUL_vbinop_, v_1, v_2) = $ivbinop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $imul_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Jnn : Jnn, M : M, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), ADD_SAT_vbinop_(sx), v_1, v_2) = $ivbinopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $iadd_sat_, sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Jnn : Jnn, M : M, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), SUB_SAT_vbinop_(sx), v_1, v_2) = $ivbinopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $isub_sat_, sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Jnn : Jnn, M : M, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), MIN_vbinop_(sx), v_1, v_2) = $ivbinopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $imin_, sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Jnn : Jnn, M : M, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), MAX_vbinop_(sx), v_1, v_2) = $ivbinopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $imax_, sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Jnn : Jnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), `AVGRU`_vbinop_, v_1, v_2) = $ivbinopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $iavgr_, U_sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Jnn : Jnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), `Q15MULR_SATS`_vbinop_, v_1, v_2) = $ivbinopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $iq15mulr_sat_, S_sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Jnn : Jnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), `RELAXED_Q15MULRS`_vbinop_, v_1, v_2) = $ivbinopsxnd_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $irelaxed_q15mulr_, S_sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), ADD_vbinop_, v_1, v_2) = $fvbinop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fadd_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), SUB_vbinop_, v_1, v_2) = $fvbinop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fsub_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), MUL_vbinop_, v_1, v_2) = $fvbinop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fmul_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), DIV_vbinop_, v_1, v_2) = $fvbinop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fdiv_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), MIN_vbinop_, v_1, v_2) = $fvbinop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fmin_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), MAX_vbinop_, v_1, v_2) = $fvbinop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fmax_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), PMIN_vbinop_, v_1, v_2) = $fvbinop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fpmin_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), PMAX_vbinop_, v_1, v_2) = $fvbinop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fpmax_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), RELAXED_MIN_vbinop_, v_1, v_2) = $fvbinop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $frelaxed_min_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vbinop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), RELAXED_MAX_vbinop_, v_1, v_2) = $fvbinop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $frelaxed_max_, v_1, v_2)

;; 4-numerics.watsup
def $vternop_(shape : shape, vternop_ : vternop_(shape), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)*
  ;; 4-numerics.watsup
  def $vternop_{Jnn : Jnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), v_3 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), RELAXED_LANESELECT_vternop_, v_1, v_2, v_3) = $ivternopnd_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $irelaxed_laneselect_, v_1, v_2, v_3)
  ;; 4-numerics.watsup
  def $vternop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), v_3 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), RELAXED_MADD_vternop_, v_1, v_2, v_3) = $fvternop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $frelaxed_madd_, v_1, v_2, v_3)
  ;; 4-numerics.watsup
  def $vternop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), v_3 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), RELAXED_NMADD_vternop_, v_1, v_2, v_3) = $fvternop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $frelaxed_nmadd_, v_1, v_2, v_3)

;; 4-numerics.watsup
def $vtestop_(shape : shape, vtestop_ : vtestop_(shape), vec_ : vec_(V128_Vnn)) : u32
  ;; 4-numerics.watsup
  def $vtestop_{Jnn : Jnn, M : M, v : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), ALL_TRUE_vtestop_, v) = $ivtestop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $inez_, v)

;; 4-numerics.watsup
def $vrelop_(shape : shape, vrelop_ : vrelop_(shape), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $vrelop_{Jnn : Jnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), EQ_vrelop_, v_1, v_2) = $ivrelop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $ieq_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Jnn : Jnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), NE_vrelop_, v_1, v_2) = $ivrelop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $ine_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Jnn : Jnn, M : M, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), LT_vrelop_(sx), v_1, v_2) = $ivrelopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $ilt_, sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Jnn : Jnn, M : M, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), GT_vrelop_(sx), v_1, v_2) = $ivrelopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $igt_, sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Jnn : Jnn, M : M, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), LE_vrelop_(sx), v_1, v_2) = $ivrelopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $ile_, sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Jnn : Jnn, M : M, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), GE_vrelop_(sx), v_1, v_2) = $ivrelopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $ige_, sx, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), EQ_vrelop_, v_1, v_2) = $fvrelop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $feq_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), NE_vrelop_, v_1, v_2) = $fvrelop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fne_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), LT_vrelop_, v_1, v_2) = $fvrelop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $flt_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), GT_vrelop_, v_1, v_2) = $fvrelop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fgt_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), LE_vrelop_, v_1, v_2) = $fvrelop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fle_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vrelop_{Fnn : Fnn, M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), GE_vrelop_, v_1, v_2) = $fvrelop_(`%X%`_shape((Fnn : Fnn <: lanetype), `%`_dim(M)), def $fge_, v_1, v_2)

;; 4-numerics.watsup
def $lcvtop__(shape_1 : shape, shape_2 : shape, vcvtop__ : vcvtop__(shape_1, shape_2), lane_ : lane_($lanetype(shape_1))) : lane_($lanetype(shape_2))*
  ;; 4-numerics.watsup
  def $lcvtop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, sx : sx, c_1 : lane_($lanetype(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)))), c : lane_($lanetype(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))))}(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), EXTEND_vcvtop__(sx), c_1) = [c]
    -- if (c = $extend__($lsizenn1((Jnn_1 : Jnn <: lanetype)), $lsizenn2((Jnn_2 : Jnn <: lanetype)), sx, c_1))
  ;; 4-numerics.watsup
  def $lcvtop__{Jnn_1 : Jnn, M_1 : M, Fnn_2 : Fnn, M_2 : M, sx : sx, c_1 : lane_($lanetype(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)))), c : lane_($lanetype(`%X%`_shape((Fnn_2 : Fnn <: lanetype), `%`_dim(M_2))))}(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Fnn_2 : Fnn <: lanetype), `%`_dim(M_2)), CONVERT_vcvtop__(sx), c_1) = [c]
    -- if (c = $convert__($lsizenn1((Jnn_1 : Jnn <: lanetype)), $lsizenn2((Fnn_2 : Fnn <: lanetype)), sx, c_1))
  ;; 4-numerics.watsup
  def $lcvtop__{Fnn_1 : Fnn, M_1 : M, Inn_2 : Inn, M_2 : M, sx : sx, c_1 : lane_($lanetype(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)))), `c?` : lane_($lanetype(`%X%`_shape((Inn_2 : Inn <: lanetype), `%`_dim(M_2))))?}(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Inn_2 : Inn <: lanetype), `%`_dim(M_2)), TRUNC_SAT_vcvtop__(sx), c_1) = lift(c?{c <- `c?`})
    -- if (c?{c <- `c?`} = $trunc_sat__($lsizenn1((Fnn_1 : Fnn <: lanetype)), $lsizenn2((Inn_2 : Inn <: lanetype)), sx, c_1))
  ;; 4-numerics.watsup
  def $lcvtop__{Fnn_1 : Fnn, M_1 : M, Inn_2 : Inn, M_2 : M, sx : sx, c_1 : lane_($lanetype(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)))), `c?` : lane_($lanetype(`%X%`_shape((Inn_2 : Inn <: lanetype), `%`_dim(M_2))))?}(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Inn_2 : Inn <: lanetype), `%`_dim(M_2)), RELAXED_TRUNC_vcvtop__(sx), c_1) = lift(c?{c <- `c?`})
    -- if (c?{c <- `c?`} = $relaxed_trunc__($lsizenn1((Fnn_1 : Fnn <: lanetype)), $lsizenn2((Inn_2 : Inn <: lanetype)), sx, c_1))
  ;; 4-numerics.watsup
  def $lcvtop__{Fnn_1 : Fnn, M_1 : M, Fnn_2 : Fnn, M_2 : M, c_1 : lane_($lanetype(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)))), `c*` : lane_($lanetype(`%X%`_shape((Fnn_2 : Fnn <: lanetype), `%`_dim(M_2))))*}(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Fnn_2 : Fnn <: lanetype), `%`_dim(M_2)), DEMOTE_vcvtop__, c_1) = c*{c <- `c*`}
    -- if (c*{c <- `c*`} = $demote__($lsizenn1((Fnn_1 : Fnn <: lanetype)), $lsizenn2((Fnn_2 : Fnn <: lanetype)), c_1))
  ;; 4-numerics.watsup
  def $lcvtop__{Fnn_1 : Fnn, M_1 : M, Fnn_2 : Fnn, M_2 : M, c_1 : lane_($lanetype(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)))), `c*` : lane_($lanetype(`%X%`_shape((Fnn_2 : Fnn <: lanetype), `%`_dim(M_2))))*}(`%X%`_shape((Fnn_1 : Fnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Fnn_2 : Fnn <: lanetype), `%`_dim(M_2)), PROMOTE_vcvtop__, c_1) = c*{c <- `c*`}
    -- if (c*{c <- `c*`} = $promote__($lsizenn1((Fnn_1 : Fnn <: lanetype)), $lsizenn2((Fnn_2 : Fnn <: lanetype)), c_1))

;; 4-numerics.watsup
def $vcvtop__(shape_1 : shape, shape_2 : shape, vcvtop__ : vcvtop__(shape_1, shape_2), half__(shape_1, shape_2)?, zero__(shape_1, shape_2)?, vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $vcvtop__{Lnn_1 : Lnn, M : M, Lnn_2 : Lnn, vcvtop : vcvtop__(`%X%`_shape(Lnn_1, `%`_dim(M)), `%X%`_shape(Lnn_2, `%`_dim(M))), v_1 : vec_(V128_Vnn), v : vec_(V128_Vnn), `c_1*` : lane_($lanetype(`%X%`_shape(Lnn_1, `%`_dim(M))))*, `c**` : lane_(Lnn_2)**}(`%X%`_shape(Lnn_1, `%`_dim(M)), `%X%`_shape(Lnn_2, `%`_dim(M)), vcvtop, ?(), ?(), v_1) = v
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape(Lnn_1, `%`_dim(M)), v_1))
    -- if (c*{c <- `c*`}*{`c*` <- `c**`} = $setproduct_(syntax lane_(Lnn_2), $lcvtop__(`%X%`_shape(Lnn_1, `%`_dim(M)), `%X%`_shape(Lnn_2, `%`_dim(M)), vcvtop, c_1)*{c_1 <- `c_1*`}))
    -- if v <- $invlanes_(`%X%`_shape(Lnn_2, `%`_dim(M)), c*{c <- `c*`})*{`c*` <- `c**`}
  ;; 4-numerics.watsup
  def $vcvtop__{Lnn_1 : Lnn, M_1 : M, Lnn_2 : Lnn, M_2 : M, vcvtop : vcvtop__(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape(Lnn_2, `%`_dim(M_2))), half : half__(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape(Lnn_2, `%`_dim(M_2))), v_1 : vec_(V128_Vnn), v : vec_(V128_Vnn), `c_1*` : lane_($lanetype(`%X%`_shape(Lnn_1, `%`_dim(M_1))))*, `c**` : lane_(Lnn_2)**}(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape(Lnn_2, `%`_dim(M_2)), vcvtop, ?(half), ?(), v_1) = v
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape(Lnn_1, `%`_dim(M_1)), v_1)[$half__(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape(Lnn_2, `%`_dim(M_2)), half, 0, M_2) : M_2])
    -- if (c*{c <- `c*`}*{`c*` <- `c**`} = $setproduct_(syntax lane_(Lnn_2), $lcvtop__(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape(Lnn_2, `%`_dim(M_2)), vcvtop, c_1)*{c_1 <- `c_1*`}))
    -- if v <- $invlanes_(`%X%`_shape(Lnn_2, `%`_dim(M_2)), c*{c <- `c*`})*{`c*` <- `c**`}
  ;; 4-numerics.watsup
  def $vcvtop__{Lnn_1 : Lnn, M_1 : M, Lnn_2 : Lnn, M_2 : M, vcvtop : vcvtop__(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape(Lnn_2, `%`_dim(M_2))), zero : zero__(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape(Lnn_2, `%`_dim(M_2))), v_1 : vec_(V128_Vnn), v : vec_(V128_Vnn), `c_1*` : lane_($lanetype(`%X%`_shape(Lnn_1, `%`_dim(M_1))))*, `c**` : lane_(Lnn_2)**}(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape(Lnn_2, `%`_dim(M_2)), vcvtop, ?(), ?(zero), v_1) = v
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape(Lnn_1, `%`_dim(M_1)), v_1))
    -- if (c*{c <- `c*`}*{`c*` <- `c**`} = $setproduct_(syntax lane_(Lnn_2), $lcvtop__(`%X%`_shape(Lnn_1, `%`_dim(M_1)), `%X%`_shape(Lnn_2, `%`_dim(M_2)), vcvtop, c_1)*{c_1 <- `c_1*`} ++ [$zero(Lnn_2)]^M_1{}))
    -- if v <- $invlanes_(`%X%`_shape(Lnn_2, `%`_dim(M_2)), c*{c <- `c*`})*{`c*` <- `c**`}

;; 4-numerics.watsup
def $vshiftop_(ishape : ishape, vshiftop_ : vshiftop_(ishape), vec_ : vec_(V128_Vnn), u32 : u32) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $vshiftop_{Jnn : Jnn, M : M, v : vec_(V128_Vnn), i : u32}(`%`_ishape(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))), SHL_vshiftop_, v, i) = $ivshiftop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $ishl_, v, i)
  ;; 4-numerics.watsup
  def $vshiftop_{Jnn : Jnn, M : M, sx : sx, v : vec_(V128_Vnn), i : u32}(`%`_ishape(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))), SHR_vshiftop_(sx), v, i) = $ivshiftopsx_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), def $ishr_, sx, v, i)

;; 4-numerics.watsup
def $vbitmaskop_(ishape : ishape, vec_ : vec_(V128_Vnn)) : u32
  ;; 4-numerics.watsup
  def $vbitmaskop_{Jnn : Jnn, M : M, v : vec_(V128_Vnn)}(`%`_ishape(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))), v) = $ivbitmaskop_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), v)

;; 4-numerics.watsup
def $vswizzlop_(bshape : bshape, vswizzlop_ : vswizzlop_(bshape), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $vswizzlop_{M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%`_bshape(`%X%`_shape(I8_lanetype, `%`_dim(M))), SWIZZLE_vswizzlop_, v_1, v_2) = $ivswizzlop_(`%X%`_shape(I8_lanetype, `%`_dim(M)), def $iswizzle_lane_, v_1, v_2)
  ;; 4-numerics.watsup
  def $vswizzlop_{M : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%`_bshape(`%X%`_shape(I8_lanetype, `%`_dim(M))), RELAXED_SWIZZLE_vswizzlop_, v_1, v_2) = $ivswizzlop_(`%X%`_shape(I8_lanetype, `%`_dim(M)), def $irelaxed_swizzle_lane_, v_1, v_2)

;; 4-numerics.watsup
def $vshufflop_(bshape : bshape, laneidx*, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $vshufflop_{M : M, `i*` : laneidx*, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%`_bshape(`%X%`_shape(I8_lanetype, `%`_dim(M))), i*{i <- `i*`}, v_1, v_2) = $ivshufflop_(`%X%`_shape(I8_lanetype, `%`_dim(M)), i*{i <- `i*`}, v_1, v_2)

;; 4-numerics.watsup
def $vnarrowop__(shape_1 : shape, shape_2 : shape, sx : sx, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $vnarrowop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, sx : sx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), v : vec_(V128_Vnn), `c_1*` : lane_($lanetype(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))))*, `c'_1*` : iN($lsize((Jnn_2 : Jnn <: lanetype)))*, `c'_2*` : iN($lsize((Jnn_2 : Jnn <: lanetype)))*}(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), sx, v_1, v_2) = v
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), v_1))
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), v_2))
    -- if (c'_1*{c'_1 <- `c'_1*`} = $narrow__($lsize((Jnn_1 : Jnn <: lanetype)), $lsize((Jnn_2 : Jnn <: lanetype)), sx, c_1)*{c_1 <- `c_1*`})
    -- if (c'_2*{c'_2 <- `c'_2*`} = $narrow__($lsize((Jnn_1 : Jnn <: lanetype)), $lsize((Jnn_2 : Jnn <: lanetype)), sx, c_2)*{c_2 <- `c_2*`})
    -- if (v = $invlanes_(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), c'_1*{c'_1 <- `c'_1*`} ++ c'_2*{c'_2 <- `c'_2*`}))

;; 4-numerics.watsup
def $ivadd_pairwise_(N : N, iN(N)*) : iN(N)*
  ;; 4-numerics.watsup
  def $ivadd_pairwise_{N : N, `i*` : iN(N)*, `j_1*` : iN(N)*, `j_2*` : iN(N)*}(N, i*{i <- `i*`}) = $iadd_(N, j_1, j_2)*{j_1 <- `j_1*`, j_2 <- `j_2*`}
    -- if ($concat_(syntax N, [j_1!`%`_iN.0 j_2!`%`_iN.0]*{j_1 <- `j_1*`, j_2 <- `j_2*`}) = i!`%`_iN.0*{i <- `i*`})

;; 4-numerics.watsup
def $ivextunop__(shape_1 : shape, shape_2 : shape, def $f_(N : N, iN(N)*) : iN(N)*, sx : sx, vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $ivextunop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, def $f_(N : N, iN(N)*) : iN(N)*, sx : sx, v_1 : vec_(V128_Vnn), `c*` : lane_($lanetype(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))))*, `c'_1*` : iN($lsizenn2((Jnn_2 : Jnn <: lanetype)))*}(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), def $f_, sx, v_1) = $invlanes_(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), c*{c <- `c*`})
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), v_1))
    -- if (c'_1*{c'_1 <- `c'_1*`} = $extend__($lsizenn1((Jnn_1 : Jnn <: lanetype)), $lsizenn2((Jnn_2 : Jnn <: lanetype)), sx, c_1)*{c_1 <- `c_1*`})
    -- if (c*{c <- `c*`} = $f_($lsizenn2((Jnn_2 : Jnn <: lanetype)), c'_1*{c'_1 <- `c'_1*`}))

;; 4-numerics.watsup
def $vextunop__(ishape_1 : ishape, ishape_2 : ishape, vextunop__ : vextunop__(ishape_1, ishape_2), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $vextunop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, sx : sx, v_1 : vec_(V128_Vnn)}(`%`_ishape(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))), `%`_ishape(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))), EXTADD_PAIRWISE_vextunop__(sx), v_1) = $ivextunop__(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), def $ivadd_pairwise_, sx, v_1)

;; 4-numerics.watsup
def $ivdot_(N : N, iN(N)*, iN(N)*) : iN(N)*
  ;; 4-numerics.watsup
  def $ivdot_{N : N, `i_1*` : iN(N)*, `i_2*` : iN(N)*, `j_1*` : iN(N)*, `j_2*` : iN(N)*}(N, i_1*{i_1 <- `i_1*`}, i_2*{i_2 <- `i_2*`}) = $iadd_(N, j_1, j_2)*{j_1 <- `j_1*`, j_2 <- `j_2*`}
    -- if ($concat_(syntax iN(N), [j_1 j_2]*{j_1 <- `j_1*`, j_2 <- `j_2*`}) = $imul_(N, i_1, i_2)*{i_1 <- `i_1*`, i_2 <- `i_2*`})

;; 4-numerics.watsup
def $ivdot_sat_(N : N, iN(N)*, iN(N)*) : iN(N)*
  ;; 4-numerics.watsup
  def $ivdot_sat_{N : N, `i_1*` : iN(N)*, `i_2*` : iN(N)*, `j_1*` : iN(N)*, `j_2*` : iN(N)*}(N, i_1*{i_1 <- `i_1*`}, i_2*{i_2 <- `i_2*`}) = $iadd_sat_(N, S_sx, j_1, j_2)*{j_1 <- `j_1*`, j_2 <- `j_2*`}
    -- if ($concat_(syntax iN(N), [j_1 j_2]*{j_1 <- `j_1*`, j_2 <- `j_2*`}) = $imul_(N, i_1, i_2)*{i_1 <- `i_1*`, i_2 <- `i_2*`})

;; 4-numerics.watsup
def $ivextbinop__(shape_1 : shape, shape_2 : shape, def $f_(N : N, iN(N)*, iN(N)*) : iN(N)*, sx : sx, sx : sx, laneidx : laneidx, laneidx : laneidx, vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $ivextbinop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, def $f_(N : N, iN(N)*, iN(N)*) : iN(N)*, sx_1 : sx, sx_2 : sx, i : laneidx, k : laneidx, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), `c*` : lane_($lanetype(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))))*, `c_1*` : lane_($lanetype(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))))*, `c_2*` : lane_($lanetype(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))))*, `c'_1*` : iN($lsizenn2((Jnn_2 : Jnn <: lanetype)))*, `c'_2*` : iN($lsizenn2((Jnn_2 : Jnn <: lanetype)))*}(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), def $f_, sx_1, sx_2, i, k, v_1, v_2) = $invlanes_(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), c*{c <- `c*`})
    -- if (c_1*{c_1 <- `c_1*`} = $lanes_(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), v_1)[i!`%`_laneidx.0 : k!`%`_laneidx.0])
    -- if (c_2*{c_2 <- `c_2*`} = $lanes_(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), v_2)[i!`%`_laneidx.0 : k!`%`_laneidx.0])
    -- if (c'_1*{c'_1 <- `c'_1*`} = $extend__($lsizenn1((Jnn_1 : Jnn <: lanetype)), $lsizenn2((Jnn_2 : Jnn <: lanetype)), sx_1, c_1)*{c_1 <- `c_1*`})
    -- if (c'_2*{c'_2 <- `c'_2*`} = $extend__($lsizenn1((Jnn_1 : Jnn <: lanetype)), $lsizenn2((Jnn_2 : Jnn <: lanetype)), sx_2, c_2)*{c_2 <- `c_2*`})
    -- if (c*{c <- `c*`} = $f_($lsizenn2((Jnn_2 : Jnn <: lanetype)), c'_1*{c'_1 <- `c'_1*`}, c'_2*{c'_2 <- `c'_2*`}))

;; 4-numerics.watsup
def $ivmul_(N : N, iN(N)*, iN(N)*) : iN(N)*
  ;; 4-numerics.watsup
  def $ivmul_{N : N, `i_1*` : iN(N)*, `i_2*` : iN(N)*}(N, i_1*{i_1 <- `i_1*`}, i_2*{i_2 <- `i_2*`}) = $imul_(N, i_1, i_2)*{i_1 <- `i_1*`, i_2 <- `i_2*`}

;; 4-numerics.watsup
def $vextbinop__(ishape_1 : ishape, ishape_2 : ishape, vextbinop__ : vextbinop__(ishape_1, ishape_2), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $vextbinop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, sx : sx, half : half__(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))), v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn), i : laneidx}(`%`_ishape(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))), `%`_ishape(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))), EXTMUL_vextbinop__(sx, half), v_1, v_2) = $ivextbinop__(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), def $ivmul_, sx, sx, i, `%`_laneidx(M_2), v_1, v_2)
    -- if (i!`%`_laneidx.0 = $half__(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), half, 0, M_2))
  ;; 4-numerics.watsup
  def $vextbinop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%`_ishape(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))), `%`_ishape(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))), `DOTS`_vextbinop__, v_1, v_2) = $ivextbinop__(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), def $ivdot_, S_sx, S_sx, `%`_laneidx(0), `%`_laneidx(M_1), v_1, v_2)
  ;; 4-numerics.watsup
  def $vextbinop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, v_1 : vec_(V128_Vnn), v_2 : vec_(V128_Vnn)}(`%`_ishape(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))), `%`_ishape(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))), `RELAXED_DOTS`_vextbinop__, v_1, v_2) = $ivextbinop__(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1)), `%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), def $ivdot_sat_, S_sx, $relaxed2($R_idot, syntax sx, S_sx, U_sx), `%`_laneidx(0), `%`_laneidx(M_1), v_1, v_2)

;; 4-numerics.watsup
def $vextternop__(ishape_1 : ishape, ishape_2 : ishape, vextternop__ : vextternop__(ishape_1, ishape_2), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn), vec_ : vec_(V128_Vnn)) : vec_(V128_Vnn)
  ;; 4-numerics.watsup
  def $vextternop__{Jnn_1 : Jnn, M_1 : M, Jnn_2 : Jnn, M_2 : M, c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), c_3 : vec_(V128_Vnn), c : vec_(V128_Vnn), Jnn : Jnn, M : M, c' : vec_(V128_Vnn), c'' : vec_(V128_Vnn)}(`%`_ishape(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))), `%`_ishape(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))), `RELAXED_DOT_ADDS`_vextternop__, c_1, c_2, c_3) = c
    -- if ($lsizenn((Jnn : Jnn <: lanetype)) = (2 * $lsizenn1((Jnn_1 : Jnn <: lanetype))))
    -- if (M = (2 * M_2))
    -- if (c' = $vextbinop__(`%`_ishape(`%X%`_shape((Jnn_1 : Jnn <: lanetype), `%`_dim(M_1))), `%`_ishape(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))), `RELAXED_DOTS`_vextbinop__, c_1, c_2))
    -- if (c'' = $vextunop__(`%`_ishape(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M))), `%`_ishape(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2))), EXTADD_PAIRWISE_vextunop__(S_sx), c'))
    -- if c <- $vbinop_(`%X%`_shape((Jnn_2 : Jnn <: lanetype), `%`_dim(M_2)), ADD_vbinop_, c'', c_3)

;; 5-runtime.watsup
syntax num =
  | CONST{numtype : numtype, num_ : num_(numtype)}(numtype : numtype, num_ : num_(numtype))

;; 5-runtime.watsup
syntax vec =
  | VCONST{vectype : vectype, vec_ : vec_(vectype)}(vectype : vectype, vec_ : vec_(vectype))

;; 5-runtime.watsup
syntax ref =
  | REF.I31_NUM{u31 : u31}(u31 : u31)
  | REF.STRUCT_ADDR{structaddr : structaddr}(structaddr : structaddr)
  | REF.ARRAY_ADDR{arrayaddr : arrayaddr}(arrayaddr : arrayaddr)
  | REF.FUNC_ADDR{funcaddr : funcaddr}(funcaddr : funcaddr)
  | REF.EXN_ADDR{exnaddr : exnaddr}(exnaddr : exnaddr)
  | REF.HOST_ADDR{hostaddr : hostaddr}(hostaddr : hostaddr)
  | REF.EXTERN{addrref : addrref}(addrref : addrref)
  | REF.NULL{heaptype : heaptype}(heaptype : heaptype)

;; 5-runtime.watsup
syntax result =
  | _VALS{`val*` : val*}(val*{val <- `val*`} : val*)
  | `(REF.EXN_ADDR%)THROW_REF`{exnaddr : exnaddr}(exnaddr : exnaddr)
  | TRAP

;; 5-runtime.watsup
syntax hostfunc =
  | `...`

;; 5-runtime.watsup
syntax funccode =
  | FUNC{typeidx : typeidx, `local*` : local*, expr : expr}(typeidx : typeidx, local*{local <- `local*`} : local*, expr : expr)
  | `...`

;; 5-runtime.watsup
syntax funcinst =
{
  TYPE{deftype : deftype} deftype,
  MODULE{moduleinst : moduleinst} moduleinst,
  CODE{funccode : funccode} funccode
}

;; 5-runtime.watsup
syntax globalinst =
{
  TYPE{globaltype : globaltype} globaltype,
  VALUE{val : val} val
}

;; 5-runtime.watsup
syntax tableinst =
{
  TYPE{tabletype : tabletype} tabletype,
  REFS{`ref*` : ref*} ref*
}

;; 5-runtime.watsup
syntax meminst =
{
  TYPE{memtype : memtype} memtype,
  BYTES{`byte*` : byte*} byte*
}

;; 5-runtime.watsup
syntax taginst =
{
  TYPE{tagtype : tagtype} tagtype
}

;; 5-runtime.watsup
syntax eleminst =
{
  TYPE{elemtype : elemtype} elemtype,
  REFS{`ref*` : ref*} ref*
}

;; 5-runtime.watsup
syntax datainst =
{
  BYTES{`byte*` : byte*} byte*
}

;; 5-runtime.watsup
syntax packval =
  | PACK{packtype : packtype, iN : iN($psizenn(packtype))}(packtype : packtype, iN : iN($psizenn(packtype)))

;; 5-runtime.watsup
syntax fieldval =
  | CONST{numtype : numtype, num_ : num_(numtype)}(numtype : numtype, num_ : num_(numtype))
  | VCONST{vectype : vectype, vec_ : vec_(vectype)}(vectype : vectype, vec_ : vec_(vectype))
  | REF.NULL{heaptype : heaptype}(heaptype : heaptype)
  | REF.I31_NUM{u31 : u31}(u31 : u31)
  | REF.STRUCT_ADDR{structaddr : structaddr}(structaddr : structaddr)
  | REF.ARRAY_ADDR{arrayaddr : arrayaddr}(arrayaddr : arrayaddr)
  | REF.FUNC_ADDR{funcaddr : funcaddr}(funcaddr : funcaddr)
  | REF.EXN_ADDR{exnaddr : exnaddr}(exnaddr : exnaddr)
  | REF.HOST_ADDR{hostaddr : hostaddr}(hostaddr : hostaddr)
  | REF.EXTERN{addrref : addrref}(addrref : addrref)
  | PACK{packtype : packtype, iN : iN($psizenn(packtype))}(packtype : packtype, iN : iN($psizenn(packtype)))

;; 5-runtime.watsup
syntax structinst =
{
  TYPE{deftype : deftype} deftype,
  FIELDS{`fieldval*` : fieldval*} fieldval*
}

;; 5-runtime.watsup
syntax arrayinst =
{
  TYPE{deftype : deftype} deftype,
  FIELDS{`fieldval*` : fieldval*} fieldval*
}

;; 5-runtime.watsup
syntax exninst =
{
  TAG{tagaddr : tagaddr} tagaddr,
  FIELDS{`val*` : val*} val*
}

;; 5-runtime.watsup
syntax store =
{
  FUNCS{`funcinst*` : funcinst*} funcinst*,
  GLOBALS{`globalinst*` : globalinst*} globalinst*,
  TABLES{`tableinst*` : tableinst*} tableinst*,
  MEMS{`meminst*` : meminst*} meminst*,
  TAGS{`taginst*` : taginst*} taginst*,
  ELEMS{`eleminst*` : eleminst*} eleminst*,
  DATAS{`datainst*` : datainst*} datainst*,
  STRUCTS{`structinst*` : structinst*} structinst*,
  ARRAYS{`arrayinst*` : arrayinst*} arrayinst*,
  EXNS{`exninst*` : exninst*} exninst*
}

;; 5-runtime.watsup
syntax state =
  | `%;%`{store : store, frame : frame}(store : store, frame : frame)

;; 5-runtime.watsup
syntax config =
  | `%;%`{state : state, `instr*` : instr*}(state : state, instr*{instr <- `instr*`} : instr*)

;; 6-runtime-aux.watsup
def $inst_valtype(moduleinst : moduleinst, valtype : valtype) : valtype
  ;; 6-runtime-aux.watsup
  def $inst_valtype{moduleinst : moduleinst, t : valtype, `dt*` : deftype*}(moduleinst, t) = $subst_all_valtype(t, (dt : deftype <: heaptype)*{dt <- `dt*`})
    -- if (dt*{dt <- `dt*`} = moduleinst.TYPES_moduleinst)

;; 6-runtime-aux.watsup
def $inst_reftype(moduleinst : moduleinst, reftype : reftype) : reftype
  ;; 6-runtime-aux.watsup
  def $inst_reftype{moduleinst : moduleinst, rt : reftype, `dt*` : deftype*}(moduleinst, rt) = $subst_all_reftype(rt, (dt : deftype <: heaptype)*{dt <- `dt*`})
    -- if (dt*{dt <- `dt*`} = moduleinst.TYPES_moduleinst)

;; 6-runtime-aux.watsup
def $inst_globaltype(moduleinst : moduleinst, globaltype : globaltype) : globaltype
  ;; 6-runtime-aux.watsup
  def $inst_globaltype{moduleinst : moduleinst, gt : globaltype, `dt*` : deftype*}(moduleinst, gt) = $subst_all_globaltype(gt, (dt : deftype <: heaptype)*{dt <- `dt*`})
    -- if (dt*{dt <- `dt*`} = moduleinst.TYPES_moduleinst)

;; 6-runtime-aux.watsup
def $inst_tabletype(moduleinst : moduleinst, tabletype : tabletype) : tabletype
  ;; 6-runtime-aux.watsup
  def $inst_tabletype{moduleinst : moduleinst, tt : tabletype, `dt*` : deftype*}(moduleinst, tt) = $subst_all_tabletype(tt, (dt : deftype <: heaptype)*{dt <- `dt*`})
    -- if (dt*{dt <- `dt*`} = moduleinst.TYPES_moduleinst)

;; 6-runtime-aux.watsup
def $inst_memtype(moduleinst : moduleinst, memtype : memtype) : memtype
  ;; 6-runtime-aux.watsup
  def $inst_memtype{moduleinst : moduleinst, mt : memtype, `dt*` : deftype*}(moduleinst, mt) = $subst_all_memtype(mt, (dt : deftype <: heaptype)*{dt <- `dt*`})
    -- if (dt*{dt <- `dt*`} = moduleinst.TYPES_moduleinst)

;; 6-runtime-aux.watsup
def $Ki : nat
  ;; 6-runtime-aux.watsup
  def $Ki = 1024

;; 6-runtime-aux.watsup
def $packfield_(storagetype : storagetype, val : val) : fieldval
  ;; 6-runtime-aux.watsup
  def $packfield_{valtype : valtype, val : val}((valtype : valtype <: storagetype), val) = (val : val <: fieldval)
  ;; 6-runtime-aux.watsup
  def $packfield_{packtype : packtype, i : num_(I32_numtype)}((packtype : packtype <: storagetype), CONST_val(I32_numtype, i)) = PACK_fieldval(packtype, $wrap__(32, $psize(packtype), i))

;; 6-runtime-aux.watsup
def $unpackfield_(storagetype : storagetype, sx?, fieldval : fieldval) : val
  ;; 6-runtime-aux.watsup
  def $unpackfield_{valtype : valtype, val : val}((valtype : valtype <: storagetype), ?(), (val : val <: fieldval)) = val
  ;; 6-runtime-aux.watsup
  def $unpackfield_{packtype : packtype, sx : sx, i : iN($psizenn(packtype))}((packtype : packtype <: storagetype), ?(sx), PACK_fieldval(packtype, i)) = CONST_val(I32_numtype, $extend__($psize(packtype), 32, sx, i))

;; 6-runtime-aux.watsup
rec {

;; 6-runtime-aux.watsup:66.1-66.87
def $funcsxa(externaddr*) : funcaddr*
  ;; 6-runtime-aux.watsup:72.1-72.24
  def $funcsxa([]) = []
  ;; 6-runtime-aux.watsup:73.1-73.45
  def $funcsxa{a : addr, `xa*` : externaddr*}([FUNC_externaddr(a)] ++ xa*{xa <- `xa*`}) = [a] ++ $funcsxa(xa*{xa <- `xa*`})
  ;; 6-runtime-aux.watsup:74.1-74.59
  def $funcsxa{externaddr : externaddr, `xa*` : externaddr*}([externaddr] ++ xa*{xa <- `xa*`}) = $funcsxa(xa*{xa <- `xa*`})
    -- otherwise
}

;; 6-runtime-aux.watsup
rec {

;; 6-runtime-aux.watsup:67.1-67.89
def $globalsxa(externaddr*) : globaladdr*
  ;; 6-runtime-aux.watsup:76.1-76.26
  def $globalsxa([]) = []
  ;; 6-runtime-aux.watsup:77.1-77.51
  def $globalsxa{a : addr, `xa*` : externaddr*}([GLOBAL_externaddr(a)] ++ xa*{xa <- `xa*`}) = [a] ++ $globalsxa(xa*{xa <- `xa*`})
  ;; 6-runtime-aux.watsup:78.1-78.63
  def $globalsxa{externaddr : externaddr, `xa*` : externaddr*}([externaddr] ++ xa*{xa <- `xa*`}) = $globalsxa(xa*{xa <- `xa*`})
    -- otherwise
}

;; 6-runtime-aux.watsup
rec {

;; 6-runtime-aux.watsup:68.1-68.88
def $tablesxa(externaddr*) : tableaddr*
  ;; 6-runtime-aux.watsup:80.1-80.25
  def $tablesxa([]) = []
  ;; 6-runtime-aux.watsup:81.1-81.48
  def $tablesxa{a : addr, `xa*` : externaddr*}([TABLE_externaddr(a)] ++ xa*{xa <- `xa*`}) = [a] ++ $tablesxa(xa*{xa <- `xa*`})
  ;; 6-runtime-aux.watsup:82.1-82.61
  def $tablesxa{externaddr : externaddr, `xa*` : externaddr*}([externaddr] ++ xa*{xa <- `xa*`}) = $tablesxa(xa*{xa <- `xa*`})
    -- otherwise
}

;; 6-runtime-aux.watsup
rec {

;; 6-runtime-aux.watsup:69.1-69.86
def $memsxa(externaddr*) : memaddr*
  ;; 6-runtime-aux.watsup:84.1-84.23
  def $memsxa([]) = []
  ;; 6-runtime-aux.watsup:85.1-85.42
  def $memsxa{a : addr, `xa*` : externaddr*}([MEM_externaddr(a)] ++ xa*{xa <- `xa*`}) = [a] ++ $memsxa(xa*{xa <- `xa*`})
  ;; 6-runtime-aux.watsup:86.1-86.57
  def $memsxa{externaddr : externaddr, `xa*` : externaddr*}([externaddr] ++ xa*{xa <- `xa*`}) = $memsxa(xa*{xa <- `xa*`})
    -- otherwise
}

;; 6-runtime-aux.watsup
rec {

;; 6-runtime-aux.watsup:70.1-70.86
def $tagsxa(externaddr*) : tagaddr*
  ;; 6-runtime-aux.watsup:88.1-88.23
  def $tagsxa([]) = []
  ;; 6-runtime-aux.watsup:89.1-89.42
  def $tagsxa{a : addr, `xa*` : externaddr*}([TAG_externaddr(a)] ++ xa*{xa <- `xa*`}) = [a] ++ $tagsxa(xa*{xa <- `xa*`})
  ;; 6-runtime-aux.watsup:90.1-90.57
  def $tagsxa{externaddr : externaddr, `xa*` : externaddr*}([externaddr] ++ xa*{xa <- `xa*`}) = $tagsxa(xa*{xa <- `xa*`})
    -- otherwise
}

;; 6-runtime-aux.watsup
def $store(state : state) : store
  ;; 6-runtime-aux.watsup
  def $store{s : store, f : frame}(`%;%`_state(s, f)) = s

;; 6-runtime-aux.watsup
def $frame(state : state) : frame
  ;; 6-runtime-aux.watsup
  def $frame{s : store, f : frame}(`%;%`_state(s, f)) = f

;; 6-runtime-aux.watsup
def $tagaddr(state : state) : tagaddr*
  ;; 6-runtime-aux.watsup
  def $tagaddr{s : store, f : frame}(`%;%`_state(s, f)) = f.MODULE_frame.TAGS_moduleinst

;; 6-runtime-aux.watsup
def $moduleinst(state : state) : moduleinst
  ;; 6-runtime-aux.watsup
  def $moduleinst{s : store, f : frame}(`%;%`_state(s, f)) = f.MODULE_frame

;; 6-runtime-aux.watsup
def $funcinst(state : state) : funcinst*
  ;; 6-runtime-aux.watsup
  def $funcinst{s : store, f : frame}(`%;%`_state(s, f)) = s.FUNCS_store

;; 6-runtime-aux.watsup
def $globalinst(state : state) : globalinst*
  ;; 6-runtime-aux.watsup
  def $globalinst{s : store, f : frame}(`%;%`_state(s, f)) = s.GLOBALS_store

;; 6-runtime-aux.watsup
def $tableinst(state : state) : tableinst*
  ;; 6-runtime-aux.watsup
  def $tableinst{s : store, f : frame}(`%;%`_state(s, f)) = s.TABLES_store

;; 6-runtime-aux.watsup
def $meminst(state : state) : meminst*
  ;; 6-runtime-aux.watsup
  def $meminst{s : store, f : frame}(`%;%`_state(s, f)) = s.MEMS_store

;; 6-runtime-aux.watsup
def $taginst(state : state) : taginst*
  ;; 6-runtime-aux.watsup
  def $taginst{s : store, f : frame}(`%;%`_state(s, f)) = s.TAGS_store

;; 6-runtime-aux.watsup
def $eleminst(state : state) : eleminst*
  ;; 6-runtime-aux.watsup
  def $eleminst{s : store, f : frame}(`%;%`_state(s, f)) = s.ELEMS_store

;; 6-runtime-aux.watsup
def $datainst(state : state) : datainst*
  ;; 6-runtime-aux.watsup
  def $datainst{s : store, f : frame}(`%;%`_state(s, f)) = s.DATAS_store

;; 6-runtime-aux.watsup
def $structinst(state : state) : structinst*
  ;; 6-runtime-aux.watsup
  def $structinst{s : store, f : frame}(`%;%`_state(s, f)) = s.STRUCTS_store

;; 6-runtime-aux.watsup
def $arrayinst(state : state) : arrayinst*
  ;; 6-runtime-aux.watsup
  def $arrayinst{s : store, f : frame}(`%;%`_state(s, f)) = s.ARRAYS_store

;; 6-runtime-aux.watsup
def $exninst(state : state) : exninst*
  ;; 6-runtime-aux.watsup
  def $exninst{s : store, f : frame}(`%;%`_state(s, f)) = s.EXNS_store

;; 6-runtime-aux.watsup
def $type(state : state, typeidx : typeidx) : deftype
  ;; 6-runtime-aux.watsup
  def $type{s : store, f : frame, x : idx}(`%;%`_state(s, f), x) = f.MODULE_frame.TYPES_moduleinst[x!`%`_idx.0]

;; 6-runtime-aux.watsup
def $func(state : state, funcidx : funcidx) : funcinst
  ;; 6-runtime-aux.watsup
  def $func{s : store, f : frame, x : idx}(`%;%`_state(s, f), x) = s.FUNCS_store[f.MODULE_frame.FUNCS_moduleinst[x!`%`_idx.0]]

;; 6-runtime-aux.watsup
def $global(state : state, globalidx : globalidx) : globalinst
  ;; 6-runtime-aux.watsup
  def $global{s : store, f : frame, x : idx}(`%;%`_state(s, f), x) = s.GLOBALS_store[f.MODULE_frame.GLOBALS_moduleinst[x!`%`_idx.0]]

;; 6-runtime-aux.watsup
def $table(state : state, tableidx : tableidx) : tableinst
  ;; 6-runtime-aux.watsup
  def $table{s : store, f : frame, x : idx}(`%;%`_state(s, f), x) = s.TABLES_store[f.MODULE_frame.TABLES_moduleinst[x!`%`_idx.0]]

;; 6-runtime-aux.watsup
def $mem(state : state, memidx : memidx) : meminst
  ;; 6-runtime-aux.watsup
  def $mem{s : store, f : frame, x : idx}(`%;%`_state(s, f), x) = s.MEMS_store[f.MODULE_frame.MEMS_moduleinst[x!`%`_idx.0]]

;; 6-runtime-aux.watsup
def $tag(state : state, tagidx : tagidx) : taginst
  ;; 6-runtime-aux.watsup
  def $tag{s : store, f : frame, x : idx}(`%;%`_state(s, f), x) = s.TAGS_store[f.MODULE_frame.TAGS_moduleinst[x!`%`_idx.0]]

;; 6-runtime-aux.watsup
def $elem(state : state, tableidx : tableidx) : eleminst
  ;; 6-runtime-aux.watsup
  def $elem{s : store, f : frame, x : idx}(`%;%`_state(s, f), x) = s.ELEMS_store[f.MODULE_frame.ELEMS_moduleinst[x!`%`_idx.0]]

;; 6-runtime-aux.watsup
def $data(state : state, dataidx : dataidx) : datainst
  ;; 6-runtime-aux.watsup
  def $data{s : store, f : frame, x : idx}(`%;%`_state(s, f), x) = s.DATAS_store[f.MODULE_frame.DATAS_moduleinst[x!`%`_idx.0]]

;; 6-runtime-aux.watsup
def $local(state : state, localidx : localidx) : val?
  ;; 6-runtime-aux.watsup
  def $local{s : store, f : frame, x : idx}(`%;%`_state(s, f), x) = f.LOCALS_frame[x!`%`_idx.0]

;; 6-runtime-aux.watsup
def $with_local(state : state, localidx : localidx, val : val) : state
  ;; 6-runtime-aux.watsup
  def $with_local{s : store, f : frame, x : idx, v : val}(`%;%`_state(s, f), x, v) = `%;%`_state(s, f[LOCALS_frame[x!`%`_idx.0] = ?(v)])

;; 6-runtime-aux.watsup
def $with_global(state : state, globalidx : globalidx, val : val) : state
  ;; 6-runtime-aux.watsup
  def $with_global{s : store, f : frame, x : idx, v : val}(`%;%`_state(s, f), x, v) = `%;%`_state(s[GLOBALS_store[f.MODULE_frame.GLOBALS_moduleinst[x!`%`_idx.0]].VALUE_globalinst = v], f)

;; 6-runtime-aux.watsup
def $with_table(state : state, tableidx : tableidx, nat : nat, ref : ref) : state
  ;; 6-runtime-aux.watsup
  def $with_table{s : store, f : frame, x : idx, i : nat, r : ref}(`%;%`_state(s, f), x, i, r) = `%;%`_state(s[TABLES_store[f.MODULE_frame.TABLES_moduleinst[x!`%`_idx.0]].REFS_tableinst[i] = r], f)

;; 6-runtime-aux.watsup
def $with_tableinst(state : state, tableidx : tableidx, tableinst : tableinst) : state
  ;; 6-runtime-aux.watsup
  def $with_tableinst{s : store, f : frame, x : idx, ti : tableinst}(`%;%`_state(s, f), x, ti) = `%;%`_state(s[TABLES_store[f.MODULE_frame.TABLES_moduleinst[x!`%`_idx.0]] = ti], f)

;; 6-runtime-aux.watsup
def $with_mem(state : state, memidx : memidx, nat : nat, nat : nat, byte*) : state
  ;; 6-runtime-aux.watsup
  def $with_mem{s : store, f : frame, x : idx, i : nat, j : nat, `b*` : byte*}(`%;%`_state(s, f), x, i, j, b*{b <- `b*`}) = `%;%`_state(s[MEMS_store[f.MODULE_frame.MEMS_moduleinst[x!`%`_idx.0]].BYTES_meminst[i : j] = b*{b <- `b*`}], f)

;; 6-runtime-aux.watsup
def $with_meminst(state : state, memidx : memidx, meminst : meminst) : state
  ;; 6-runtime-aux.watsup
  def $with_meminst{s : store, f : frame, x : idx, mi : meminst}(`%;%`_state(s, f), x, mi) = `%;%`_state(s[MEMS_store[f.MODULE_frame.MEMS_moduleinst[x!`%`_idx.0]] = mi], f)

;; 6-runtime-aux.watsup
def $with_elem(state : state, elemidx : elemidx, ref*) : state
  ;; 6-runtime-aux.watsup
  def $with_elem{s : store, f : frame, x : idx, `r*` : ref*}(`%;%`_state(s, f), x, r*{r <- `r*`}) = `%;%`_state(s[ELEMS_store[f.MODULE_frame.ELEMS_moduleinst[x!`%`_idx.0]].REFS_eleminst = r*{r <- `r*`}], f)

;; 6-runtime-aux.watsup
def $with_data(state : state, dataidx : dataidx, byte*) : state
  ;; 6-runtime-aux.watsup
  def $with_data{s : store, f : frame, x : idx, `b*` : byte*}(`%;%`_state(s, f), x, b*{b <- `b*`}) = `%;%`_state(s[DATAS_store[f.MODULE_frame.DATAS_moduleinst[x!`%`_idx.0]].BYTES_datainst = b*{b <- `b*`}], f)

;; 6-runtime-aux.watsup
def $with_struct(state : state, structaddr : structaddr, nat : nat, fieldval : fieldval) : state
  ;; 6-runtime-aux.watsup
  def $with_struct{s : store, f : frame, a : addr, i : nat, fv : fieldval}(`%;%`_state(s, f), a, i, fv) = `%;%`_state(s[STRUCTS_store[a].FIELDS_structinst[i] = fv], f)

;; 6-runtime-aux.watsup
def $with_array(state : state, arrayaddr : arrayaddr, nat : nat, fieldval : fieldval) : state
  ;; 6-runtime-aux.watsup
  def $with_array{s : store, f : frame, a : addr, i : nat, fv : fieldval}(`%;%`_state(s, f), a, i, fv) = `%;%`_state(s[ARRAYS_store[a].FIELDS_arrayinst[i] = fv], f)

;; 6-runtime-aux.watsup
def $add_structinst(state : state, structinst*) : state
  ;; 6-runtime-aux.watsup
  def $add_structinst{s : store, f : frame, `si*` : structinst*}(`%;%`_state(s, f), si*{si <- `si*`}) = `%;%`_state(s[STRUCTS_store =++ si*{si <- `si*`}], f)

;; 6-runtime-aux.watsup
def $add_arrayinst(state : state, arrayinst*) : state
  ;; 6-runtime-aux.watsup
  def $add_arrayinst{s : store, f : frame, `ai*` : arrayinst*}(`%;%`_state(s, f), ai*{ai <- `ai*`}) = `%;%`_state(s[ARRAYS_store =++ ai*{ai <- `ai*`}], f)

;; 6-runtime-aux.watsup
def $add_exninst(state : state, exninst*) : state
  ;; 6-runtime-aux.watsup
  def $add_exninst{s : store, f : frame, `exn*` : exninst*}(`%;%`_state(s, f), exn*{exn <- `exn*`}) = `%;%`_state(s[EXNS_store =++ exn*{exn <- `exn*`}], f)

;; 6-runtime-aux.watsup
def $growtable(tableinst : tableinst, nat : nat, ref : ref) : tableinst
  ;; 6-runtime-aux.watsup
  def $growtable{tableinst : tableinst, n : n, r : ref, tableinst' : tableinst, at : addrtype, i : u64, j : u64, rt : reftype, `r'*` : ref*, i' : u64}(tableinst, n, r) = tableinst'
    -- if (tableinst = {TYPE `%%%`_tabletype(at, `[%..%]`_limits(i, j), rt), REFS r'*{r' <- `r'*`}})
    -- if (tableinst' = {TYPE `%%%`_tabletype(at, `[%..%]`_limits(i', j), rt), REFS r'*{r' <- `r'*`} ++ r^n{}})
    -- if ((i'!`%`_u64.0 = (|r'*{r' <- `r'*`}| + n)) /\ ((|r'*{r' <- `r'*`}| + n) <= j!`%`_u64.0))

;; 6-runtime-aux.watsup
def $growmem(meminst : meminst, nat : nat) : meminst
  ;; 6-runtime-aux.watsup
  def $growmem{meminst : meminst, n : n, meminst' : meminst, at : addrtype, i : u64, j : u64, `b*` : byte*, i' : u64}(meminst, n) = meminst'
    -- if (meminst = {TYPE `%%PAGE`_memtype(at, `[%..%]`_limits(i, j)), BYTES b*{b <- `b*`}})
    -- if (meminst' = {TYPE `%%PAGE`_memtype(at, `[%..%]`_limits(i', j)), BYTES b*{b <- `b*`} ++ `%`_byte(0)^(n * (64 * $Ki)){}})
    -- if (((i'!`%`_u64.0 : nat <:> rat) = (((|b*{b <- `b*`}| : nat <:> rat) / ((64 * $Ki) : nat <:> rat)) + (n : nat <:> rat))) /\ ((((|b*{b <- `b*`}| : nat <:> rat) / ((64 * $Ki) : nat <:> rat)) + (n : nat <:> rat)) <= (j!`%`_u64.0 : nat <:> rat)))

;; 7-runtime-typing.watsup
relation Num_type: `%|-%:%`(store, num, numtype)
  ;; 7-runtime-typing.watsup
  rule _{s : store, nt : numtype, c : num_(nt)}:
    `%|-%:%`(s, CONST_num(nt, c), nt)

;; 7-runtime-typing.watsup
relation Vec_type: `%|-%:%`(store, vec, vectype)
  ;; 7-runtime-typing.watsup
  rule _{s : store, vt : vectype, c : vec_(vt)}:
    `%|-%:%`(s, VCONST_vec(vt, c), vt)

;; 7-runtime-typing.watsup
rec {

;; 7-runtime-typing.watsup:7.1-7.42
relation Ref_type: `%|-%:%`(store, ref, reftype)
  ;; 7-runtime-typing.watsup:17.1-19.35
  rule null{s : store, ht : heaptype, ht' : heaptype}:
    `%|-%:%`(s, REF.NULL_ref(ht), REF_reftype(?(NULL_NULL), ht'))
    -- Heaptype_sub: `%|-%<:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, ht', ht)

  ;; 7-runtime-typing.watsup:21.1-22.33
  rule i31{s : store, i : u31}:
    `%|-%:%`(s, REF.I31_NUM_ref(i), REF_reftype(?(), I31_heaptype))

  ;; 7-runtime-typing.watsup:24.1-26.31
  rule struct{s : store, a : addr, dt : deftype}:
    `%|-%:%`(s, REF.STRUCT_ADDR_ref(a), REF_reftype(?(), (dt : deftype <: heaptype)))
    -- if (s.STRUCTS_store[a].TYPE_structinst = dt)

  ;; 7-runtime-typing.watsup:28.1-30.30
  rule array{s : store, a : addr, dt : deftype}:
    `%|-%:%`(s, REF.ARRAY_ADDR_ref(a), REF_reftype(?(), (dt : deftype <: heaptype)))
    -- if (s.ARRAYS_store[a].TYPE_arrayinst = dt)

  ;; 7-runtime-typing.watsup:32.1-34.29
  rule func{s : store, a : addr, dt : deftype}:
    `%|-%:%`(s, REF.FUNC_ADDR_ref(a), REF_reftype(?(), (dt : deftype <: heaptype)))
    -- if (s.FUNCS_store[a].TYPE_funcinst = dt)

  ;; 7-runtime-typing.watsup:36.1-37.34
  rule exn{s : store, a : addr}:
    `%|-%:%`(s, REF.EXN_ADDR_ref(a), REF_reftype(?(), EXN_heaptype))

  ;; 7-runtime-typing.watsup:39.1-40.35
  rule host{s : store, a : addr}:
    `%|-%:%`(s, REF.HOST_ADDR_ref(a), REF_reftype(?(), ANY_heaptype))

  ;; 7-runtime-typing.watsup:42.1-43.41
  rule extern{s : store, addrref : addrref}:
    `%|-%:%`(s, REF.EXTERN_ref(addrref), REF_reftype(?(), EXTERN_heaptype))

  ;; 7-runtime-typing.watsup:45.1-48.34
  rule sub{s : store, ref : ref, rt : reftype, rt' : reftype}:
    `%|-%:%`(s, ref, rt)
    -- Ref_type: `%|-%:%`(s, ref, rt')
    -- Reftype_sub: `%|-%<:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, rt', rt)
}

;; 7-runtime-typing.watsup
relation Val_type: `%|-%:%`(store, val, valtype)
  ;; 7-runtime-typing.watsup
  rule num{s : store, num : num, nt : numtype}:
    `%|-%:%`(s, (num : num <: val), (nt : numtype <: valtype))
    -- Num_type: `%|-%:%`(s, num, nt)

  ;; 7-runtime-typing.watsup
  rule vec{s : store, vec : vec, vt : vectype}:
    `%|-%:%`(s, (vec : vec <: val), (vt : vectype <: valtype))
    -- Vec_type: `%|-%:%`(s, vec, vt)

  ;; 7-runtime-typing.watsup
  rule ref{s : store, ref : ref, rt : reftype}:
    `%|-%:%`(s, (ref : ref <: val), (rt : reftype <: valtype))
    -- Ref_type: `%|-%:%`(s, ref, rt)

;; 7-runtime-typing.watsup
rec {

;; 7-runtime-typing.watsup:68.1-68.59
relation Externaddr_type: `%|-%:%`(store, externaddr, externtype)
  ;; 7-runtime-typing.watsup:70.1-72.30
  rule func{s : store, a : addr, funcinst : funcinst}:
    `%|-%:%`(s, FUNC_externaddr(a), FUNC_externtype((funcinst.TYPE_funcinst : deftype <: typeuse)))
    -- if (s.FUNCS_store[a] = funcinst)

  ;; 7-runtime-typing.watsup:74.1-76.34
  rule global{s : store, a : addr, globalinst : globalinst}:
    `%|-%:%`(s, GLOBAL_externaddr(a), GLOBAL_externtype(globalinst.TYPE_globalinst))
    -- if (s.GLOBALS_store[a] = globalinst)

  ;; 7-runtime-typing.watsup:78.1-80.32
  rule table{s : store, a : addr, tableinst : tableinst}:
    `%|-%:%`(s, TABLE_externaddr(a), TABLE_externtype(tableinst.TYPE_tableinst))
    -- if (s.TABLES_store[a] = tableinst)

  ;; 7-runtime-typing.watsup:82.1-84.28
  rule mem{s : store, a : addr, meminst : meminst}:
    `%|-%:%`(s, MEM_externaddr(a), MEM_externtype(meminst.TYPE_meminst))
    -- if (s.MEMS_store[a] = meminst)

  ;; 7-runtime-typing.watsup:86.1-88.28
  rule tag{s : store, a : addr, taginst : taginst}:
    `%|-%:%`(s, TAG_externaddr(a), TAG_externtype((taginst.TYPE_taginst : deftype <: typeuse)))
    -- if (s.TAGS_store[a] = taginst)

  ;; 7-runtime-typing.watsup:90.1-93.37
  rule sub{s : store, externaddr : externaddr, xt : externtype, xt' : externtype}:
    `%|-%:%`(s, externaddr, xt)
    -- Externaddr_type: `%|-%:%`(s, externaddr, xt')
    -- Externtype_sub: `%|-%<:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, xt', xt)
}

;; 8-reduction.watsup
relation Step_pure: `%~>%`(instr*, instr*)
  ;; 8-reduction.watsup
  rule unreachable:
    `%~>%`([UNREACHABLE_instr], [TRAP_instr])

  ;; 8-reduction.watsup
  rule nop:
    `%~>%`([NOP_instr], [])

  ;; 8-reduction.watsup
  rule drop{val : val}:
    `%~>%`([(val : val <: instr) DROP_instr], [])

  ;; 8-reduction.watsup
  rule `select-true`{val_1 : val, val_2 : val, c : num_(I32_numtype), `t*?` : valtype*?}:
    `%~>%`([(val_1 : val <: instr) (val_2 : val <: instr) CONST_instr(I32_numtype, c) SELECT_instr(t*{t <- `t*`}?{`t*` <- `t*?`})], [(val_1 : val <: instr)])
    -- if (c!`%`_num_.0 =/= 0)

  ;; 8-reduction.watsup
  rule `select-false`{val_1 : val, val_2 : val, c : num_(I32_numtype), `t*?` : valtype*?}:
    `%~>%`([(val_1 : val <: instr) (val_2 : val <: instr) CONST_instr(I32_numtype, c) SELECT_instr(t*{t <- `t*`}?{`t*` <- `t*?`})], [(val_2 : val <: instr)])
    -- if (c!`%`_num_.0 = 0)

  ;; 8-reduction.watsup
  rule `if-true`{c : num_(I32_numtype), bt : blocktype, `instr_1*` : instr*, `instr_2*` : instr*}:
    `%~>%`([CONST_instr(I32_numtype, c) `IF%%ELSE%`_instr(bt, instr_1*{instr_1 <- `instr_1*`}, instr_2*{instr_2 <- `instr_2*`})], [BLOCK_instr(bt, instr_1*{instr_1 <- `instr_1*`})])
    -- if (c!`%`_num_.0 =/= 0)

  ;; 8-reduction.watsup
  rule `if-false`{c : num_(I32_numtype), bt : blocktype, `instr_1*` : instr*, `instr_2*` : instr*}:
    `%~>%`([CONST_instr(I32_numtype, c) `IF%%ELSE%`_instr(bt, instr_1*{instr_1 <- `instr_1*`}, instr_2*{instr_2 <- `instr_2*`})], [BLOCK_instr(bt, instr_2*{instr_2 <- `instr_2*`})])
    -- if (c!`%`_num_.0 = 0)

  ;; 8-reduction.watsup
  rule `label-vals`{n : n, `instr*` : instr*, `val*` : val*}:
    `%~>%`([`LABEL_%{%}%`_instr(n, instr*{instr <- `instr*`}, (val : val <: instr)*{val <- `val*`})], (val : val <: instr)*{val <- `val*`})

  ;; 8-reduction.watsup
  rule `br-label-zero`{n : n, `instr'*` : instr*, `val'*` : val*, `val*` : val*, l : labelidx, `instr*` : instr*}:
    `%~>%`([`LABEL_%{%}%`_instr(n, instr'*{instr' <- `instr'*`}, (val' : val <: instr)*{val' <- `val'*`} ++ (val : val <: instr)^n{val <- `val*`} ++ [BR_instr(l)] ++ instr*{instr <- `instr*`})], (val : val <: instr)^n{val <- `val*`} ++ instr'*{instr' <- `instr'*`})
    -- if (l!`%`_labelidx.0 = 0)

  ;; 8-reduction.watsup
  rule `br-label-succ`{n : n, `instr'*` : instr*, `val*` : val*, l : labelidx, `instr*` : instr*}:
    `%~>%`([`LABEL_%{%}%`_instr(n, instr'*{instr' <- `instr'*`}, (val : val <: instr)*{val <- `val*`} ++ [BR_instr(l)] ++ instr*{instr <- `instr*`})], (val : val <: instr)*{val <- `val*`} ++ [BR_instr(`%`_labelidx((((l!`%`_labelidx.0 : nat <:> int) - (1 : nat <:> int)) : int <:> nat)))])
    -- if (l!`%`_labelidx.0 > 0)

  ;; 8-reduction.watsup
  rule `br-handler`{n : n, `catch*` : catch*, `val*` : val*, l : labelidx, `instr*` : instr*}:
    `%~>%`([`HANDLER_%{%}%`_instr(n, catch*{catch <- `catch*`}, (val : val <: instr)*{val <- `val*`} ++ [BR_instr(l)] ++ instr*{instr <- `instr*`})], (val : val <: instr)*{val <- `val*`} ++ [BR_instr(l)])

  ;; 8-reduction.watsup
  rule `br_if-true`{c : num_(I32_numtype), l : labelidx}:
    `%~>%`([CONST_instr(I32_numtype, c) BR_IF_instr(l)], [BR_instr(l)])
    -- if (c!`%`_num_.0 =/= 0)

  ;; 8-reduction.watsup
  rule `br_if-false`{c : num_(I32_numtype), l : labelidx}:
    `%~>%`([CONST_instr(I32_numtype, c) BR_IF_instr(l)], [])
    -- if (c!`%`_num_.0 = 0)

  ;; 8-reduction.watsup
  rule `br_table-lt`{i : num_(I32_numtype), `l*` : labelidx*, l' : labelidx}:
    `%~>%`([CONST_instr(I32_numtype, i) BR_TABLE_instr(l*{l <- `l*`}, l')], [BR_instr(l*{l <- `l*`}[i!`%`_num_.0])])
    -- if (i!`%`_num_.0 < |l*{l <- `l*`}|)

  ;; 8-reduction.watsup
  rule `br_table-ge`{i : num_(I32_numtype), `l*` : labelidx*, l' : labelidx}:
    `%~>%`([CONST_instr(I32_numtype, i) BR_TABLE_instr(l*{l <- `l*`}, l')], [BR_instr(l')])
    -- if (i!`%`_num_.0 >= |l*{l <- `l*`}|)

  ;; 8-reduction.watsup
  rule `br_on_null-null`{val : val, l : labelidx, ht : heaptype}:
    `%~>%`([(val : val <: instr) BR_ON_NULL_instr(l)], [BR_instr(l)])
    -- if (val = REF.NULL_val(ht))

  ;; 8-reduction.watsup
  rule `br_on_null-addr`{val : val, l : labelidx}:
    `%~>%`([(val : val <: instr) BR_ON_NULL_instr(l)], [(val : val <: instr)])
    -- otherwise

  ;; 8-reduction.watsup
  rule `br_on_non_null-null`{val : val, l : labelidx, ht : heaptype}:
    `%~>%`([(val : val <: instr) BR_ON_NON_NULL_instr(l)], [])
    -- if (val = REF.NULL_val(ht))

  ;; 8-reduction.watsup
  rule `br_on_non_null-addr`{val : val, l : labelidx}:
    `%~>%`([(val : val <: instr) BR_ON_NON_NULL_instr(l)], [(val : val <: instr) BR_instr(l)])
    -- otherwise

  ;; 8-reduction.watsup
  rule call_indirect{x : idx, yy : typeuse}:
    `%~>%`([CALL_INDIRECT_instr(x, yy)], [TABLE.GET_instr(x) REF.CAST_instr(REF_reftype(?(NULL_NULL), (yy : typeuse <: heaptype))) CALL_REF_instr(yy)])

  ;; 8-reduction.watsup
  rule return_call_indirect{x : idx, yy : typeuse}:
    `%~>%`([RETURN_CALL_INDIRECT_instr(x, yy)], [TABLE.GET_instr(x) REF.CAST_instr(REF_reftype(?(NULL_NULL), (yy : typeuse <: heaptype))) RETURN_CALL_REF_instr(yy)])

  ;; 8-reduction.watsup
  rule `frame-vals`{n : n, f : frame, `val*` : val*}:
    `%~>%`([`FRAME_%{%}%`_instr(n, f, (val : val <: instr)^n{val <- `val*`})], (val : val <: instr)^n{val <- `val*`})

  ;; 8-reduction.watsup
  rule `return-frame`{n : n, f : frame, `val'*` : val*, `val*` : val*, `instr*` : instr*}:
    `%~>%`([`FRAME_%{%}%`_instr(n, f, (val' : val <: instr)*{val' <- `val'*`} ++ (val : val <: instr)^n{val <- `val*`} ++ [RETURN_instr] ++ instr*{instr <- `instr*`})], (val : val <: instr)^n{val <- `val*`})

  ;; 8-reduction.watsup
  rule `return-label`{n : n, `instr'*` : instr*, `val*` : val*, `instr*` : instr*}:
    `%~>%`([`LABEL_%{%}%`_instr(n, instr'*{instr' <- `instr'*`}, (val : val <: instr)*{val <- `val*`} ++ [RETURN_instr] ++ instr*{instr <- `instr*`})], (val : val <: instr)*{val <- `val*`} ++ [RETURN_instr])

  ;; 8-reduction.watsup
  rule `return-handler`{n : n, `catch*` : catch*, `val*` : val*, `instr*` : instr*}:
    `%~>%`([`HANDLER_%{%}%`_instr(n, catch*{catch <- `catch*`}, (val : val <: instr)*{val <- `val*`} ++ [RETURN_instr] ++ instr*{instr <- `instr*`})], (val : val <: instr)*{val <- `val*`} ++ [RETURN_instr])

  ;; 8-reduction.watsup
  rule `handler-vals`{n : n, `catch*` : catch*, `val*` : val*}:
    `%~>%`([`HANDLER_%{%}%`_instr(n, catch*{catch <- `catch*`}, (val : val <: instr)*{val <- `val*`})], (val : val <: instr)*{val <- `val*`})

  ;; 8-reduction.watsup
  rule `trap-instrs`{`val*` : val*, `instr*` : instr*}:
    `%~>%`((val : val <: instr)*{val <- `val*`} ++ [TRAP_instr] ++ instr*{instr <- `instr*`}, [TRAP_instr])
    -- if ((val*{val <- `val*`} =/= []) \/ (instr*{instr <- `instr*`} =/= []))

  ;; 8-reduction.watsup
  rule `trap-label`{n : n, `instr'*` : instr*}:
    `%~>%`([`LABEL_%{%}%`_instr(n, instr'*{instr' <- `instr'*`}, [TRAP_instr])], [TRAP_instr])

  ;; 8-reduction.watsup
  rule `trap-frame`{n : n, f : frame}:
    `%~>%`([`FRAME_%{%}%`_instr(n, f, [TRAP_instr])], [TRAP_instr])

  ;; 8-reduction.watsup
  rule `unop-val`{nt : numtype, c_1 : num_(nt), unop : unop_(nt), c : num_(nt)}:
    `%~>%`([CONST_instr(nt, c_1) UNOP_instr(nt, unop)], [CONST_instr(nt, c)])
    -- if c <- $unop_(nt, unop, c_1)

  ;; 8-reduction.watsup
  rule `unop-trap`{nt : numtype, c_1 : num_(nt), unop : unop_(nt)}:
    `%~>%`([CONST_instr(nt, c_1) UNOP_instr(nt, unop)], [TRAP_instr])
    -- if ($unop_(nt, unop, c_1) = [])

  ;; 8-reduction.watsup
  rule `binop-val`{nt : numtype, c_1 : num_(nt), c_2 : num_(nt), binop : binop_(nt), c : num_(nt)}:
    `%~>%`([CONST_instr(nt, c_1) CONST_instr(nt, c_2) BINOP_instr(nt, binop)], [CONST_instr(nt, c)])
    -- if c <- $binop_(nt, binop, c_1, c_2)

  ;; 8-reduction.watsup
  rule `binop-trap`{nt : numtype, c_1 : num_(nt), c_2 : num_(nt), binop : binop_(nt)}:
    `%~>%`([CONST_instr(nt, c_1) CONST_instr(nt, c_2) BINOP_instr(nt, binop)], [TRAP_instr])
    -- if ($binop_(nt, binop, c_1, c_2) = [])

  ;; 8-reduction.watsup
  rule testop{nt : numtype, c_1 : num_(nt), testop : testop_(nt), c : num_(I32_numtype)}:
    `%~>%`([CONST_instr(nt, c_1) TESTOP_instr(nt, testop)], [CONST_instr(I32_numtype, c)])
    -- if (c = $testop_(nt, testop, c_1))

  ;; 8-reduction.watsup
  rule relop{nt : numtype, c_1 : num_(nt), c_2 : num_(nt), relop : relop_(nt), c : num_(I32_numtype)}:
    `%~>%`([CONST_instr(nt, c_1) CONST_instr(nt, c_2) RELOP_instr(nt, relop)], [CONST_instr(I32_numtype, c)])
    -- if (c = $relop_(nt, relop, c_1, c_2))

  ;; 8-reduction.watsup
  rule `cvtop-val`{nt_1 : numtype, c_1 : num_(nt_1), nt_2 : numtype, cvtop : cvtop__(nt_1, nt_2), c : num_(nt_2)}:
    `%~>%`([CONST_instr(nt_1, c_1) CVTOP_instr(nt_2, nt_1, cvtop)], [CONST_instr(nt_2, c)])
    -- if c <- $cvtop__(nt_1, nt_2, cvtop, c_1)

  ;; 8-reduction.watsup
  rule `cvtop-trap`{nt_1 : numtype, c_1 : num_(nt_1), nt_2 : numtype, cvtop : cvtop__(nt_1, nt_2)}:
    `%~>%`([CONST_instr(nt_1, c_1) CVTOP_instr(nt_2, nt_1, cvtop)], [TRAP_instr])
    -- if ($cvtop__(nt_1, nt_2, cvtop, c_1) = [])

  ;; 8-reduction.watsup
  rule ref.i31{i : num_(I32_numtype)}:
    `%~>%`([CONST_instr(I32_numtype, i) REF.I31_instr], [REF.I31_NUM_instr($wrap__(32, 31, i))])

  ;; 8-reduction.watsup
  rule `ref.is_null-true`{ref : ref, ht : heaptype}:
    `%~>%`([(ref : ref <: instr) REF.IS_NULL_instr], [CONST_instr(I32_numtype, `%`_num_(1))])
    -- if (ref = REF.NULL_ref(ht))

  ;; 8-reduction.watsup
  rule `ref.is_null-false`{ref : ref}:
    `%~>%`([(ref : ref <: instr) REF.IS_NULL_instr], [CONST_instr(I32_numtype, `%`_num_(0))])
    -- otherwise

  ;; 8-reduction.watsup
  rule `ref.as_non_null-null`{ref : ref, ht : heaptype}:
    `%~>%`([(ref : ref <: instr) REF.AS_NON_NULL_instr], [TRAP_instr])
    -- if (ref = REF.NULL_ref(ht))

  ;; 8-reduction.watsup
  rule `ref.as_non_null-addr`{ref : ref}:
    `%~>%`([(ref : ref <: instr) REF.AS_NON_NULL_instr], [(ref : ref <: instr)])
    -- otherwise

  ;; 8-reduction.watsup
  rule `ref.eq-null`{ref_1 : ref, ref_2 : ref, ht_1 : heaptype, ht_2 : heaptype}:
    `%~>%`([(ref_1 : ref <: instr) (ref_2 : ref <: instr) REF.EQ_instr], [CONST_instr(I32_numtype, `%`_num_(1))])
    -- if ((ref_1 = REF.NULL_ref(ht_1)) /\ (ref_2 = REF.NULL_ref(ht_2)))

  ;; 8-reduction.watsup
  rule `ref.eq-true`{ref_1 : ref, ref_2 : ref}:
    `%~>%`([(ref_1 : ref <: instr) (ref_2 : ref <: instr) REF.EQ_instr], [CONST_instr(I32_numtype, `%`_num_(1))])
    -- otherwise
    -- if (ref_1 = ref_2)

  ;; 8-reduction.watsup
  rule `ref.eq-false`{ref_1 : ref, ref_2 : ref}:
    `%~>%`([(ref_1 : ref <: instr) (ref_2 : ref <: instr) REF.EQ_instr], [CONST_instr(I32_numtype, `%`_num_(0))])
    -- otherwise

  ;; 8-reduction.watsup
  rule `i31.get-null`{ht : heaptype, sx : sx}:
    `%~>%`([REF.NULL_instr(ht) I31.GET_instr(sx)], [TRAP_instr])

  ;; 8-reduction.watsup
  rule `i31.get-num`{i : u31, sx : sx}:
    `%~>%`([REF.I31_NUM_instr(i) I31.GET_instr(sx)], [CONST_instr(I32_numtype, $extend__(31, 32, sx, i))])

  ;; 8-reduction.watsup
  rule array.new{val : val, n : n, x : idx}:
    `%~>%`([(val : val <: instr) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.NEW_instr(x)], (val : val <: instr)^n{} ++ [ARRAY.NEW_FIXED_instr(x, `%`_u32(n))])

  ;; 8-reduction.watsup
  rule `extern.convert_any-null`{ht : heaptype}:
    `%~>%`([REF.NULL_instr(ht) EXTERN.CONVERT_ANY_instr], [REF.NULL_instr(EXTERN_heaptype)])

  ;; 8-reduction.watsup
  rule `extern.convert_any-addr`{addrref : addrref}:
    `%~>%`([(addrref : addrref <: instr) EXTERN.CONVERT_ANY_instr], [REF.EXTERN_instr(addrref)])

  ;; 8-reduction.watsup
  rule `any.convert_extern-null`{ht : heaptype}:
    `%~>%`([REF.NULL_instr(ht) ANY.CONVERT_EXTERN_instr], [REF.NULL_instr(ANY_heaptype)])

  ;; 8-reduction.watsup
  rule `any.convert_extern-addr`{addrref : addrref}:
    `%~>%`([REF.EXTERN_instr(addrref) ANY.CONVERT_EXTERN_instr], [(addrref : addrref <: instr)])

  ;; 8-reduction.watsup
  rule vvunop{c_1 : vec_(V128_Vnn), vvunop : vvunop, c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VVUNOP_instr(V128_vectype, vvunop)], [VCONST_instr(V128_vectype, c)])
    -- if c <- $vvunop_(V128_vectype, vvunop, c_1)

  ;; 8-reduction.watsup
  rule vvbinop{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), vvbinop : vvbinop, c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VVBINOP_instr(V128_vectype, vvbinop)], [VCONST_instr(V128_vectype, c)])
    -- if c <- $vvbinop_(V128_vectype, vvbinop, c_1, c_2)

  ;; 8-reduction.watsup
  rule vvternop{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), c_3 : vec_(V128_Vnn), vvternop : vvternop, c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VCONST_instr(V128_vectype, c_3) VVTERNOP_instr(V128_vectype, vvternop)], [VCONST_instr(V128_vectype, c)])
    -- if c <- $vvternop_(V128_vectype, vvternop, c_1, c_2, c_3)

  ;; 8-reduction.watsup
  rule vvtestop{c_1 : vec_(V128_Vnn), c : num_(I32_numtype)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VVTESTOP_instr(V128_vectype, ANY_TRUE_vvtestop)], [CONST_instr(I32_numtype, c)])
    -- if (c = $ine_($vsize(V128_vectype), c_1, `%`_iN(0)))

  ;; 8-reduction.watsup
  rule `vunop-val`{c_1 : vec_(V128_Vnn), sh : shape, vunop : vunop_(sh), c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VUNOP_instr(sh, vunop)], [VCONST_instr(V128_vectype, c)])
    -- if c <- $vunop_(sh, vunop, c_1)

  ;; 8-reduction.watsup
  rule `vunop-trap`{c_1 : vec_(V128_Vnn), sh : shape, vunop : vunop_(sh)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VUNOP_instr(sh, vunop)], [TRAP_instr])
    -- if ($vunop_(sh, vunop, c_1) = [])

  ;; 8-reduction.watsup
  rule `vbinop-val`{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), sh : shape, vbinop : vbinop_(sh), c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VBINOP_instr(sh, vbinop)], [VCONST_instr(V128_vectype, c)])
    -- if c <- $vbinop_(sh, vbinop, c_1, c_2)

  ;; 8-reduction.watsup
  rule `vbinop-trap`{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), sh : shape, vbinop : vbinop_(sh)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VBINOP_instr(sh, vbinop)], [TRAP_instr])
    -- if ($vbinop_(sh, vbinop, c_1, c_2) = [])

  ;; 8-reduction.watsup
  rule `vternop-val`{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), c_3 : vec_(V128_Vnn), sh : shape, vternop : vternop_(sh), c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VCONST_instr(V128_vectype, c_3) VTERNOP_instr(sh, vternop)], [VCONST_instr(V128_vectype, c)])
    -- if c <- $vternop_(sh, vternop, c_1, c_2, c_3)

  ;; 8-reduction.watsup
  rule `vternop-trap`{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), c_3 : vec_(V128_Vnn), sh : shape, vternop : vternop_(sh)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VCONST_instr(V128_vectype, c_3) VTERNOP_instr(sh, vternop)], [TRAP_instr])
    -- if ($vternop_(sh, vternop, c_1, c_2, c_3) = [])

  ;; 8-reduction.watsup
  rule vtestop{c_1 : vec_(V128_Vnn), sh : shape, vtestop : vtestop_(sh), i : num_(I32_numtype)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VTESTOP_instr(sh, vtestop)], [CONST_instr(I32_numtype, i)])
    -- if (i = $vtestop_(sh, vtestop, c_1))

  ;; 8-reduction.watsup
  rule vrelop{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), sh : shape, vrelop : vrelop_(sh), c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VRELOP_instr(sh, vrelop)], [VCONST_instr(V128_vectype, c)])
    -- if (c = $vrelop_(sh, vrelop, c_1, c_2))

  ;; 8-reduction.watsup
  rule vshiftop{c_1 : vec_(V128_Vnn), i : num_(I32_numtype), sh : ishape, vshiftop : vshiftop_(sh), c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) CONST_instr(I32_numtype, i) VSHIFTOP_instr(sh, vshiftop)], [VCONST_instr(V128_vectype, c)])
    -- if (c = $vshiftop_(sh, vshiftop, c_1, i))

  ;; 8-reduction.watsup
  rule vbitmask{c_1 : vec_(V128_Vnn), sh : ishape, c : num_(I32_numtype)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VBITMASK_instr(sh)], [CONST_instr(I32_numtype, c)])
    -- if (c = $vbitmaskop_(sh, c_1))

  ;; 8-reduction.watsup
  rule vswizzlop{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), sh : bshape, vswizzlop : vswizzlop_(sh), c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VSWIZZLOP_instr(sh, vswizzlop)], [VCONST_instr(V128_vectype, c)])
    -- if (c = $vswizzlop_(sh, vswizzlop, c_1, c_2))

  ;; 8-reduction.watsup
  rule vshuffle{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), sh : bshape, `i*` : laneidx*, c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VSHUFFLE_instr(sh, i*{i <- `i*`})], [VCONST_instr(V128_vectype, c)])
    -- if (c = $vshufflop_(sh, i*{i <- `i*`}, c_1, c_2))

  ;; 8-reduction.watsup
  rule vsplat{Lnn : Lnn, c_1 : num_($lunpack(Lnn)), M : M, c : vec_(V128_Vnn)}:
    `%~>%`([CONST_instr($lunpack(Lnn), c_1) VSPLAT_instr(`%X%`_shape(Lnn, `%`_dim(M)))], [VCONST_instr(V128_vectype, c)])
    -- if (c = $invlanes_(`%X%`_shape(Lnn, `%`_dim(M)), $lpacknum_(Lnn, c_1)^M{}))

  ;; 8-reduction.watsup
  rule `vextract_lane-num`{c_1 : vec_(V128_Vnn), nt : numtype, M : M, i : laneidx, c_2 : num_(nt)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VEXTRACT_LANE_instr(`%X%`_shape((nt : numtype <: lanetype), `%`_dim(M)), ?(), i)], [CONST_instr(nt, c_2)])
    -- if (c_2 = $lanes_(`%X%`_shape((nt : numtype <: lanetype), `%`_dim(M)), c_1)[i!`%`_laneidx.0])

  ;; 8-reduction.watsup
  rule `vextract_lane-pack`{c_1 : vec_(V128_Vnn), pt : packtype, M : M, sx : sx, i : laneidx, c_2 : num_(I32_numtype)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VEXTRACT_LANE_instr(`%X%`_shape((pt : packtype <: lanetype), `%`_dim(M)), ?(sx), i)], [CONST_instr(I32_numtype, c_2)])
    -- if (c_2 = $extend__($psize(pt), 32, sx, $lanes_(`%X%`_shape((pt : packtype <: lanetype), `%`_dim(M)), c_1)[i!`%`_laneidx.0]))

  ;; 8-reduction.watsup
  rule vreplace_lane{c_1 : vec_(V128_Vnn), Lnn : Lnn, c_2 : num_($lunpack(Lnn)), M : M, i : laneidx, c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) CONST_instr($lunpack(Lnn), c_2) VREPLACE_LANE_instr(`%X%`_shape(Lnn, `%`_dim(M)), i)], [VCONST_instr(V128_vectype, c)])
    -- if (c = $invlanes_(`%X%`_shape(Lnn, `%`_dim(M)), $lanes_(`%X%`_shape(Lnn, `%`_dim(M)), c_1)[[i!`%`_laneidx.0] = $lpacknum_(Lnn, c_2)]))

  ;; 8-reduction.watsup
  rule vextunop{c_1 : vec_(V128_Vnn), sh_2 : ishape, sh_1 : ishape, vextunop : vextunop__(sh_1, sh_2), c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VEXTUNOP_instr(sh_2, sh_1, vextunop)], [VCONST_instr(V128_vectype, c)])
    -- if ($vextunop__(sh_1, sh_2, vextunop, c_1) = c)

  ;; 8-reduction.watsup
  rule vextbinop{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), sh_2 : ishape, sh_1 : ishape, vextbinop : vextbinop__(sh_1, sh_2), c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VEXTBINOP_instr(sh_2, sh_1, vextbinop)], [VCONST_instr(V128_vectype, c)])
    -- if ($vextbinop__(sh_1, sh_2, vextbinop, c_1, c_2) = c)

  ;; 8-reduction.watsup
  rule vextternop{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), c_3 : vec_(V128_Vnn), sh_2 : ishape, sh_1 : ishape, vextternop : vextternop__(sh_1, sh_2), c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VCONST_instr(V128_vectype, c_3) VEXTTERNOP_instr(sh_2, sh_1, vextternop)], [VCONST_instr(V128_vectype, c)])
    -- if ($vextternop__(sh_1, sh_2, vextternop, c_1, c_2, c_3) = c)

  ;; 8-reduction.watsup
  rule vnarrow{c_1 : vec_(V128_Vnn), c_2 : vec_(V128_Vnn), sh_2 : ishape, sh_1 : ishape, sx : sx, c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCONST_instr(V128_vectype, c_2) VNARROW_instr(sh_2, sh_1, sx)], [VCONST_instr(V128_vectype, c)])
    -- if (c = $vnarrowop__(sh_1!`%`_ishape.0, sh_2!`%`_ishape.0, sx, c_1, c_2))

  ;; 8-reduction.watsup
  rule vcvtop{c_1 : vec_(V128_Vnn), sh_2 : shape, sh_1 : shape, vcvtop : vcvtop__(sh_1, sh_2), `half?` : half__(sh_1, sh_2)?, `zero?` : zero__(sh_1, sh_2)?, c : vec_(V128_Vnn)}:
    `%~>%`([VCONST_instr(V128_vectype, c_1) VCVTOP_instr(sh_2, sh_1, vcvtop, half?{half <- `half?`}, zero?{zero <- `zero?`})], [VCONST_instr(V128_vectype, c)])
    -- if (c = $vcvtop__(sh_1, sh_2, vcvtop, half?{half <- `half?`}, zero?{zero <- `zero?`}, c_1))

  ;; 8-reduction.watsup
  rule local.tee{val : val, x : idx}:
    `%~>%`([(val : val <: instr) LOCAL.TEE_instr(x)], [(val : val <: instr) (val : val <: instr) LOCAL.SET_instr(x)])

;; 8-reduction.watsup
def $blocktype_(state : state, blocktype : blocktype) : functype
  ;; 8-reduction.watsup
  def $blocktype_{z : state, x : idx, ft : functype}(z, _IDX_blocktype(x)) = ft
    -- Expand: `%~~%`($type(z, x), FUNC_comptype(ft))
  ;; 8-reduction.watsup
  def $blocktype_{z : state, `t?` : valtype?}(z, _RESULT_blocktype(t?{t <- `t?`})) = `%->%`_functype(`%`_resulttype([]), `%`_resulttype(lift(t?{t <- `t?`})))

;; 8-reduction.watsup
relation Step_read: `%~>%`(config, instr*)
  ;; 8-reduction.watsup
  rule block{z : state, `val*` : val*, m : m, bt : blocktype, `instr*` : instr*, n : n, `t_1*` : valtype*, `t_2*` : valtype*}:
    `%~>%`(`%;%`_config(z, (val : val <: instr)^m{val <- `val*`} ++ [BLOCK_instr(bt, instr*{instr <- `instr*`})]), [`LABEL_%{%}%`_instr(n, [], (val : val <: instr)^m{val <- `val*`} ++ instr*{instr <- `instr*`})])
    -- if ($blocktype_(z, bt) = `%->%`_functype(`%`_resulttype(t_1^m{t_1 <- `t_1*`}), `%`_resulttype(t_2^n{t_2 <- `t_2*`})))

  ;; 8-reduction.watsup
  rule loop{z : state, `val*` : val*, m : m, bt : blocktype, `instr*` : instr*, `t_1*` : valtype*, `t_2*` : valtype*, n : n}:
    `%~>%`(`%;%`_config(z, (val : val <: instr)^m{val <- `val*`} ++ [LOOP_instr(bt, instr*{instr <- `instr*`})]), [`LABEL_%{%}%`_instr(m, [LOOP_instr(bt, instr*{instr <- `instr*`})], (val : val <: instr)^m{val <- `val*`} ++ instr*{instr <- `instr*`})])
    -- if ($blocktype_(z, bt) = `%->%`_functype(`%`_resulttype(t_1^m{t_1 <- `t_1*`}), `%`_resulttype(t_2^n{t_2 <- `t_2*`})))

  ;; 8-reduction.watsup
  rule `br_on_cast-succeed`{s : store, f : frame, ref : ref, l : labelidx, rt_1 : reftype, rt_2 : reftype, rt : reftype}:
    `%~>%`(`%;%`_config(`%;%`_state(s, f), [(ref : ref <: instr) BR_ON_CAST_instr(l, rt_1, rt_2)]), [(ref : ref <: instr) BR_instr(l)])
    -- Ref_type: `%|-%:%`(s, ref, rt)
    -- Reftype_sub: `%|-%<:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, rt, $inst_reftype(f.MODULE_frame, rt_2))

  ;; 8-reduction.watsup
  rule `br_on_cast-fail`{s : store, f : frame, ref : ref, l : labelidx, rt_1 : reftype, rt_2 : reftype}:
    `%~>%`(`%;%`_config(`%;%`_state(s, f), [(ref : ref <: instr) BR_ON_CAST_instr(l, rt_1, rt_2)]), [(ref : ref <: instr)])
    -- otherwise

  ;; 8-reduction.watsup
  rule `br_on_cast_fail-succeed`{s : store, f : frame, ref : ref, l : labelidx, rt_1 : reftype, rt_2 : reftype, rt : reftype}:
    `%~>%`(`%;%`_config(`%;%`_state(s, f), [(ref : ref <: instr) BR_ON_CAST_FAIL_instr(l, rt_1, rt_2)]), [(ref : ref <: instr)])
    -- Ref_type: `%|-%:%`(s, ref, rt)
    -- Reftype_sub: `%|-%<:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, rt, $inst_reftype(f.MODULE_frame, rt_2))

  ;; 8-reduction.watsup
  rule `br_on_cast_fail-fail`{s : store, f : frame, ref : ref, l : labelidx, rt_1 : reftype, rt_2 : reftype}:
    `%~>%`(`%;%`_config(`%;%`_state(s, f), [(ref : ref <: instr) BR_ON_CAST_FAIL_instr(l, rt_1, rt_2)]), [(ref : ref <: instr) BR_instr(l)])
    -- otherwise

  ;; 8-reduction.watsup
  rule call{z : state, x : idx, a : addr}:
    `%~>%`(`%;%`_config(z, [CALL_instr(x)]), [REF.FUNC_ADDR_instr(a) CALL_REF_instr(($funcinst(z)[a].TYPE_funcinst : deftype <: typeuse))])
    -- if ($moduleinst(z).FUNCS_moduleinst[x!`%`_idx.0] = a)

  ;; 8-reduction.watsup
  rule `call_ref-null`{z : state, ht : heaptype, yy : typeuse}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht) CALL_REF_instr(yy)]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `call_ref-func`{z : state, `val*` : val*, n : n, a : addr, yy : typeuse, m : m, f : frame, `instr*` : instr*, fi : funcinst, `t_1*` : valtype*, `t_2*` : valtype*, x : idx, `t*` : valtype*}:
    `%~>%`(`%;%`_config(z, (val : val <: instr)^n{val <- `val*`} ++ [REF.FUNC_ADDR_instr(a) CALL_REF_instr(yy)]), [`FRAME_%{%}%`_instr(m, f, [`LABEL_%{%}%`_instr(m, [], instr*{instr <- `instr*`})])])
    -- if ($funcinst(z)[a] = fi)
    -- Expand: `%~~%`(fi.TYPE_funcinst, FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1^n{t_1 <- `t_1*`}), `%`_resulttype(t_2^m{t_2 <- `t_2*`}))))
    -- if (fi.CODE_funcinst = FUNC_funccode(x, LOCAL_local(t)*{t <- `t*`}, instr*{instr <- `instr*`}))
    -- if (f = {LOCALS ?(val)^n{val <- `val*`} ++ $default_(t)*{t <- `t*`}, MODULE fi.MODULE_funcinst})

  ;; 8-reduction.watsup
  rule return_call{z : state, x : idx, a : addr}:
    `%~>%`(`%;%`_config(z, [RETURN_CALL_instr(x)]), [REF.FUNC_ADDR_instr(a) RETURN_CALL_REF_instr(($funcinst(z)[a].TYPE_funcinst : deftype <: typeuse))])
    -- if ($moduleinst(z).FUNCS_moduleinst[x!`%`_idx.0] = a)

  ;; 8-reduction.watsup
  rule `return_call_ref-label`{z : state, k : n, `instr'*` : instr*, `val*` : val*, yy : typeuse, `instr*` : instr*}:
    `%~>%`(`%;%`_config(z, [`LABEL_%{%}%`_instr(k, instr'*{instr' <- `instr'*`}, (val : val <: instr)*{val <- `val*`} ++ [RETURN_CALL_REF_instr(yy)] ++ instr*{instr <- `instr*`})]), (val : val <: instr)*{val <- `val*`} ++ [RETURN_CALL_REF_instr(yy)])

  ;; 8-reduction.watsup
  rule `return_call_ref-handler`{z : state, k : n, `catch*` : catch*, `val*` : val*, yy : typeuse, `instr*` : instr*}:
    `%~>%`(`%;%`_config(z, [`HANDLER_%{%}%`_instr(k, catch*{catch <- `catch*`}, (val : val <: instr)*{val <- `val*`} ++ [RETURN_CALL_REF_instr(yy)] ++ instr*{instr <- `instr*`})]), (val : val <: instr)*{val <- `val*`} ++ [RETURN_CALL_REF_instr(yy)])

  ;; 8-reduction.watsup
  rule `return_call_ref-frame-null`{z : state, k : n, f : frame, `val*` : val*, ht : heaptype, yy : typeuse, `instr*` : instr*}:
    `%~>%`(`%;%`_config(z, [`FRAME_%{%}%`_instr(k, f, (val : val <: instr)*{val <- `val*`} ++ [REF.NULL_instr(ht)] ++ [RETURN_CALL_REF_instr(yy)] ++ instr*{instr <- `instr*`})]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `return_call_ref-frame-addr`{z : state, k : n, f : frame, `val'*` : val*, `val*` : val*, n : n, a : addr, yy : typeuse, `instr*` : instr*, `t_1*` : valtype*, `t_2*` : valtype*, m : m}:
    `%~>%`(`%;%`_config(z, [`FRAME_%{%}%`_instr(k, f, (val' : val <: instr)*{val' <- `val'*`} ++ (val : val <: instr)^n{val <- `val*`} ++ [REF.FUNC_ADDR_instr(a)] ++ [RETURN_CALL_REF_instr(yy)] ++ instr*{instr <- `instr*`})]), (val : val <: instr)^n{val <- `val*`} ++ [REF.FUNC_ADDR_instr(a) CALL_REF_instr(yy)])
    -- Expand: `%~~%`($funcinst(z)[a].TYPE_funcinst, FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1^n{t_1 <- `t_1*`}), `%`_resulttype(t_2^m{t_2 <- `t_2*`}))))

  ;; 8-reduction.watsup
  rule `throw_ref-null`{z : state, ht : heaptype}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht) THROW_REF_instr]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `throw_ref-instrs`{z : state, `val*` : val*, a : addr, `instr*` : instr*}:
    `%~>%`(`%;%`_config(z, (val : val <: instr)*{val <- `val*`} ++ [REF.EXN_ADDR_instr(a)] ++ [THROW_REF_instr] ++ instr*{instr <- `instr*`}), [REF.EXN_ADDR_instr(a) THROW_REF_instr])
    -- if ((val*{val <- `val*`} =/= []) \/ (instr*{instr <- `instr*`} =/= []))

  ;; 8-reduction.watsup
  rule `throw_ref-label`{z : state, n : n, `instr'*` : instr*, a : addr}:
    `%~>%`(`%;%`_config(z, [`LABEL_%{%}%`_instr(n, instr'*{instr' <- `instr'*`}, [REF.EXN_ADDR_instr(a) THROW_REF_instr])]), [REF.EXN_ADDR_instr(a) THROW_REF_instr])

  ;; 8-reduction.watsup
  rule `throw_ref-frame`{z : state, n : n, f : frame, a : addr}:
    `%~>%`(`%;%`_config(z, [`FRAME_%{%}%`_instr(n, f, [REF.EXN_ADDR_instr(a) THROW_REF_instr])]), [REF.EXN_ADDR_instr(a) THROW_REF_instr])

  ;; 8-reduction.watsup
  rule `throw_ref-handler-empty`{z : state, n : n, a : addr}:
    `%~>%`(`%;%`_config(z, [`HANDLER_%{%}%`_instr(n, [], [REF.EXN_ADDR_instr(a) THROW_REF_instr])]), [REF.EXN_ADDR_instr(a) THROW_REF_instr])

  ;; 8-reduction.watsup
  rule `throw_ref-handler-catch`{z : state, n : n, x : idx, l : labelidx, `catch'*` : catch*, a : addr, `val*` : val*}:
    `%~>%`(`%;%`_config(z, [`HANDLER_%{%}%`_instr(n, [CATCH_catch(x, l)] ++ catch'*{catch' <- `catch'*`}, [REF.EXN_ADDR_instr(a) THROW_REF_instr])]), (val : val <: instr)*{val <- `val*`} ++ [BR_instr(l)])
    -- if ($exninst(z)[a].TAG_exninst = $tagaddr(z)[x!`%`_idx.0])
    -- if (val*{val <- `val*`} = $exninst(z)[a].FIELDS_exninst)

  ;; 8-reduction.watsup
  rule `throw_ref-handler-catch_ref`{z : state, n : n, x : idx, l : labelidx, `catch'*` : catch*, a : addr, `val*` : val*}:
    `%~>%`(`%;%`_config(z, [`HANDLER_%{%}%`_instr(n, [CATCH_REF_catch(x, l)] ++ catch'*{catch' <- `catch'*`}, [REF.EXN_ADDR_instr(a) THROW_REF_instr])]), (val : val <: instr)*{val <- `val*`} ++ [REF.EXN_ADDR_instr(a) BR_instr(l)])
    -- if ($exninst(z)[a].TAG_exninst = $tagaddr(z)[x!`%`_idx.0])
    -- if (val*{val <- `val*`} = $exninst(z)[a].FIELDS_exninst)

  ;; 8-reduction.watsup
  rule `throw_ref-handler-catch_all`{z : state, n : n, l : labelidx, `catch'*` : catch*, a : addr}:
    `%~>%`(`%;%`_config(z, [`HANDLER_%{%}%`_instr(n, [CATCH_ALL_catch(l)] ++ catch'*{catch' <- `catch'*`}, [REF.EXN_ADDR_instr(a) THROW_REF_instr])]), [BR_instr(l)])

  ;; 8-reduction.watsup
  rule `throw_ref-handler-catch_all_ref`{z : state, n : n, l : labelidx, `catch'*` : catch*, a : addr}:
    `%~>%`(`%;%`_config(z, [`HANDLER_%{%}%`_instr(n, [CATCH_ALL_REF_catch(l)] ++ catch'*{catch' <- `catch'*`}, [REF.EXN_ADDR_instr(a) THROW_REF_instr])]), [REF.EXN_ADDR_instr(a) BR_instr(l)])

  ;; 8-reduction.watsup
  rule `throw_ref-handler-next`{z : state, n : n, catch : catch, `catch'*` : catch*, a : addr}:
    `%~>%`(`%;%`_config(z, [`HANDLER_%{%}%`_instr(n, [catch] ++ catch'*{catch' <- `catch'*`}, [REF.EXN_ADDR_instr(a) THROW_REF_instr])]), [`HANDLER_%{%}%`_instr(n, catch'*{catch' <- `catch'*`}, [REF.EXN_ADDR_instr(a) THROW_REF_instr])])
    -- otherwise

  ;; 8-reduction.watsup
  rule try_table{z : state, `val*` : val*, m : m, bt : blocktype, `catch*` : catch*, `instr*` : instr*, n : n, `t_1*` : valtype*, `t_2*` : valtype*}:
    `%~>%`(`%;%`_config(z, (val : val <: instr)^m{val <- `val*`} ++ [TRY_TABLE_instr(bt, `%`_list(catch*{catch <- `catch*`}), instr*{instr <- `instr*`})]), [`HANDLER_%{%}%`_instr(n, catch*{catch <- `catch*`}, [`LABEL_%{%}%`_instr(n, [], (val : val <: instr)^m{val <- `val*`} ++ instr*{instr <- `instr*`})])])
    -- if ($blocktype_(z, bt) = `%->%`_functype(`%`_resulttype(t_1^m{t_1 <- `t_1*`}), `%`_resulttype(t_2^n{t_2 <- `t_2*`})))

  ;; 8-reduction.watsup
  rule `ref.null-idx`{z : state, x : idx}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(_IDX_heaptype(x))]), [REF.NULL_instr(($type(z, x) : deftype <: heaptype))])

  ;; 8-reduction.watsup
  rule ref.func{z : state, x : idx}:
    `%~>%`(`%;%`_config(z, [REF.FUNC_instr(x)]), [REF.FUNC_ADDR_instr($moduleinst(z).FUNCS_moduleinst[x!`%`_idx.0])])

  ;; 8-reduction.watsup
  rule `ref.test-true`{s : store, f : frame, ref : ref, rt : reftype, rt' : reftype}:
    `%~>%`(`%;%`_config(`%;%`_state(s, f), [(ref : ref <: instr) REF.TEST_instr(rt)]), [CONST_instr(I32_numtype, `%`_num_(1))])
    -- Ref_type: `%|-%:%`(s, ref, rt')
    -- Reftype_sub: `%|-%<:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, rt', $inst_reftype(f.MODULE_frame, rt))

  ;; 8-reduction.watsup
  rule `ref.test-false`{s : store, f : frame, ref : ref, rt : reftype}:
    `%~>%`(`%;%`_config(`%;%`_state(s, f), [(ref : ref <: instr) REF.TEST_instr(rt)]), [CONST_instr(I32_numtype, `%`_num_(0))])
    -- otherwise

  ;; 8-reduction.watsup
  rule `ref.cast-succeed`{s : store, f : frame, ref : ref, rt : reftype, rt' : reftype}:
    `%~>%`(`%;%`_config(`%;%`_state(s, f), [(ref : ref <: instr) REF.CAST_instr(rt)]), [(ref : ref <: instr)])
    -- Ref_type: `%|-%:%`(s, ref, rt')
    -- Reftype_sub: `%|-%<:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [], RETURN ?(), REFS []}, rt', $inst_reftype(f.MODULE_frame, rt))

  ;; 8-reduction.watsup
  rule `ref.cast-fail`{s : store, f : frame, ref : ref, rt : reftype}:
    `%~>%`(`%;%`_config(`%;%`_state(s, f), [(ref : ref <: instr) REF.CAST_instr(rt)]), [TRAP_instr])
    -- otherwise

  ;; 8-reduction.watsup
  rule struct.new_default{z : state, x : idx, `val*` : val*, `mut*` : mut*, `zt*` : storagetype*}:
    `%~>%`(`%;%`_config(z, [STRUCT.NEW_DEFAULT_instr(x)]), (val : val <: instr)*{val <- `val*`} ++ [STRUCT.NEW_instr(x)])
    -- Expand: `%~~%`($type(z, x), STRUCT_comptype(`%`_structtype(`%%`_fieldtype(mut, zt)*{mut <- `mut*`, zt <- `zt*`})))
    -- (if ($default_($unpack(zt)) = ?(val)))*{val <- `val*`, zt <- `zt*`}

  ;; 8-reduction.watsup
  rule `struct.get-null`{z : state, ht : heaptype, `sx?` : sx?, x : idx, i : u32}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht) STRUCT.GET_instr(sx?{sx <- `sx?`}, x, i)]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `struct.get-struct`{z : state, a : addr, `sx?` : sx?, x : idx, i : u32, `zt*` : storagetype*, `mut*` : mut*}:
    `%~>%`(`%;%`_config(z, [REF.STRUCT_ADDR_instr(a) STRUCT.GET_instr(sx?{sx <- `sx?`}, x, i)]), [($unpackfield_(zt*{zt <- `zt*`}[i!`%`_u32.0], sx?{sx <- `sx?`}, $structinst(z)[a].FIELDS_structinst[i!`%`_u32.0]) : val <: instr)])
    -- Expand: `%~~%`($type(z, x), STRUCT_comptype(`%`_structtype(`%%`_fieldtype(mut, zt)*{mut <- `mut*`, zt <- `zt*`})))

  ;; 8-reduction.watsup
  rule array.new_default{z : state, n : n, x : idx, val : val, mut : mut, zt : storagetype}:
    `%~>%`(`%;%`_config(z, [CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.NEW_DEFAULT_instr(x)]), (val : val <: instr)^n{} ++ [ARRAY.NEW_FIXED_instr(x, `%`_u32(n))])
    -- Expand: `%~~%`($type(z, x), ARRAY_comptype(`%%`_arraytype(mut, zt)))
    -- if ($default_($unpack(zt)) = ?(val))

  ;; 8-reduction.watsup
  rule `array.new_elem-oob`{z : state, i : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.NEW_ELEM_instr(x, y)]), [TRAP_instr])
    -- if ((i!`%`_num_.0 + n) > |$elem(z, y).REFS_eleminst|)

  ;; 8-reduction.watsup
  rule `array.new_elem-alloc`{z : state, i : num_(I32_numtype), n : n, x : idx, y : idx, `ref*` : ref*}:
    `%~>%`(`%;%`_config(z, [CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.NEW_ELEM_instr(x, y)]), (ref : ref <: instr)^n{ref <- `ref*`} ++ [ARRAY.NEW_FIXED_instr(x, `%`_u32(n))])
    -- if (ref^n{ref <- `ref*`} = $elem(z, y).REFS_eleminst[i!`%`_num_.0 : n])

  ;; 8-reduction.watsup
  rule `array.new_data-oob`{z : state, i : num_(I32_numtype), n : n, x : idx, y : idx, mut : mut, zt : storagetype}:
    `%~>%`(`%;%`_config(z, [CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.NEW_DATA_instr(x, y)]), [TRAP_instr])
    -- Expand: `%~~%`($type(z, x), ARRAY_comptype(`%%`_arraytype(mut, zt)))
    -- if ((i!`%`_num_.0 + ((((n * $zsize(zt)) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$data(z, y).BYTES_datainst|)

  ;; 8-reduction.watsup
  rule `array.new_data-num`{z : state, i : num_(I32_numtype), n : n, x : idx, y : idx, zt : storagetype, `c*` : lit_(zt)*, mut : mut}:
    `%~>%`(`%;%`_config(z, [CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.NEW_DATA_instr(x, y)]), $const($cunpack(zt), $cunpacknum_(zt, c))^n{c <- `c*`} ++ [ARRAY.NEW_FIXED_instr(x, `%`_u32(n))])
    -- Expand: `%~~%`($type(z, x), ARRAY_comptype(`%%`_arraytype(mut, zt)))
    -- if ($concatn_(syntax byte, $zbytes_(zt, c)^n{c <- `c*`}, ((($zsize(zt) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) = $data(z, y).BYTES_datainst[i!`%`_num_.0 : ((((n * $zsize(zt)) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)])

  ;; 8-reduction.watsup
  rule `array.get-null`{z : state, ht : heaptype, i : num_(I32_numtype), `sx?` : sx?, x : idx}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht) CONST_instr(I32_numtype, i) ARRAY.GET_instr(sx?{sx <- `sx?`}, x)]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `array.get-oob`{z : state, a : addr, i : num_(I32_numtype), `sx?` : sx?, x : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) ARRAY.GET_instr(sx?{sx <- `sx?`}, x)]), [TRAP_instr])
    -- if (i!`%`_num_.0 >= |$arrayinst(z)[a].FIELDS_arrayinst|)

  ;; 8-reduction.watsup
  rule `array.get-array`{z : state, a : addr, i : num_(I32_numtype), `sx?` : sx?, x : idx, zt : storagetype, mut : mut}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) ARRAY.GET_instr(sx?{sx <- `sx?`}, x)]), [($unpackfield_(zt, sx?{sx <- `sx?`}, $arrayinst(z)[a].FIELDS_arrayinst[i!`%`_num_.0]) : val <: instr)])
    -- Expand: `%~~%`($type(z, x), ARRAY_comptype(`%%`_arraytype(mut, zt)))

  ;; 8-reduction.watsup
  rule `array.len-null`{z : state, ht : heaptype}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht) ARRAY.LEN_instr]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `array.len-array`{z : state, a : addr}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) ARRAY.LEN_instr]), [CONST_instr(I32_numtype, `%`_num_(|$arrayinst(z)[a].FIELDS_arrayinst|))])

  ;; 8-reduction.watsup
  rule `array.fill-null`{z : state, ht : heaptype, i : num_(I32_numtype), val : val, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht) CONST_instr(I32_numtype, i) (val : val <: instr) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.FILL_instr(x)]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `array.fill-oob`{z : state, a : addr, i : num_(I32_numtype), val : val, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) (val : val <: instr) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.FILL_instr(x)]), [TRAP_instr])
    -- if ((i!`%`_num_.0 + n) > |$arrayinst(z)[a].FIELDS_arrayinst|)

  ;; 8-reduction.watsup
  rule `array.fill-zero`{z : state, a : addr, i : num_(I32_numtype), val : val, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) (val : val <: instr) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.FILL_instr(x)]), [])
    -- otherwise
    -- if (n = 0)

  ;; 8-reduction.watsup
  rule `array.fill-succ`{z : state, a : addr, i : num_(I32_numtype), val : val, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) (val : val <: instr) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.FILL_instr(x)]), [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) (val : val <: instr) ARRAY.SET_instr(x) REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, `%`_num_((i!`%`_num_.0 + 1))) (val : val <: instr) CONST_instr(I32_numtype, `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) ARRAY.FILL_instr(x)])
    -- otherwise

  ;; 8-reduction.watsup
  rule `array.copy-null1`{z : state, ht_1 : heaptype, i_1 : num_(I32_numtype), ref : ref, i_2 : num_(I32_numtype), n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht_1) CONST_instr(I32_numtype, i_1) (ref : ref <: instr) CONST_instr(I32_numtype, i_2) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.COPY_instr(x_1, x_2)]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `array.copy-null2`{z : state, ref : ref, i_1 : num_(I32_numtype), ht_2 : heaptype, i_2 : num_(I32_numtype), n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [(ref : ref <: instr) CONST_instr(I32_numtype, i_1) REF.NULL_instr(ht_2) CONST_instr(I32_numtype, i_2) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.COPY_instr(x_1, x_2)]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `array.copy-oob1`{z : state, a_1 : addr, i_1 : num_(I32_numtype), a_2 : addr, i_2 : num_(I32_numtype), n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a_1) CONST_instr(I32_numtype, i_1) REF.ARRAY_ADDR_instr(a_2) CONST_instr(I32_numtype, i_2) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.COPY_instr(x_1, x_2)]), [TRAP_instr])
    -- if ((i_1!`%`_num_.0 + n) > |$arrayinst(z)[a_1].FIELDS_arrayinst|)

  ;; 8-reduction.watsup
  rule `array.copy-oob2`{z : state, a_1 : addr, i_1 : num_(I32_numtype), a_2 : addr, i_2 : num_(I32_numtype), n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a_1) CONST_instr(I32_numtype, i_1) REF.ARRAY_ADDR_instr(a_2) CONST_instr(I32_numtype, i_2) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.COPY_instr(x_1, x_2)]), [TRAP_instr])
    -- if ((i_2!`%`_num_.0 + n) > |$arrayinst(z)[a_2].FIELDS_arrayinst|)

  ;; 8-reduction.watsup
  rule `array.copy-zero`{z : state, a_1 : addr, i_1 : num_(I32_numtype), a_2 : addr, i_2 : num_(I32_numtype), n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a_1) CONST_instr(I32_numtype, i_1) REF.ARRAY_ADDR_instr(a_2) CONST_instr(I32_numtype, i_2) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.COPY_instr(x_1, x_2)]), [])
    -- otherwise
    -- if (n = 0)

  ;; 8-reduction.watsup
  rule `array.copy-le`{z : state, a_1 : addr, i_1 : num_(I32_numtype), a_2 : addr, i_2 : num_(I32_numtype), n : n, x_1 : idx, x_2 : idx, `sx?` : sx?, mut : mut, zt_2 : storagetype}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a_1) CONST_instr(I32_numtype, i_1) REF.ARRAY_ADDR_instr(a_2) CONST_instr(I32_numtype, i_2) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.COPY_instr(x_1, x_2)]), [REF.ARRAY_ADDR_instr(a_1) CONST_instr(I32_numtype, i_1) REF.ARRAY_ADDR_instr(a_2) CONST_instr(I32_numtype, i_2) ARRAY.GET_instr(sx?{sx <- `sx?`}, x_2) ARRAY.SET_instr(x_1) REF.ARRAY_ADDR_instr(a_1) CONST_instr(I32_numtype, `%`_num_((i_1!`%`_num_.0 + 1))) REF.ARRAY_ADDR_instr(a_2) CONST_instr(I32_numtype, `%`_num_((i_2!`%`_num_.0 + 1))) CONST_instr(I32_numtype, `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) ARRAY.COPY_instr(x_1, x_2)])
    -- otherwise
    -- Expand: `%~~%`($type(z, x_2), ARRAY_comptype(`%%`_arraytype(mut, zt_2)))
    -- if ((i_1!`%`_num_.0 <= i_2!`%`_num_.0) /\ (sx?{sx <- `sx?`} = $sx(zt_2)))

  ;; 8-reduction.watsup
  rule `array.copy-gt`{z : state, a_1 : addr, i_1 : num_(I32_numtype), a_2 : addr, i_2 : num_(I32_numtype), n : n, x_1 : idx, x_2 : idx, `sx?` : sx?, mut : mut, zt_2 : storagetype}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a_1) CONST_instr(I32_numtype, i_1) REF.ARRAY_ADDR_instr(a_2) CONST_instr(I32_numtype, i_2) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.COPY_instr(x_1, x_2)]), [REF.ARRAY_ADDR_instr(a_1) CONST_instr(I32_numtype, `%`_num_(((((i_1!`%`_num_.0 + n) : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) REF.ARRAY_ADDR_instr(a_2) CONST_instr(I32_numtype, `%`_num_(((((i_2!`%`_num_.0 + n) : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) ARRAY.GET_instr(sx?{sx <- `sx?`}, x_2) ARRAY.SET_instr(x_1) REF.ARRAY_ADDR_instr(a_1) CONST_instr(I32_numtype, i_1) REF.ARRAY_ADDR_instr(a_2) CONST_instr(I32_numtype, i_2) CONST_instr(I32_numtype, `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) ARRAY.COPY_instr(x_1, x_2)])
    -- otherwise
    -- Expand: `%~~%`($type(z, x_2), ARRAY_comptype(`%%`_arraytype(mut, zt_2)))
    -- if (sx?{sx <- `sx?`} = $sx(zt_2))

  ;; 8-reduction.watsup
  rule `array.init_elem-null`{z : state, ht : heaptype, i : num_(I32_numtype), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht) CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.INIT_ELEM_instr(x, y)]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `array.init_elem-oob1`{z : state, a : addr, i : num_(I32_numtype), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.INIT_ELEM_instr(x, y)]), [TRAP_instr])
    -- if ((i!`%`_num_.0 + n) > |$arrayinst(z)[a].FIELDS_arrayinst|)

  ;; 8-reduction.watsup
  rule `array.init_elem-oob2`{z : state, a : addr, i : num_(I32_numtype), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.INIT_ELEM_instr(x, y)]), [TRAP_instr])
    -- if ((j!`%`_num_.0 + n) > |$elem(z, y).REFS_eleminst|)

  ;; 8-reduction.watsup
  rule `array.init_elem-zero`{z : state, a : addr, i : num_(I32_numtype), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.INIT_ELEM_instr(x, y)]), [])
    -- otherwise
    -- if (n = 0)

  ;; 8-reduction.watsup
  rule `array.init_elem-succ`{z : state, a : addr, i : num_(I32_numtype), j : num_(I32_numtype), n : n, x : idx, y : idx, ref : ref}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.INIT_ELEM_instr(x, y)]), [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) (ref : ref <: instr) ARRAY.SET_instr(x) REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, `%`_num_((i!`%`_num_.0 + 1))) CONST_instr(I32_numtype, `%`_num_((j!`%`_num_.0 + 1))) CONST_instr(I32_numtype, `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) ARRAY.INIT_ELEM_instr(x, y)])
    -- otherwise
    -- if (ref = $elem(z, y).REFS_eleminst[j!`%`_num_.0])

  ;; 8-reduction.watsup
  rule `array.init_data-null`{z : state, ht : heaptype, i : num_(I32_numtype), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht) CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.INIT_DATA_instr(x, y)]), [TRAP_instr])

  ;; 8-reduction.watsup
  rule `array.init_data-oob1`{z : state, a : addr, i : num_(I32_numtype), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.INIT_DATA_instr(x, y)]), [TRAP_instr])
    -- if ((i!`%`_num_.0 + n) > |$arrayinst(z)[a].FIELDS_arrayinst|)

  ;; 8-reduction.watsup
  rule `array.init_data-oob2`{z : state, a : addr, i : num_(I32_numtype), j : num_(I32_numtype), n : n, x : idx, y : idx, mut : mut, zt : storagetype}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.INIT_DATA_instr(x, y)]), [TRAP_instr])
    -- Expand: `%~~%`($type(z, x), ARRAY_comptype(`%%`_arraytype(mut, zt)))
    -- if ((j!`%`_num_.0 + ((((n * $zsize(zt)) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$data(z, y).BYTES_datainst|)

  ;; 8-reduction.watsup
  rule `array.init_data-zero`{z : state, a : addr, i : num_(I32_numtype), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.INIT_DATA_instr(x, y)]), [])
    -- otherwise
    -- if (n = 0)

  ;; 8-reduction.watsup
  rule `array.init_data-num`{z : state, a : addr, i : num_(I32_numtype), j : num_(I32_numtype), n : n, x : idx, y : idx, zt : storagetype, c : lit_(zt), mut : mut}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) ARRAY.INIT_DATA_instr(x, y)]), [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) $const($cunpack(zt), $cunpacknum_(zt, c)) ARRAY.SET_instr(x) REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, `%`_num_((i!`%`_num_.0 + 1))) CONST_instr(I32_numtype, `%`_num_((j!`%`_num_.0 + ((($zsize(zt) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)))) CONST_instr(I32_numtype, `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) ARRAY.INIT_DATA_instr(x, y)])
    -- otherwise
    -- Expand: `%~~%`($type(z, x), ARRAY_comptype(`%%`_arraytype(mut, zt)))
    -- if ($zbytes_(zt, c) = $data(z, y).BYTES_datainst[j!`%`_num_.0 : ((($zsize(zt) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)])

  ;; 8-reduction.watsup
  rule local.get{z : state, x : idx, val : val}:
    `%~>%`(`%;%`_config(z, [LOCAL.GET_instr(x)]), [(val : val <: instr)])
    -- if ($local(z, x) = ?(val))

  ;; 8-reduction.watsup
  rule global.get{z : state, x : idx, val : val}:
    `%~>%`(`%;%`_config(z, [GLOBAL.GET_instr(x)]), [(val : val <: instr)])
    -- if ($global(z, x).VALUE_globalinst = val)

  ;; 8-reduction.watsup
  rule `table.get-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) TABLE.GET_instr(x)]), [TRAP_instr])
    -- if (i!`%`_num_.0 >= |$table(z, x).REFS_tableinst|)

  ;; 8-reduction.watsup
  rule `table.get-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) TABLE.GET_instr(x)]), [($table(z, x).REFS_tableinst[i!`%`_num_.0] : ref <: instr)])
    -- if (i!`%`_num_.0 < |$table(z, x).REFS_tableinst|)

  ;; 8-reduction.watsup
  rule table.size{z : state, x : idx, at : addrtype, n : n, lim : limits, rt : reftype}:
    `%~>%`(`%;%`_config(z, [TABLE.SIZE_instr(x)]), [CONST_instr((at : addrtype <: numtype), `%`_num_(n))])
    -- if (|$table(z, x).REFS_tableinst| = n)
    -- if ($table(z, x).TYPE_tableinst = `%%%`_tabletype(at, lim, rt))

  ;; 8-reduction.watsup
  rule `table.fill-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), val : val, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) (val : val <: instr) CONST_instr((at : addrtype <: numtype), `%`_num_(n)) TABLE.FILL_instr(x)]), [TRAP_instr])
    -- if ((i!`%`_num_.0 + n) > |$table(z, x).REFS_tableinst|)

  ;; 8-reduction.watsup
  rule `table.fill-zero`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), val : val, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) (val : val <: instr) CONST_instr((at : addrtype <: numtype), `%`_num_(n)) TABLE.FILL_instr(x)]), [])
    -- otherwise
    -- if (n = 0)

  ;; 8-reduction.watsup
  rule `table.fill-succ`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), val : val, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) (val : val <: instr) CONST_instr((at : addrtype <: numtype), `%`_num_(n)) TABLE.FILL_instr(x)]), [CONST_instr((at : addrtype <: numtype), i) (val : val <: instr) TABLE.SET_instr(x) CONST_instr((at : addrtype <: numtype), `%`_num_((i!`%`_num_.0 + 1))) (val : val <: instr) CONST_instr((at : addrtype <: numtype), `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) TABLE.FILL_instr(x)])
    -- otherwise

  ;; 8-reduction.watsup
  rule `table.copy-oob`{z : state, at_1 : addrtype, i_1 : num_((at_1 : addrtype <: numtype)), at_2 : addrtype, i_2 : num_((at_2 : addrtype <: numtype)), at' : addrtype, n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) CONST_instr((at' : addrtype <: numtype), `%`_num_(n)) TABLE.COPY_instr(x_1, x_2)]), [TRAP_instr])
    -- if (((i_1!`%`_num_.0 + n) > |$table(z, x_1).REFS_tableinst|) \/ ((i_2!`%`_num_.0 + n) > |$table(z, x_2).REFS_tableinst|))

  ;; 8-reduction.watsup
  rule `table.copy-zero`{z : state, at_1 : addrtype, i_1 : num_((at_1 : addrtype <: numtype)), at_2 : addrtype, i_2 : num_((at_2 : addrtype <: numtype)), at' : addrtype, n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) CONST_instr((at' : addrtype <: numtype), `%`_num_(n)) TABLE.COPY_instr(x_1, x_2)]), [])
    -- otherwise
    -- if (n = 0)

  ;; 8-reduction.watsup
  rule `table.copy-le`{z : state, at_1 : addrtype, i_1 : num_((at_1 : addrtype <: numtype)), at_2 : addrtype, i_2 : num_((at_2 : addrtype <: numtype)), at' : addrtype, n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) CONST_instr((at' : addrtype <: numtype), `%`_num_(n)) TABLE.COPY_instr(x_1, x_2)]), [CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) TABLE.GET_instr(x_2) TABLE.SET_instr(x_1) CONST_instr((at_1 : addrtype <: numtype), `%`_num_((i_1!`%`_num_.0 + 1))) CONST_instr((at_2 : addrtype <: numtype), `%`_num_((i_2!`%`_num_.0 + 1))) CONST_instr((at' : addrtype <: numtype), `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) TABLE.COPY_instr(x_1, x_2)])
    -- otherwise
    -- if (i_1!`%`_num_.0 <= i_2!`%`_num_.0)

  ;; 8-reduction.watsup
  rule `table.copy-gt`{z : state, at_1 : addrtype, i_1 : num_((at_1 : addrtype <: numtype)), at_2 : addrtype, i_2 : num_((at_2 : addrtype <: numtype)), at' : addrtype, n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) CONST_instr((at' : addrtype <: numtype), `%`_num_(n)) TABLE.COPY_instr(x_1, x_2)]), [CONST_instr((at_1 : addrtype <: numtype), `%`_num_(((((i_1!`%`_num_.0 + n) : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) CONST_instr((at_2 : addrtype <: numtype), `%`_num_(((((i_2!`%`_num_.0 + n) : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) TABLE.GET_instr(x_2) TABLE.SET_instr(x_1) CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) CONST_instr((at' : addrtype <: numtype), `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) TABLE.COPY_instr(x_1, x_2)])
    -- otherwise

  ;; 8-reduction.watsup
  rule `table.init-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) TABLE.INIT_instr(x, y)]), [TRAP_instr])
    -- if (((i!`%`_num_.0 + n) > |$table(z, x).REFS_tableinst|) \/ ((j!`%`_num_.0 + n) > |$elem(z, y).REFS_eleminst|))

  ;; 8-reduction.watsup
  rule `table.init-zero`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) TABLE.INIT_instr(x, y)]), [])
    -- otherwise
    -- if (n = 0)

  ;; 8-reduction.watsup
  rule `table.init-succ`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) TABLE.INIT_instr(x, y)]), [CONST_instr((at : addrtype <: numtype), i) ($elem(z, y).REFS_eleminst[j!`%`_num_.0] : ref <: instr) TABLE.SET_instr(x) CONST_instr((at : addrtype <: numtype), `%`_num_((i!`%`_num_.0 + 1))) CONST_instr(I32_numtype, `%`_num_((j!`%`_num_.0 + 1))) CONST_instr(I32_numtype, `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) TABLE.INIT_instr(x, y)])
    -- otherwise

  ;; 8-reduction.watsup
  rule `load-num-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), nt : numtype, x : idx, ao : memarg}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) LOAD_instr(nt, ?(), x, ao)]), [TRAP_instr])
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + ((($size(nt) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup
  rule `load-num-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), nt : numtype, x : idx, ao : memarg, c : num_(nt)}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) LOAD_instr(nt, ?(), x, ao)]), [CONST_instr(nt, c)])
    -- if ($nbytes_(nt, c) = $mem(z, x).BYTES_meminst[(i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) : ((($size(nt) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)])

  ;; 8-reduction.watsup
  rule `load-pack-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), Inn : Inn, n : n, sx : sx, x : idx, ao : memarg}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) LOAD_instr((Inn : Inn <: numtype), ?(`%_%`_loadop_(`%`_sz(n), sx)), x, ao)]), [TRAP_instr])
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + (((n : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup
  rule `load-pack-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), Inn : Inn, n : n, sx : sx, x : idx, ao : memarg, c : iN(n)}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) LOAD_instr((Inn : Inn <: numtype), ?(`%_%`_loadop_(`%`_sz(n), sx)), x, ao)]), [CONST_instr((Inn : Inn <: numtype), $extend__(n, $size((Inn : Inn <: numtype)), sx, c))])
    -- if ($ibytes_(n, c) = $mem(z, x).BYTES_meminst[(i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) : (((n : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)])

  ;; 8-reduction.watsup
  rule `vload-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), x : idx, ao : memarg}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VLOAD_instr(V128_vectype, ?(), x, ao)]), [TRAP_instr])
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + ((($vsize(V128_vectype) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup
  rule `vload-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), x : idx, ao : memarg, c : vec_(V128_Vnn)}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VLOAD_instr(V128_vectype, ?(), x, ao)]), [VCONST_instr(V128_vectype, c)])
    -- if ($vbytes_(V128_vectype, c) = $mem(z, x).BYTES_meminst[(i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) : ((($vsize(V128_vectype) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)])

  ;; 8-reduction.watsup
  rule `vload-pack-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), M : M, K : K, sx : sx, x : idx, ao : memarg}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VLOAD_instr(V128_vectype, ?(`SHAPE%X%_%`_vloadop_(`%`_sz(M), K, sx)), x, ao)]), [TRAP_instr])
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + ((((M * K) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup
  rule `vload-pack-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), M : M, K : K, sx : sx, x : idx, ao : memarg, c : vec_(V128_Vnn), `j*` : iN(M)*, `k*` : nat*, Jnn : Jnn}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VLOAD_instr(V128_vectype, ?(`SHAPE%X%_%`_vloadop_(`%`_sz(M), K, sx)), x, ao)]), [VCONST_instr(V128_vectype, c)])
    -- (if ($ibytes_(M, j) = $mem(z, x).BYTES_meminst[((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + ((((k * M) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) : (((M : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)]))^(k<K){j <- `j*`, k <- `k*`}
    -- if ((c = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(K)), $extend__(M, $lsizenn((Jnn : Jnn <: lanetype)), sx, j)^K{j <- `j*`})) /\ ($lsizenn((Jnn : Jnn <: lanetype)) = (M * 2)))

  ;; 8-reduction.watsup
  rule `vload-splat-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), N : N, x : idx, ao : memarg}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VLOAD_instr(V128_vectype, ?(SPLAT_vloadop_(`%`_sz(N))), x, ao)]), [TRAP_instr])
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + (((N : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup
  rule `vload-splat-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), N : N, x : idx, ao : memarg, c : vec_(V128_Vnn), j : iN(N), Jnn : Jnn, M : M}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VLOAD_instr(V128_vectype, ?(SPLAT_vloadop_(`%`_sz(N))), x, ao)]), [VCONST_instr(V128_vectype, c)])
    -- if ($ibytes_(N, j) = $mem(z, x).BYTES_meminst[(i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) : (((N : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)])
    -- if (N = $lsize((Jnn : Jnn <: lanetype)))
    -- if ((M : nat <:> rat) = ((128 : nat <:> rat) / (N : nat <:> rat)))
    -- if (c = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), `%`_lane_(j!`%`_iN.0)^M{}))

  ;; 8-reduction.watsup
  rule `vload-zero-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), N : N, x : idx, ao : memarg}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VLOAD_instr(V128_vectype, ?(ZERO_vloadop_(`%`_sz(N))), x, ao)]), [TRAP_instr])
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + (((N : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup
  rule `vload-zero-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), N : N, x : idx, ao : memarg, c : vec_(V128_Vnn), j : iN(N)}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VLOAD_instr(V128_vectype, ?(ZERO_vloadop_(`%`_sz(N))), x, ao)]), [VCONST_instr(V128_vectype, c)])
    -- if ($ibytes_(N, j) = $mem(z, x).BYTES_meminst[(i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) : (((N : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)])
    -- if (c = $extend__(N, 128, U_sx, j))

  ;; 8-reduction.watsup
  rule `vload_lane-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), c_1 : vec_(V128_Vnn), N : N, x : idx, ao : memarg, j : laneidx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VCONST_instr(V128_vectype, c_1) VLOAD_LANE_instr(V128_vectype, `%`_sz(N), x, ao, j)]), [TRAP_instr])
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + (((N : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup
  rule `vload_lane-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), c_1 : vec_(V128_Vnn), N : N, x : idx, ao : memarg, j : laneidx, c : vec_(V128_Vnn), k : iN(N), Jnn : Jnn, M : M}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VCONST_instr(V128_vectype, c_1) VLOAD_LANE_instr(V128_vectype, `%`_sz(N), x, ao, j)]), [VCONST_instr(V128_vectype, c)])
    -- if ($ibytes_(N, k) = $mem(z, x).BYTES_meminst[(i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) : (((N : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)])
    -- if (N = $lsize((Jnn : Jnn <: lanetype)))
    -- if ((M : nat <:> rat) = (($vsize(V128_vectype) : nat <:> rat) / (N : nat <:> rat)))
    -- if (c = $invlanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), $lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c_1)[[j!`%`_laneidx.0] = `%`_lane_(k!`%`_iN.0)]))

  ;; 8-reduction.watsup
  rule memory.size{z : state, x : idx, at : addrtype, n : n, lim : limits}:
    `%~>%`(`%;%`_config(z, [MEMORY.SIZE_instr(x)]), [CONST_instr((at : addrtype <: numtype), `%`_num_(n))])
    -- if ((n * (64 * $Ki)) = |$mem(z, x).BYTES_meminst|)
    -- if ($mem(z, x).TYPE_meminst = `%%PAGE`_memtype(at, lim))

  ;; 8-reduction.watsup
  rule `memory.fill-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), val : val, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) (val : val <: instr) CONST_instr((at : addrtype <: numtype), `%`_num_(n)) MEMORY.FILL_instr(x)]), [TRAP_instr])
    -- if ((i!`%`_num_.0 + n) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup
  rule `memory.fill-zero`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), val : val, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) (val : val <: instr) CONST_instr((at : addrtype <: numtype), `%`_num_(n)) MEMORY.FILL_instr(x)]), [])
    -- otherwise
    -- if (n = 0)

  ;; 8-reduction.watsup
  rule `memory.fill-succ`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), val : val, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) (val : val <: instr) CONST_instr((at : addrtype <: numtype), `%`_num_(n)) MEMORY.FILL_instr(x)]), [CONST_instr((at : addrtype <: numtype), i) (val : val <: instr) STORE_instr(I32_numtype, ?(`%`_storeop_(`%`_sz(8))), x, $memarg0) CONST_instr((at : addrtype <: numtype), `%`_num_((i!`%`_num_.0 + 1))) (val : val <: instr) CONST_instr((at : addrtype <: numtype), `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) MEMORY.FILL_instr(x)])
    -- otherwise

  ;; 8-reduction.watsup
  rule `memory.copy-oob`{z : state, at_1 : addrtype, i_1 : num_((at_1 : addrtype <: numtype)), at_2 : addrtype, i_2 : num_((at_2 : addrtype <: numtype)), at' : addrtype, n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) CONST_instr((at' : addrtype <: numtype), `%`_num_(n)) MEMORY.COPY_instr(x_1, x_2)]), [TRAP_instr])
    -- if (((i_1!`%`_num_.0 + n) > |$mem(z, x_1).BYTES_meminst|) \/ ((i_2!`%`_num_.0 + n) > |$mem(z, x_2).BYTES_meminst|))

  ;; 8-reduction.watsup
  rule `memory.copy-zero`{z : state, at_1 : addrtype, i_1 : num_((at_1 : addrtype <: numtype)), at_2 : addrtype, i_2 : num_((at_2 : addrtype <: numtype)), at' : addrtype, n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) CONST_instr((at' : addrtype <: numtype), `%`_num_(n)) MEMORY.COPY_instr(x_1, x_2)]), [])
    -- otherwise
    -- if (n = 0)

  ;; 8-reduction.watsup
  rule `memory.copy-le`{z : state, at_1 : addrtype, i_1 : num_((at_1 : addrtype <: numtype)), at_2 : addrtype, i_2 : num_((at_2 : addrtype <: numtype)), at' : addrtype, n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) CONST_instr((at' : addrtype <: numtype), `%`_num_(n)) MEMORY.COPY_instr(x_1, x_2)]), [CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) LOAD_instr(I32_numtype, ?(`%_%`_loadop_(`%`_sz(8), U_sx)), x_2, $memarg0) STORE_instr(I32_numtype, ?(`%`_storeop_(`%`_sz(8))), x_1, $memarg0) CONST_instr((at_1 : addrtype <: numtype), `%`_num_((i_1!`%`_num_.0 + 1))) CONST_instr((at_2 : addrtype <: numtype), `%`_num_((i_2!`%`_num_.0 + 1))) CONST_instr((at' : addrtype <: numtype), `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) MEMORY.COPY_instr(x_1, x_2)])
    -- otherwise
    -- if (i_1!`%`_num_.0 <= i_2!`%`_num_.0)

  ;; 8-reduction.watsup
  rule `memory.copy-gt`{z : state, at_1 : addrtype, i_1 : num_((at_1 : addrtype <: numtype)), at_2 : addrtype, i_2 : num_((at_2 : addrtype <: numtype)), at' : addrtype, n : n, x_1 : idx, x_2 : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) CONST_instr((at' : addrtype <: numtype), `%`_num_(n)) MEMORY.COPY_instr(x_1, x_2)]), [CONST_instr((at_1 : addrtype <: numtype), `%`_num_(((((i_1!`%`_num_.0 + n) : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) CONST_instr((at_2 : addrtype <: numtype), `%`_num_(((((i_2!`%`_num_.0 + n) : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) LOAD_instr(I32_numtype, ?(`%_%`_loadop_(`%`_sz(8), U_sx)), x_2, $memarg0) STORE_instr(I32_numtype, ?(`%`_storeop_(`%`_sz(8))), x_1, $memarg0) CONST_instr((at_1 : addrtype <: numtype), i_1) CONST_instr((at_2 : addrtype <: numtype), i_2) CONST_instr((at' : addrtype <: numtype), `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) MEMORY.COPY_instr(x_1, x_2)])
    -- otherwise

  ;; 8-reduction.watsup
  rule `memory.init-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) MEMORY.INIT_instr(x, y)]), [TRAP_instr])
    -- if (((i!`%`_num_.0 + n) > |$mem(z, x).BYTES_meminst|) \/ ((j!`%`_num_.0 + n) > |$data(z, y).BYTES_datainst|))

  ;; 8-reduction.watsup
  rule `memory.init-zero`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) MEMORY.INIT_instr(x, y)]), [])
    -- otherwise
    -- if (n = 0)

  ;; 8-reduction.watsup
  rule `memory.init-succ`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), j : num_(I32_numtype), n : n, x : idx, y : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) CONST_instr(I32_numtype, j) CONST_instr(I32_numtype, `%`_num_(n)) MEMORY.INIT_instr(x, y)]), [CONST_instr((at : addrtype <: numtype), i) CONST_instr(I32_numtype, `%`_num_($data(z, y).BYTES_datainst[j!`%`_num_.0]!`%`_byte.0)) STORE_instr(I32_numtype, ?(`%`_storeop_(`%`_sz(8))), x, $memarg0) CONST_instr((at : addrtype <: numtype), `%`_num_((i!`%`_num_.0 + 1))) CONST_instr(I32_numtype, `%`_num_((j!`%`_num_.0 + 1))) CONST_instr(I32_numtype, `%`_num_((((n : nat <:> int) - (1 : nat <:> int)) : int <:> nat))) MEMORY.INIT_instr(x, y)])
    -- otherwise

;; 8-reduction.watsup
rec {

;; 8-reduction.watsup:5.1-5.88
relation Step: `%~>%`(config, config)
  ;; 8-reduction.watsup:13.1-15.34
  rule pure{z : state, `instr*` : instr*, `instr'*` : instr*}:
    `%~>%`(`%;%`_config(z, instr*{instr <- `instr*`}), `%;%`_config(z, instr'*{instr' <- `instr'*`}))
    -- Step_pure: `%~>%`(instr*{instr <- `instr*`}, instr'*{instr' <- `instr'*`})

  ;; 8-reduction.watsup:17.1-19.37
  rule read{z : state, `instr*` : instr*, `instr'*` : instr*}:
    `%~>%`(`%;%`_config(z, instr*{instr <- `instr*`}), `%;%`_config(z, instr'*{instr' <- `instr'*`}))
    -- Step_read: `%~>%`(`%;%`_config(z, instr*{instr <- `instr*`}), instr'*{instr' <- `instr'*`})

  ;; 8-reduction.watsup:32.1-35.41
  rule `ctxt-instrs`{z : state, `val*` : val*, `instr*` : instr*, `instr_1*` : instr*, z' : state, `instr'*` : instr*}:
    `%~>%`(`%;%`_config(z, (val : val <: instr)*{val <- `val*`} ++ instr*{instr <- `instr*`} ++ instr_1*{instr_1 <- `instr_1*`}), `%;%`_config(z', (val : val <: instr)*{val <- `val*`} ++ instr'*{instr' <- `instr'*`} ++ instr_1*{instr_1 <- `instr_1*`}))
    -- Step: `%~>%`(`%;%`_config(z, instr*{instr <- `instr*`}), `%;%`_config(z', instr'*{instr' <- `instr'*`}))
    -- if ((val*{val <- `val*`} =/= []) \/ (instr_1*{instr_1 <- `instr_1*`} =/= []))

  ;; 8-reduction.watsup:37.1-39.36
  rule `ctxt-label`{z : state, n : n, `instr_0*` : instr*, `instr*` : instr*, z' : state, `instr'*` : instr*}:
    `%~>%`(`%;%`_config(z, [`LABEL_%{%}%`_instr(n, instr_0*{instr_0 <- `instr_0*`}, instr*{instr <- `instr*`})]), `%;%`_config(z', [`LABEL_%{%}%`_instr(n, instr_0*{instr_0 <- `instr_0*`}, instr'*{instr' <- `instr'*`})]))
    -- Step: `%~>%`(`%;%`_config(z, instr*{instr <- `instr*`}), `%;%`_config(z', instr'*{instr' <- `instr'*`}))

  ;; 8-reduction.watsup:41.1-43.44
  rule `ctxt-frame`{s : store, f : frame, n : n, f' : frame, `instr*` : instr*, s' : store, `instr'*` : instr*}:
    `%~>%`(`%;%`_config(`%;%`_state(s, f), [`FRAME_%{%}%`_instr(n, f', instr*{instr <- `instr*`})]), `%;%`_config(`%;%`_state(s', f), [`FRAME_%{%}%`_instr(n, f', instr'*{instr' <- `instr'*`})]))
    -- Step: `%~>%`(`%;%`_config(`%;%`_state(s, f'), instr*{instr <- `instr*`}), `%;%`_config(`%;%`_state(s', f'), instr'*{instr' <- `instr'*`}))

  ;; 8-reduction.watsup:227.1-231.49
  rule throw{z : state, `val*` : val*, n : n, x : idx, exn : exninst, a : addr, `t*` : valtype*}:
    `%~>%`(`%;%`_config(z, (val : val <: instr)^n{val <- `val*`} ++ [THROW_instr(x)]), `%;%`_config($add_exninst(z, [exn]), [REF.EXN_ADDR_instr(a) THROW_REF_instr]))
    -- Expand: `%~~%`($tag(z, x).TYPE_taginst, FUNC_comptype(`%->%`_functype(`%`_resulttype(t^n{t <- `t*`}), `%`_resulttype([]))))
    -- if (a = |$exninst(z)|)
    -- if (exn = {TAG $tagaddr(z)[x!`%`_idx.0], FIELDS val^n{val <- `val*`}})

  ;; 8-reduction.watsup:406.1-410.65
  rule struct.new{z : state, `val*` : val*, n : n, x : idx, si : structinst, a : addr, `mut*` : mut*, `zt*` : storagetype*}:
    `%~>%`(`%;%`_config(z, (val : val <: instr)^n{val <- `val*`} ++ [STRUCT.NEW_instr(x)]), `%;%`_config($add_structinst(z, [si]), [REF.STRUCT_ADDR_instr(a)]))
    -- Expand: `%~~%`($type(z, x), STRUCT_comptype(`%`_structtype(`%%`_fieldtype(mut, zt)^n{mut <- `mut*`, zt <- `zt*`})))
    -- if (a = |$structinst(z)|)
    -- if (si = {TYPE $type(z, x), FIELDS $packfield_(zt, val)^n{val <- `val*`, zt <- `zt*`}})

  ;; 8-reduction.watsup:426.1-427.53
  rule `struct.set-null`{z : state, ht : heaptype, val : val, x : idx, i : u32}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht) (val : val <: instr) STRUCT.SET_instr(x, i)]), `%;%`_config(z, [TRAP_instr]))

  ;; 8-reduction.watsup:429.1-431.45
  rule `struct.set-struct`{z : state, a : addr, val : val, x : idx, i : u32, `zt*` : storagetype*, `mut*` : mut*}:
    `%~>%`(`%;%`_config(z, [REF.STRUCT_ADDR_instr(a) (val : val <: instr) STRUCT.SET_instr(x, i)]), `%;%`_config($with_struct(z, a, i!`%`_u32.0, $packfield_(zt*{zt <- `zt*`}[i!`%`_u32.0], val)), []))
    -- Expand: `%~~%`($type(z, x), STRUCT_comptype(`%`_structtype(`%%`_fieldtype(mut, zt)*{mut <- `mut*`, zt <- `zt*`})))

  ;; 8-reduction.watsup:444.1-449.65
  rule array.new_fixed{z : state, `val*` : val*, n : n, x : idx, ai : arrayinst, a : addr, mut : mut, zt : storagetype}:
    `%~>%`(`%;%`_config(z, (val : val <: instr)^n{val <- `val*`} ++ [ARRAY.NEW_FIXED_instr(x, `%`_u32(n))]), `%;%`_config($add_arrayinst(z, [ai]), [REF.ARRAY_ADDR_instr(a)]))
    -- Expand: `%~~%`($type(z, x), ARRAY_comptype(`%%`_arraytype(mut, zt)))
    -- if ((a = |$arrayinst(z)|) /\ (ai = {TYPE $type(z, x), FIELDS $packfield_(zt, val)^n{val <- `val*`}}))

  ;; 8-reduction.watsup:489.1-490.64
  rule `array.set-null`{z : state, ht : heaptype, i : num_(I32_numtype), val : val, x : idx}:
    `%~>%`(`%;%`_config(z, [REF.NULL_instr(ht) CONST_instr(I32_numtype, i) (val : val <: instr) ARRAY.SET_instr(x)]), `%;%`_config(z, [TRAP_instr]))

  ;; 8-reduction.watsup:492.1-494.39
  rule `array.set-oob`{z : state, a : addr, i : num_(I32_numtype), val : val, x : idx}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) (val : val <: instr) ARRAY.SET_instr(x)]), `%;%`_config(z, [TRAP_instr]))
    -- if (i!`%`_num_.0 >= |$arrayinst(z)[a].FIELDS_arrayinst|)

  ;; 8-reduction.watsup:496.1-499.43
  rule `array.set-array`{z : state, a : addr, i : num_(I32_numtype), val : val, x : idx, zt : storagetype, mut : mut}:
    `%~>%`(`%;%`_config(z, [REF.ARRAY_ADDR_instr(a) CONST_instr(I32_numtype, i) (val : val <: instr) ARRAY.SET_instr(x)]), `%;%`_config($with_array(z, a, i!`%`_num_.0, $packfield_(zt, val)), []))
    -- Expand: `%~~%`($type(z, x), ARRAY_comptype(`%%`_arraytype(mut, zt)))

  ;; 8-reduction.watsup:779.1-780.56
  rule local.set{z : state, val : val, x : idx}:
    `%~>%`(`%;%`_config(z, [(val : val <: instr) LOCAL.SET_instr(x)]), `%;%`_config($with_local(z, x, val), []))

  ;; 8-reduction.watsup:792.1-793.58
  rule global.set{z : state, val : val, x : idx}:
    `%~>%`(`%;%`_config(z, [(val : val <: instr) GLOBAL.SET_instr(x)]), `%;%`_config($with_global(z, x, val), []))

  ;; 8-reduction.watsup:806.1-808.33
  rule `table.set-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), ref : ref, x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) (ref : ref <: instr) TABLE.SET_instr(x)]), `%;%`_config(z, [TRAP_instr]))
    -- if (i!`%`_num_.0 >= |$table(z, x).REFS_tableinst|)

  ;; 8-reduction.watsup:810.1-812.32
  rule `table.set-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), ref : ref, x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) (ref : ref <: instr) TABLE.SET_instr(x)]), `%;%`_config($with_table(z, x, i!`%`_num_.0, ref), []))
    -- if (i!`%`_num_.0 < |$table(z, x).REFS_tableinst|)

  ;; 8-reduction.watsup:821.1-824.46
  rule `table.grow-succeed`{z : state, ref : ref, at : addrtype, n : n, x : idx, ti : tableinst}:
    `%~>%`(`%;%`_config(z, [(ref : ref <: instr) CONST_instr((at : addrtype <: numtype), `%`_num_(n)) TABLE.GROW_instr(x)]), `%;%`_config($with_tableinst(z, x, ti), [CONST_instr((at : addrtype <: numtype), `%`_num_(|$table(z, x).REFS_tableinst|))]))
    -- if (ti = $growtable($table(z, x), n, ref))

  ;; 8-reduction.watsup:826.1-827.86
  rule `table.grow-fail`{z : state, ref : ref, at : addrtype, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [(ref : ref <: instr) CONST_instr((at : addrtype <: numtype), `%`_num_(n)) TABLE.GROW_instr(x)]), `%;%`_config(z, [CONST_instr((at : addrtype <: numtype), `%`_num_($invsigned_($size((at : addrtype <: numtype)), - (1 : nat <:> int))))]))

  ;; 8-reduction.watsup:887.1-888.51
  rule elem.drop{z : state, x : idx}:
    `%~>%`(`%;%`_config(z, [ELEM.DROP_instr(x)]), `%;%`_config($with_elem(z, x, []), []))

  ;; 8-reduction.watsup:971.1-974.60
  rule `store-num-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), nt : numtype, c : num_(nt), x : idx, ao : memarg}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) CONST_instr(nt, c) STORE_instr(nt, ?(), x, ao)]), `%;%`_config(z, [TRAP_instr]))
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + ((($size(nt) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup:976.1-980.29
  rule `store-num-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), nt : numtype, c : num_(nt), x : idx, ao : memarg, `b*` : byte*}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) CONST_instr(nt, c) STORE_instr(nt, ?(), x, ao)]), `%;%`_config($with_mem(z, x, (i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0), ((($size(nt) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat), b*{b <- `b*`}), []))
    -- if (b*{b <- `b*`} = $nbytes_(nt, c))

  ;; 8-reduction.watsup:982.1-985.52
  rule `store-pack-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), Inn : Inn, c : num_((Inn : Inn <: numtype)), n : n, x : idx, ao : memarg}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) CONST_instr((Inn : Inn <: numtype), c) STORE_instr((Inn : Inn <: numtype), ?(`%`_storeop_(`%`_sz(n))), x, ao)]), `%;%`_config(z, [TRAP_instr]))
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + (((n : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup:987.1-991.52
  rule `store-pack-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), Inn : Inn, c : num_((Inn : Inn <: numtype)), n : n, x : idx, ao : memarg, `b*` : byte*}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) CONST_instr((Inn : Inn <: numtype), c) STORE_instr((Inn : Inn <: numtype), ?(`%`_storeop_(`%`_sz(n))), x, ao)]), `%;%`_config($with_mem(z, x, (i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0), (((n : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat), b*{b <- `b*`}), []))
    -- if (b*{b <- `b*`} = $ibytes_(n, $wrap__($size((Inn : Inn <: numtype)), n, c)))

  ;; 8-reduction.watsup:993.1-995.63
  rule `vstore-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), c : vec_(V128_Vnn), x : idx, ao : memarg}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VCONST_instr(V128_vectype, c) VSTORE_instr(V128_vectype, x, ao)]), `%;%`_config(z, [TRAP_instr]))
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + ((($vsize(V128_vectype) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat)) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup:997.1-999.31
  rule `vstore-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), c : vec_(V128_Vnn), x : idx, ao : memarg, `b*` : byte*}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VCONST_instr(V128_vectype, c) VSTORE_instr(V128_vectype, x, ao)]), `%;%`_config($with_mem(z, x, (i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0), ((($vsize(V128_vectype) : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat), b*{b <- `b*`}), []))
    -- if (b*{b <- `b*`} = $vbytes_(V128_vectype, c))

  ;; 8-reduction.watsup:1002.1-1004.50
  rule `vstore_lane-oob`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), c : vec_(V128_Vnn), N : N, x : idx, ao : memarg, j : laneidx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VCONST_instr(V128_vectype, c) VSTORE_LANE_instr(V128_vectype, `%`_sz(N), x, ao, j)]), `%;%`_config(z, [TRAP_instr]))
    -- if (((i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0) + N) > |$mem(z, x).BYTES_meminst|)

  ;; 8-reduction.watsup:1006.1-1010.49
  rule `vstore_lane-val`{z : state, at : addrtype, i : num_((at : addrtype <: numtype)), c : vec_(V128_Vnn), N : N, x : idx, ao : memarg, j : laneidx, `b*` : byte*, Jnn : Jnn, M : M}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), i) VCONST_instr(V128_vectype, c) VSTORE_LANE_instr(V128_vectype, `%`_sz(N), x, ao, j)]), `%;%`_config($with_mem(z, x, (i!`%`_num_.0 + ao.OFFSET_memarg!`%`_u32.0), (((N : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat), b*{b <- `b*`}), []))
    -- if (N = $lsize((Jnn : Jnn <: lanetype)))
    -- if ((M : nat <:> rat) = ((128 : nat <:> rat) / (N : nat <:> rat)))
    -- if (b*{b <- `b*`} = $ibytes_(N, `%`_iN($lanes_(`%X%`_shape((Jnn : Jnn <: lanetype), `%`_dim(M)), c)[j!`%`_laneidx.0]!`%`_lane_.0)))

  ;; 8-reduction.watsup:1019.1-1022.37
  rule `memory.grow-succeed`{z : state, at : addrtype, n : n, x : idx, mi : meminst}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), `%`_num_(n)) MEMORY.GROW_instr(x)]), `%;%`_config($with_meminst(z, x, mi), [CONST_instr((at : addrtype <: numtype), `%`_num_((((|$mem(z, x).BYTES_meminst| : nat <:> rat) / ((64 * $Ki) : nat <:> rat)) : rat <:> nat)))]))
    -- if (mi = $growmem($mem(z, x), n))

  ;; 8-reduction.watsup:1024.1-1025.83
  rule `memory.grow-fail`{z : state, at : addrtype, n : n, x : idx}:
    `%~>%`(`%;%`_config(z, [CONST_instr((at : addrtype <: numtype), `%`_num_(n)) MEMORY.GROW_instr(x)]), `%;%`_config(z, [CONST_instr((at : addrtype <: numtype), `%`_num_($invsigned_($size((at : addrtype <: numtype)), - (1 : nat <:> int))))]))

  ;; 8-reduction.watsup:1085.1-1086.51
  rule data.drop{z : state, x : idx}:
    `%~>%`(`%;%`_config(z, [DATA.DROP_instr(x)]), `%;%`_config($with_data(z, x, []), []))
}

;; 8-reduction.watsup
rec {

;; 8-reduction.watsup:8.1-8.92
relation Steps: `%~>*%`(config, config)
  ;; 8-reduction.watsup:21.1-22.26
  rule refl{z : state, `instr*` : instr*}:
    `%~>*%`(`%;%`_config(z, instr*{instr <- `instr*`}), `%;%`_config(z, instr*{instr <- `instr*`}))

  ;; 8-reduction.watsup:24.1-27.44
  rule trans{z : state, `instr*` : instr*, z'' : state, `instr''*` : instr*, z' : state, `instr'*` : instr*}:
    `%~>*%`(`%;%`_config(z, instr*{instr <- `instr*`}), `%;%`_config(z'', instr''*{instr'' <- `instr''*`}))
    -- Step: `%~>%`(`%;%`_config(z, instr*{instr <- `instr*`}), `%;%`_config(z', instr'*{instr' <- `instr'*`}))
    -- Steps: `%~>*%`(`%;%`_config(z', instr'*{instr' <- `instr'*`}), `%;%`_config(z'', instr''*{instr'' <- `instr''*`}))
}

;; 8-reduction.watsup
relation Eval_expr: `%;%~>*%;%`(state, expr, state, val*)
  ;; 8-reduction.watsup
  rule _{z : state, `instr*` : instr*, z' : state, `val*` : val*}:
    `%;%~>*%;%`(z, instr*{instr <- `instr*`}, z', val*{val <- `val*`})
    -- Steps: `%~>*%`(`%;%`_config(z, instr*{instr <- `instr*`}), `%;%`_config(z', (val : val <: instr)*{val <- `val*`}))

;; 9-module.watsup
rec {

;; 9-module.watsup:7.1-7.63
def $alloctypes(type*) : deftype*
  ;; 9-module.watsup:8.1-8.27
  def $alloctypes([]) = []
  ;; 9-module.watsup:9.1-13.24
  def $alloctypes{`type'*` : type*, type : type, `deftype'*` : deftype*, `deftype*` : deftype*, rectype : rectype, x : idx}(type'*{type' <- `type'*`} ++ [type]) = deftype'*{deftype' <- `deftype'*`} ++ deftype*{deftype <- `deftype*`}
    -- if (deftype'*{deftype' <- `deftype'*`} = $alloctypes(type'*{type' <- `type'*`}))
    -- if (type = TYPE_type(rectype))
    -- if (deftype*{deftype <- `deftype*`} = $subst_all_deftypes($rolldt(x, rectype), (deftype' : deftype <: heaptype)*{deftype' <- `deftype'*`}))
    -- if (x!`%`_idx.0 = |deftype'*{deftype' <- `deftype'*`}|)
}

;; 9-module.watsup
def $allocfunc(store : store, deftype : deftype, funccode : funccode, moduleinst : moduleinst) : (store, funcaddr)
  ;; 9-module.watsup
  def $allocfunc{s : store, deftype : deftype, funccode : funccode, moduleinst : moduleinst, funcinst : funcinst}(s, deftype, funccode, moduleinst) = (s +++ {FUNCS [funcinst], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], STRUCTS [], ARRAYS [], EXNS []}, |s.FUNCS_store|)
    -- if (funcinst = {TYPE deftype, MODULE moduleinst, CODE funccode})

;; 9-module.watsup
rec {

;; 9-module.watsup:20.1-20.113
def $allocfuncs(store : store, deftype*, funccode*, moduleinst*) : (store, funcaddr*)
  ;; 9-module.watsup:21.1-21.45
  def $allocfuncs{s : store}(s, [], [], []) = (s, [])
  ;; 9-module.watsup:22.1-24.71
  def $allocfuncs{s : store, dt : deftype, `dt'*` : deftype*, funccode : funccode, `funccode'*` : funccode*, moduleinst : moduleinst, `moduleinst'*` : moduleinst*, s_2 : store, fa : funcaddr, `fa'*` : funcaddr*, s_1 : store}(s, [dt] ++ dt'*{dt' <- `dt'*`}, [funccode] ++ funccode'*{funccode' <- `funccode'*`}, [moduleinst] ++ moduleinst'*{moduleinst' <- `moduleinst'*`}) = (s_2, [fa] ++ fa'*{fa' <- `fa'*`})
    -- if ((s_1, fa) = $allocfunc(s, dt, funccode, moduleinst))
    -- if ((s_2, fa'*{fa' <- `fa'*`}) = $allocfuncs(s_1, dt'*{dt' <- `dt'*`}, funccode'*{funccode' <- `funccode'*`}, moduleinst'*{moduleinst' <- `moduleinst'*`}))
}

;; 9-module.watsup
def $allocglobal(store : store, globaltype : globaltype, val : val) : (store, globaladdr)
  ;; 9-module.watsup
  def $allocglobal{s : store, globaltype : globaltype, val : val, globalinst : globalinst}(s, globaltype, val) = (s +++ {FUNCS [], GLOBALS [globalinst], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], STRUCTS [], ARRAYS [], EXNS []}, |s.GLOBALS_store|)
    -- if (globalinst = {TYPE globaltype, VALUE val})

;; 9-module.watsup
rec {

;; 9-module.watsup:31.1-31.102
def $allocglobals(store : store, globaltype*, val*) : (store, globaladdr*)
  ;; 9-module.watsup:32.1-32.42
  def $allocglobals{s : store}(s, [], []) = (s, [])
  ;; 9-module.watsup:33.1-35.62
  def $allocglobals{s : store, globaltype : globaltype, `globaltype'*` : globaltype*, val : val, `val'*` : val*, s_2 : store, ga : globaladdr, `ga'*` : globaladdr*, s_1 : store}(s, [globaltype] ++ globaltype'*{globaltype' <- `globaltype'*`}, [val] ++ val'*{val' <- `val'*`}) = (s_2, [ga] ++ ga'*{ga' <- `ga'*`})
    -- if ((s_1, ga) = $allocglobal(s, globaltype, val))
    -- if ((s_2, ga'*{ga' <- `ga'*`}) = $allocglobals(s_1, globaltype'*{globaltype' <- `globaltype'*`}, val'*{val' <- `val'*`}))
}

;; 9-module.watsup
def $alloctable(store : store, tabletype : tabletype, ref : ref) : (store, tableaddr)
  ;; 9-module.watsup
  def $alloctable{s : store, at : addrtype, i : u64, j : u64, rt : reftype, ref : ref, tableinst : tableinst}(s, `%%%`_tabletype(at, `[%..%]`_limits(i, j), rt), ref) = (s +++ {FUNCS [], GLOBALS [], TABLES [tableinst], MEMS [], TAGS [], ELEMS [], DATAS [], STRUCTS [], ARRAYS [], EXNS []}, |s.TABLES_store|)
    -- if (tableinst = {TYPE `%%%`_tabletype(at, `[%..%]`_limits(i, j), rt), REFS ref^i!`%`_u64.0{}})

;; 9-module.watsup
rec {

;; 9-module.watsup:42.1-42.98
def $alloctables(store : store, tabletype*, ref*) : (store, tableaddr*)
  ;; 9-module.watsup:43.1-43.41
  def $alloctables{s : store}(s, [], []) = (s, [])
  ;; 9-module.watsup:44.1-46.60
  def $alloctables{s : store, tabletype : tabletype, `tabletype'*` : tabletype*, ref : ref, `ref'*` : ref*, s_2 : store, ta : tableaddr, `ta'*` : tableaddr*, s_1 : store}(s, [tabletype] ++ tabletype'*{tabletype' <- `tabletype'*`}, [ref] ++ ref'*{ref' <- `ref'*`}) = (s_2, [ta] ++ ta'*{ta' <- `ta'*`})
    -- if ((s_1, ta) = $alloctable(s, tabletype, ref))
    -- if ((s_2, ta'*{ta' <- `ta'*`}) = $alloctables(s_1, tabletype'*{tabletype' <- `tabletype'*`}, ref'*{ref' <- `ref'*`}))
}

;; 9-module.watsup
def $allocmem(store : store, memtype : memtype) : (store, memaddr)
  ;; 9-module.watsup
  def $allocmem{s : store, at : addrtype, i : u64, j : u64, meminst : meminst}(s, `%%PAGE`_memtype(at, `[%..%]`_limits(i, j))) = (s +++ {FUNCS [], GLOBALS [], TABLES [], MEMS [meminst], TAGS [], ELEMS [], DATAS [], STRUCTS [], ARRAYS [], EXNS []}, |s.MEMS_store|)
    -- if (meminst = {TYPE `%%PAGE`_memtype(at, `[%..%]`_limits(i, j)), BYTES `%`_byte(0)^(i!`%`_u64.0 * (64 * $Ki)){}})

;; 9-module.watsup
rec {

;; 9-module.watsup:53.1-53.82
def $allocmems(store : store, memtype*) : (store, memaddr*)
  ;; 9-module.watsup:54.1-54.34
  def $allocmems{s : store}(s, []) = (s, [])
  ;; 9-module.watsup:55.1-57.49
  def $allocmems{s : store, memtype : memtype, `memtype'*` : memtype*, s_2 : store, ma : memaddr, `ma'*` : memaddr*, s_1 : store}(s, [memtype] ++ memtype'*{memtype' <- `memtype'*`}) = (s_2, [ma] ++ ma'*{ma' <- `ma'*`})
    -- if ((s_1, ma) = $allocmem(s, memtype))
    -- if ((s_2, ma'*{ma' <- `ma'*`}) = $allocmems(s_1, memtype'*{memtype' <- `memtype'*`}))
}

;; 9-module.watsup
def $alloctag(store : store, tagtype : tagtype) : (store, tagaddr)
  ;; 9-module.watsup
  def $alloctag{s : store, tagtype : tagtype, taginst : taginst}(s, tagtype) = (s +++ {FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [taginst], ELEMS [], DATAS [], STRUCTS [], ARRAYS [], EXNS []}, |s.TAGS_store|)
    -- if (taginst = {TYPE tagtype})

;; 9-module.watsup
rec {

;; 9-module.watsup:64.1-64.82
def $alloctags(store : store, tagtype*) : (store, tagaddr*)
  ;; 9-module.watsup:65.1-65.34
  def $alloctags{s : store}(s, []) = (s, [])
  ;; 9-module.watsup:66.1-68.44
  def $alloctags{s : store, jt : tagtype, `jt'*` : tagtype*, s_2 : store, ja : tagaddr, `ja'*` : tagaddr*, s_1 : store}(s, [jt] ++ jt'*{jt' <- `jt'*`}) = (s_2, [ja] ++ ja'*{ja' <- `ja'*`})
    -- if ((s_1, ja) = $alloctag(s, jt))
    -- if ((s_2, ja'*{ja' <- `ja'*`}) = $alloctags(s_1, jt'*{jt' <- `jt'*`}))
}

;; 9-module.watsup
def $allocelem(store : store, elemtype : elemtype, ref*) : (store, elemaddr)
  ;; 9-module.watsup
  def $allocelem{s : store, elemtype : elemtype, `ref*` : ref*, eleminst : eleminst}(s, elemtype, ref*{ref <- `ref*`}) = (s +++ {FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [eleminst], DATAS [], STRUCTS [], ARRAYS [], EXNS []}, |s.ELEMS_store|)
    -- if (eleminst = {TYPE elemtype, REFS ref*{ref <- `ref*`}})

;; 9-module.watsup
rec {

;; 9-module.watsup:75.1-75.97
def $allocelems(store : store, elemtype*, ref**) : (store, elemaddr*)
  ;; 9-module.watsup:76.1-76.40
  def $allocelems{s : store}(s, [], []) = (s, [])
  ;; 9-module.watsup:77.1-79.55
  def $allocelems{s : store, rt : reftype, `rt'*` : reftype*, `ref*` : ref*, `ref'**` : ref**, s_2 : store, ea : elemaddr, `ea'*` : elemaddr*, s_1 : store}(s, [rt] ++ rt'*{rt' <- `rt'*`}, [ref*{ref <- `ref*`}] ++ ref'*{ref' <- `ref'*`}*{`ref'*` <- `ref'**`}) = (s_2, [ea] ++ ea'*{ea' <- `ea'*`})
    -- if ((s_1, ea) = $allocelem(s, rt, ref*{ref <- `ref*`}))
    -- if ((s_2, ea'*{ea' <- `ea'*`}) = $allocelems(s_1, rt'*{rt' <- `rt'*`}, ref'*{ref' <- `ref'*`}*{`ref'*` <- `ref'**`}))
}

;; 9-module.watsup
def $allocdata(store : store, datatype : datatype, byte*) : (store, dataaddr)
  ;; 9-module.watsup
  def $allocdata{s : store, `byte*` : byte*, datainst : datainst}(s, OK_datatype, byte*{byte <- `byte*`}) = (s +++ {FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [datainst], STRUCTS [], ARRAYS [], EXNS []}, |s.DATAS_store|)
    -- if (datainst = {BYTES byte*{byte <- `byte*`}})

;; 9-module.watsup
rec {

;; 9-module.watsup:86.1-86.98
def $allocdatas(store : store, datatype*, byte**) : (store, dataaddr*)
  ;; 9-module.watsup:87.1-87.40
  def $allocdatas{s : store}(s, [], []) = (s, [])
  ;; 9-module.watsup:88.1-90.53
  def $allocdatas{s : store, ok : datatype, `ok'*` : datatype*, `b*` : byte*, `b'**` : byte**, s_2 : store, da : dataaddr, `da'*` : dataaddr*, s_1 : store}(s, [ok] ++ ok'*{ok' <- `ok'*`}, [b*{b <- `b*`}] ++ b'*{b' <- `b'*`}*{`b'*` <- `b'**`}) = (s_2, [da] ++ da'*{da' <- `da'*`})
    -- if ((s_1, da) = $allocdata(s, ok, b*{b <- `b*`}))
    -- if ((s_2, da'*{da' <- `da'*`}) = $allocdatas(s_1, ok'*{ok' <- `ok'*`}, b'*{b' <- `b'*`}*{`b'*` <- `b'**`}))
}

;; 9-module.watsup
def $allocexport(moduleinst : moduleinst, export : export) : exportinst
  ;; 9-module.watsup
  def $allocexport{moduleinst : moduleinst, name : name, x : idx}(moduleinst, EXPORT_export(name, FUNC_externidx(x))) = {NAME name, ADDR FUNC_externaddr(moduleinst.FUNCS_moduleinst[x!`%`_idx.0])}
  ;; 9-module.watsup
  def $allocexport{moduleinst : moduleinst, name : name, x : idx}(moduleinst, EXPORT_export(name, GLOBAL_externidx(x))) = {NAME name, ADDR GLOBAL_externaddr(moduleinst.GLOBALS_moduleinst[x!`%`_idx.0])}
  ;; 9-module.watsup
  def $allocexport{moduleinst : moduleinst, name : name, x : idx}(moduleinst, EXPORT_export(name, TABLE_externidx(x))) = {NAME name, ADDR TABLE_externaddr(moduleinst.TABLES_moduleinst[x!`%`_idx.0])}
  ;; 9-module.watsup
  def $allocexport{moduleinst : moduleinst, name : name, x : idx}(moduleinst, EXPORT_export(name, MEM_externidx(x))) = {NAME name, ADDR MEM_externaddr(moduleinst.MEMS_moduleinst[x!`%`_idx.0])}
  ;; 9-module.watsup
  def $allocexport{moduleinst : moduleinst, name : name, x : idx}(moduleinst, EXPORT_export(name, TAG_externidx(x))) = {NAME name, ADDR TAG_externaddr(moduleinst.TAGS_moduleinst[x!`%`_idx.0])}

;; 9-module.watsup
def $allocexports(moduleinst : moduleinst, export*) : exportinst*
  ;; 9-module.watsup
  def $allocexports{moduleinst : moduleinst, `export*` : export*}(moduleinst, export*{export <- `export*`}) = $allocexport(moduleinst, export)*{export <- `export*`}

;; 9-module.watsup
def $allocmodule(store : store, module : module, externaddr*, val*, ref*, ref**) : (store, moduleinst)
  ;; 9-module.watsup
  def $allocmodule{s : store, module : module, `externaddr*` : externaddr*, `val_G*` : val*, `ref_T*` : ref*, `ref_E**` : ref**, s_7 : store, moduleinst : moduleinst, `type*` : type*, `import*` : import*, `func*` : func*, `global*` : global*, `table*` : table*, `mem*` : mem*, `tag*` : tag*, `elem*` : elem*, `data*` : data*, `start?` : start?, `export*` : export*, `x*` : idx*, `local**` : local**, `expr_F*` : expr*, `globaltype*` : globaltype*, `expr_G*` : expr*, `tabletype*` : tabletype*, `expr_T*` : expr*, `memtype*` : memtype*, `y*` : idx*, `elemtype*` : elemtype*, `expr_E**` : expr**, `elemmode*` : elemmode*, `byte**` : byte**, `datamode*` : datamode*, `fa_I*` : funcaddr*, `ga_I*` : globaladdr*, `ta_I*` : tableaddr*, `ma_I*` : memaddr*, `aa_I*` : tagaddr*, `fa*` : nat*, `i_F*` : nat*, `ga*` : nat*, `i_G*` : nat*, `ta*` : nat*, `i_T*` : nat*, `aa*` : nat*, `i_A*` : nat*, `ma*` : nat*, `i_M*` : nat*, `ea*` : nat*, `i_E*` : nat*, `da*` : nat*, `i_D*` : nat*, `dt*` : deftype*, s_1 : store, s_2 : store, s_3 : store, s_4 : store, s_5 : store, s_6 : store, `xi*` : exportinst*}(s, module, externaddr*{externaddr <- `externaddr*`}, val_G*{val_G <- `val_G*`}, ref_T*{ref_T <- `ref_T*`}, ref_E*{ref_E <- `ref_E*`}*{`ref_E*` <- `ref_E**`}) = (s_7, moduleinst)
    -- if (module = MODULE_module(type*{type <- `type*`}, import*{import <- `import*`}, func*{func <- `func*`}, global*{global <- `global*`}, table*{table <- `table*`}, mem*{mem <- `mem*`}, tag*{tag <- `tag*`}, elem*{elem <- `elem*`}, data*{data <- `data*`}, start?{start <- `start?`}, export*{export <- `export*`}))
    -- if (func*{func <- `func*`} = FUNC_func(x, local*{local <- `local*`}, expr_F)*{expr_F <- `expr_F*`, `local*` <- `local**`, x <- `x*`})
    -- if (global*{global <- `global*`} = GLOBAL_global(globaltype, expr_G)*{expr_G <- `expr_G*`, globaltype <- `globaltype*`})
    -- if (table*{table <- `table*`} = TABLE_table(tabletype, expr_T)*{expr_T <- `expr_T*`, tabletype <- `tabletype*`})
    -- if (mem*{mem <- `mem*`} = MEMORY_mem(memtype)*{memtype <- `memtype*`})
    -- if (tag*{tag <- `tag*`} = TAG_tag(y)*{y <- `y*`})
    -- if (elem*{elem <- `elem*`} = ELEM_elem(elemtype, expr_E*{expr_E <- `expr_E*`}, elemmode)*{elemmode <- `elemmode*`, elemtype <- `elemtype*`, `expr_E*` <- `expr_E**`})
    -- if (data*{data <- `data*`} = DATA_data(byte*{byte <- `byte*`}, datamode)*{`byte*` <- `byte**`, datamode <- `datamode*`})
    -- if (fa_I*{fa_I <- `fa_I*`} = $funcsxa(externaddr*{externaddr <- `externaddr*`}))
    -- if (ga_I*{ga_I <- `ga_I*`} = $globalsxa(externaddr*{externaddr <- `externaddr*`}))
    -- if (ta_I*{ta_I <- `ta_I*`} = $tablesxa(externaddr*{externaddr <- `externaddr*`}))
    -- if (ma_I*{ma_I <- `ma_I*`} = $memsxa(externaddr*{externaddr <- `externaddr*`}))
    -- if (aa_I*{aa_I <- `aa_I*`} = $tagsxa(externaddr*{externaddr <- `externaddr*`}))
    -- if (fa*{fa <- `fa*`} = (|s.FUNCS_store| + i_F)^(i_F<|func*{func <- `func*`}|){i_F <- `i_F*`})
    -- if (ga*{ga <- `ga*`} = (|s.GLOBALS_store| + i_G)^(i_G<|global*{global <- `global*`}|){i_G <- `i_G*`})
    -- if (ta*{ta <- `ta*`} = (|s.TABLES_store| + i_T)^(i_T<|table*{table <- `table*`}|){i_T <- `i_T*`})
    -- if (aa*{aa <- `aa*`} = (|s.TAGS_store| + i_A)^(i_A<|tag*{tag <- `tag*`}|){i_A <- `i_A*`})
    -- if (ma*{ma <- `ma*`} = (|s.MEMS_store| + i_M)^(i_M<|mem*{mem <- `mem*`}|){i_M <- `i_M*`})
    -- if (ea*{ea <- `ea*`} = (|s.ELEMS_store| + i_E)^(i_E<|elem*{elem <- `elem*`}|){i_E <- `i_E*`})
    -- if (da*{da <- `da*`} = (|s.DATAS_store| + i_D)^(i_D<|data*{data <- `data*`}|){i_D <- `i_D*`})
    -- if (dt*{dt <- `dt*`} = $alloctypes(type*{type <- `type*`}))
    -- if ((s_1, fa*{fa <- `fa*`}) = $allocfuncs(s, dt*{dt <- `dt*`}[x!`%`_idx.0]*{x <- `x*`}, FUNC_funccode(x, local*{local <- `local*`}, expr_F)*{expr_F <- `expr_F*`, `local*` <- `local**`, x <- `x*`}, moduleinst^|func*{func <- `func*`}|{}))
    -- if ((s_2, ga*{ga <- `ga*`}) = $allocglobals(s_1, $subst_all_globaltype(globaltype, (dt : deftype <: heaptype)*{dt <- `dt*`})*{globaltype <- `globaltype*`}, val_G*{val_G <- `val_G*`}))
    -- if ((s_3, ta*{ta <- `ta*`}) = $alloctables(s_2, $subst_all_tabletype(tabletype, (dt : deftype <: heaptype)*{dt <- `dt*`})*{tabletype <- `tabletype*`}, ref_T*{ref_T <- `ref_T*`}))
    -- if ((s_4, ma*{ma <- `ma*`}) = $allocmems(s_3, $subst_all_memtype(memtype, (dt : deftype <: heaptype)*{dt <- `dt*`})*{memtype <- `memtype*`}))
    -- if ((s_5, aa*{aa <- `aa*`}) = $alloctags(s_4, dt*{dt <- `dt*`}[y!`%`_idx.0]*{y <- `y*`}))
    -- if ((s_6, ea*{ea <- `ea*`}) = $allocelems(s_5, $subst_all_reftype(elemtype, (dt : deftype <: heaptype)*{dt <- `dt*`})*{elemtype <- `elemtype*`}, ref_E*{ref_E <- `ref_E*`}*{`ref_E*` <- `ref_E**`}))
    -- if ((s_7, da*{da <- `da*`}) = $allocdatas(s_6, OK_datatype^|data*{data <- `data*`}|{}, byte*{byte <- `byte*`}*{`byte*` <- `byte**`}))
    -- if (xi*{xi <- `xi*`} = $allocexports({TYPES [], FUNCS fa_I*{fa_I <- `fa_I*`} ++ fa*{fa <- `fa*`}, GLOBALS ga_I*{ga_I <- `ga_I*`} ++ ga*{ga <- `ga*`}, TABLES ta_I*{ta_I <- `ta_I*`} ++ ta*{ta <- `ta*`}, MEMS ma_I*{ma_I <- `ma_I*`} ++ ma*{ma <- `ma*`}, TAGS aa_I*{aa_I <- `aa_I*`} ++ aa*{aa <- `aa*`}, ELEMS [], DATAS [], EXPORTS []}, export*{export <- `export*`}))
    -- if (moduleinst = {TYPES dt*{dt <- `dt*`}, FUNCS fa_I*{fa_I <- `fa_I*`} ++ fa*{fa <- `fa*`}, GLOBALS ga_I*{ga_I <- `ga_I*`} ++ ga*{ga <- `ga*`}, TABLES ta_I*{ta_I <- `ta_I*`} ++ ta*{ta <- `ta*`}, MEMS ma_I*{ma_I <- `ma_I*`} ++ ma*{ma <- `ma*`}, TAGS aa_I*{aa_I <- `aa_I*`} ++ aa*{aa <- `aa*`}, ELEMS ea*{ea <- `ea*`}, DATAS da*{da <- `da*`}, EXPORTS xi*{xi <- `xi*`}})

;; 9-module.watsup
def $runelem_(elemidx : elemidx, elem : elem) : instr*
  ;; 9-module.watsup
  def $runelem_{x : idx, rt : reftype, `e*` : expr*, n : n}(x, ELEM_elem(rt, e^n{e <- `e*`}, PASSIVE_elemmode)) = []
  ;; 9-module.watsup
  def $runelem_{x : idx, rt : reftype, `e*` : expr*, n : n}(x, ELEM_elem(rt, e^n{e <- `e*`}, DECLARE_elemmode)) = [ELEM.DROP_instr(x)]
  ;; 9-module.watsup
  def $runelem_{x : idx, rt : reftype, `e*` : expr*, n : n, y : idx, `instr*` : instr*}(x, ELEM_elem(rt, e^n{e <- `e*`}, ACTIVE_elemmode(y, instr*{instr <- `instr*`}))) = instr*{instr <- `instr*`} ++ [CONST_instr(I32_numtype, `%`_num_(0)) CONST_instr(I32_numtype, `%`_num_(n)) TABLE.INIT_instr(y, x) ELEM.DROP_instr(x)]

;; 9-module.watsup
def $rundata_(dataidx : dataidx, data : data) : instr*
  ;; 9-module.watsup
  def $rundata_{x : idx, `b*` : byte*, n : n}(x, DATA_data(b^n{b <- `b*`}, PASSIVE_datamode)) = []
  ;; 9-module.watsup
  def $rundata_{x : idx, `b*` : byte*, n : n, y : idx, `instr*` : instr*}(x, DATA_data(b^n{b <- `b*`}, ACTIVE_datamode(y, instr*{instr <- `instr*`}))) = instr*{instr <- `instr*`} ++ [CONST_instr(I32_numtype, `%`_num_(0)) CONST_instr(I32_numtype, `%`_num_(n)) MEMORY.INIT_instr(y, x) DATA.DROP_instr(x)]

;; 9-module.watsup
rec {

;; 9-module.watsup:170.1-170.94
def $evalglobals(state : state, globaltype*, expr*) : (state, val*)
  ;; 9-module.watsup:171.1-171.41
  def $evalglobals{z : state}(z, [], []) = (z, [])
  ;; 9-module.watsup:172.1-177.81
  def $evalglobals{z : state, gt : globaltype, `gt'*` : globaltype*, expr : expr, `expr'*` : expr*, z' : state, val : val, `val'*` : val*, s : store, f : frame, s' : store, a : addr}(z, [gt] ++ gt'*{gt' <- `gt'*`}, [expr] ++ expr'*{expr' <- `expr'*`}) = (z', [val] ++ val'*{val' <- `val'*`})
    -- Eval_expr: `%;%~>*%;%`(z, expr, z, [val])
    -- if (z = `%;%`_state(s, f))
    -- if ((s', a) = $allocglobal(s, gt, val))
    -- if ((z', val'*{val' <- `val'*`}) = $evalglobals(`%;%`_state(s', f[MODULE_frame.GLOBALS_moduleinst =++ [a]]), gt'*{gt' <- `gt'*`}, expr'*{expr' <- `expr'*`}))
}

;; 9-module.watsup
def $instantiate(store : store, module : module, externaddr*) : config
  ;; 9-module.watsup
  def $instantiate{s : store, module : module, `externaddr*` : externaddr*, s' : store, f : frame, `instr_E*` : instr*, `instr_D*` : instr*, `instr_S?` : instr?, `xt_I*` : externtype*, `xt_E*` : externtype*, `type*` : type*, `import*` : import*, `func*` : func*, `global*` : global*, `table*` : table*, `mem*` : mem*, `tag*` : tag*, `elem*` : elem*, `data*` : data*, `start?` : start?, `export*` : export*, `globaltype*` : globaltype*, `expr_G*` : expr*, `tabletype*` : tabletype*, `expr_T*` : expr*, `reftype*` : reftype*, `expr_E**` : expr**, `elemmode*` : elemmode*, `byte**` : byte**, `datamode*` : datamode*, `x?` : idx?, moduleinst_0 : moduleinst, `i_F*` : nat*, z : state, z' : state, `val_G*` : val*, `ref_T*` : ref*, `ref_E**` : ref**, moduleinst : moduleinst, `i_E*` : nat*, `i_D*` : nat*}(s, module, externaddr*{externaddr <- `externaddr*`}) = `%;%`_config(`%;%`_state(s', f), instr_E*{instr_E <- `instr_E*`} ++ instr_D*{instr_D <- `instr_D*`} ++ lift(instr_S?{instr_S <- `instr_S?`}))
    -- Module_ok: `|-%:%`(module, `%->%`_moduletype(xt_I*{xt_I <- `xt_I*`}, xt_E*{xt_E <- `xt_E*`}))
    -- (Externaddr_type: `%|-%:%`(s, externaddr, xt_I))*{externaddr <- `externaddr*`, xt_I <- `xt_I*`}
    -- if (module = MODULE_module(type*{type <- `type*`}, import*{import <- `import*`}, func*{func <- `func*`}, global*{global <- `global*`}, table*{table <- `table*`}, mem*{mem <- `mem*`}, tag*{tag <- `tag*`}, elem*{elem <- `elem*`}, data*{data <- `data*`}, start?{start <- `start?`}, export*{export <- `export*`}))
    -- if (global*{global <- `global*`} = GLOBAL_global(globaltype, expr_G)*{expr_G <- `expr_G*`, globaltype <- `globaltype*`})
    -- if (table*{table <- `table*`} = TABLE_table(tabletype, expr_T)*{expr_T <- `expr_T*`, tabletype <- `tabletype*`})
    -- if (elem*{elem <- `elem*`} = ELEM_elem(reftype, expr_E*{expr_E <- `expr_E*`}, elemmode)*{elemmode <- `elemmode*`, `expr_E*` <- `expr_E**`, reftype <- `reftype*`})
    -- if (data*{data <- `data*`} = DATA_data(byte*{byte <- `byte*`}, datamode)*{`byte*` <- `byte**`, datamode <- `datamode*`})
    -- if (start?{start <- `start?`} = START_start(x)?{x <- `x?`})
    -- if (moduleinst_0 = {TYPES $alloctypes(type*{type <- `type*`}), FUNCS $funcsxa(externaddr*{externaddr <- `externaddr*`}) ++ (|s.FUNCS_store| + i_F)^(i_F<|func*{func <- `func*`}|){i_F <- `i_F*`}, GLOBALS $globalsxa(externaddr*{externaddr <- `externaddr*`}), TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], EXPORTS []})
    -- if (z = `%;%`_state(s, {LOCALS [], MODULE moduleinst_0}))
    -- if ((z', val_G*{val_G <- `val_G*`}) = $evalglobals(z, globaltype*{globaltype <- `globaltype*`}, expr_G*{expr_G <- `expr_G*`}))
    -- (Eval_expr: `%;%~>*%;%`(z', expr_T, z', [(ref_T : ref <: val)]))*{expr_T <- `expr_T*`, ref_T <- `ref_T*`}
    -- (Eval_expr: `%;%~>*%;%`(z', expr_E, z', [(ref_E : ref <: val)]))*{expr_E <- `expr_E*`, ref_E <- `ref_E*`}*{`expr_E*` <- `expr_E**`, `ref_E*` <- `ref_E**`}
    -- if ((s', moduleinst) = $allocmodule(s, module, externaddr*{externaddr <- `externaddr*`}, val_G*{val_G <- `val_G*`}, ref_T*{ref_T <- `ref_T*`}, ref_E*{ref_E <- `ref_E*`}*{`ref_E*` <- `ref_E**`}))
    -- if (f = {LOCALS [], MODULE moduleinst})
    -- if (instr_E*{instr_E <- `instr_E*`} = $concat_(syntax instr, $runelem_(`%`_elemidx(i_E), elem*{elem <- `elem*`}[i_E])^(i_E<|elem*{elem <- `elem*`}|){i_E <- `i_E*`}))
    -- if (instr_D*{instr_D <- `instr_D*`} = $concat_(syntax instr, $rundata_(`%`_dataidx(i_D), data*{data <- `data*`}[i_D])^(i_D<|data*{data <- `data*`}|){i_D <- `i_D*`}))
    -- if (instr_S?{instr_S <- `instr_S?`} = CALL_instr(x)?{x <- `x?`})

;; 9-module.watsup
def $invoke(store : store, funcaddr : funcaddr, val*) : config
  ;; 9-module.watsup
  def $invoke{s : store, funcaddr : funcaddr, `val*` : val*, f : frame, `t_1*` : valtype*, `t_2*` : valtype*}(s, funcaddr, val*{val <- `val*`}) = `%;%`_config(`%;%`_state(s, f), (val : val <: instr)*{val <- `val*`} ++ [REF.FUNC_ADDR_instr(funcaddr) CALL_REF_instr((s.FUNCS_store[funcaddr].TYPE_funcinst : deftype <: typeuse))])
    -- Expand: `%~~%`(s.FUNCS_store[funcaddr].TYPE_funcinst, FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`}))))
    -- (Val_type: `%|-%:%`(s, val, t_1))*{t_1 <- `t_1*`, val <- `val*`}
    -- if (f = {LOCALS [], MODULE {TYPES [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], EXPORTS []}})

;; A-binary.watsup
grammar Bbyte : byte
  ;; A-binary.watsup
  prod{b : byte} b!`%`_byte.0:0x00 | ... | b!`%`_byte.0:0xFF => b

;; A-binary.watsup
rec {

;; A-binary.watsup:20.1-22.82
grammar BuN(N : N) : uN(N)
  ;; A-binary.watsup:21.5-21.83
  prod{n : n} `%`_byte(n):Bbyte => `%`_uN(n)
    -- if ((n < (2 ^ 7)) /\ (n < (2 ^ N)))
  ;; A-binary.watsup:22.5-22.82
  prod{n : n, m : m} {`%`_byte(n):Bbyte `%`_uN(m):BuN((((N : nat <:> int) - (7 : nat <:> int)) : int <:> nat))} => `%`_uN((((2 ^ 7) * m) + (((n : nat <:> int) - ((2 ^ 7) : nat <:> int)) : int <:> nat)))
    -- if ((n >= (2 ^ 7)) /\ (N > 7))
}

;; A-binary.watsup
grammar Bu32 : u32
  ;; A-binary.watsup
  prod{n : n} `%`_uN(n):BuN(32) => `%`_u32(n)

;; A-binary.watsup
grammar Blist(syntax el, grammar BX : el) : el*
  ;; A-binary.watsup
  prod{n : n, `el*` : el*} {`%`_u32(n):Bu32 el:BX^n{el <- `el*`}} => el^n{el <- `el*`}

;; A-binary.watsup
grammar BsN(N : N) : sN(N)
  ;; A-binary.watsup
  prod{n : n} `%`_byte(n):Bbyte => `%`_sN((n : nat <:> int))
    -- if ((n < (2 ^ 6)) /\ (n < (2 ^ (((N : nat <:> int) - (1 : nat <:> int)) : int <:> nat))))
  ;; A-binary.watsup
  prod{n : n} `%`_byte(n):Bbyte => `%`_sN(((n : nat <:> int) - ((2 ^ 7) : nat <:> int)))
    -- if ((((2 ^ 6) <= n) /\ (n < (2 ^ 7))) /\ ((n : nat <:> int) >= (((2 ^ 7) : nat <:> int) - ((2 ^ (((N : nat <:> int) - (1 : nat <:> int)) : int <:> nat)) : nat <:> int))))
  ;; A-binary.watsup
  prod{n : n, i : uN((((N : nat <:> int) - (7 : nat <:> int)) : int <:> nat))} {`%`_byte(n):Bbyte i:BuN((((N : nat <:> int) - (7 : nat <:> int)) : int <:> nat))} => `%`_sN(((((2 ^ 7) * i!`%`_uN.0) + (((n : nat <:> int) - ((2 ^ 7) : nat <:> int)) : int <:> nat)) : nat <:> int))
    -- if ((n >= (2 ^ 7)) /\ (N > 7))

;; A-binary.watsup
grammar BiN(N : N) : iN(N)
  ;; A-binary.watsup
  prod{i : sN(N)} i:BsN(N) => `%`_iN($invsigned_(N, i!`%`_sN.0))

;; A-binary.watsup
grammar BfN(N : N) : fN(N)
  ;; A-binary.watsup
  prod{`b*` : byte*} b*{b <- `b*`}:Bbyte^(((N : nat <:> rat) / (8 : nat <:> rat)) : rat <:> nat){} => $invfbytes_(N, b*{b <- `b*`})

;; A-binary.watsup
grammar Bu64 : u64
  ;; A-binary.watsup
  prod{n : n} `%`_uN(n):BuN(64) => `%`_u64(n)

;; A-binary.watsup
grammar Bs33 : s33
  ;; A-binary.watsup
  prod{i : sN(33)} i:BsN(33) => i

;; A-binary.watsup
grammar Bf32 : f32
  ;; A-binary.watsup
  prod{p : fN(32)} p:BfN(32) => p

;; A-binary.watsup
grammar Bf64 : f64
  ;; A-binary.watsup
  prod{p : fN(64)} p:BfN(64) => p

;; A-binary.watsup
grammar Bname : name
  ;; A-binary.watsup
  prod{`b*` : byte*, name : name} b*{b <- `b*`}:Blist(syntax byte, grammar Bbyte) => name
    -- if ($utf8(name!`%`_name.0) = b*{b <- `b*`})

;; A-binary.watsup
grammar Btypeidx : typeidx
  ;; A-binary.watsup
  prod{x : idx} x:Bu32 => x

;; A-binary.watsup
grammar Bfuncidx : funcidx
  ;; A-binary.watsup
  prod{x : idx} x:Bu32 => x

;; A-binary.watsup
grammar Bglobalidx : globalidx
  ;; A-binary.watsup
  prod{x : idx} x:Bu32 => x

;; A-binary.watsup
grammar Btableidx : tableidx
  ;; A-binary.watsup
  prod{x : idx} x:Bu32 => x

;; A-binary.watsup
grammar Bmemidx : memidx
  ;; A-binary.watsup
  prod{x : idx} x:Bu32 => x

;; A-binary.watsup
grammar Btagidx : tagidx
  ;; A-binary.watsup
  prod{x : idx} x:Bu32 => x

;; A-binary.watsup
grammar Belemidx : elemidx
  ;; A-binary.watsup
  prod{x : idx} x:Bu32 => x

;; A-binary.watsup
grammar Bdataidx : dataidx
  ;; A-binary.watsup
  prod{x : idx} x:Bu32 => x

;; A-binary.watsup
grammar Blocalidx : localidx
  ;; A-binary.watsup
  prod{x : idx} x:Bu32 => x

;; A-binary.watsup
grammar Blabelidx : labelidx
  ;; A-binary.watsup
  prod{l : labelidx} l:Bu32 => l

;; A-binary.watsup
grammar Bexternidx : externidx
  ;; A-binary.watsup
  prod{x : idx} {0x00 x:Bfuncidx} => FUNC_externidx(x)
  ;; A-binary.watsup
  prod{x : idx} {0x01 x:Btableidx} => TABLE_externidx(x)
  ;; A-binary.watsup
  prod{x : idx} {0x02 x:Bmemidx} => MEM_externidx(x)
  ;; A-binary.watsup
  prod{x : idx} {0x03 x:Bglobalidx} => GLOBAL_externidx(x)
  ;; A-binary.watsup
  prod{x : idx} {0x04 x:Btagidx} => TAG_externidx(x)

;; A-binary.watsup
grammar Bnumtype : numtype
  ;; A-binary.watsup
  prod 0x7C => F64_numtype
  ;; A-binary.watsup
  prod 0x7D => F32_numtype
  ;; A-binary.watsup
  prod 0x7E => I64_numtype
  ;; A-binary.watsup
  prod 0x7F => I32_numtype

;; A-binary.watsup
grammar Bvectype : vectype
  ;; A-binary.watsup
  prod 0x7B => V128_vectype

;; A-binary.watsup
grammar Babsheaptype : heaptype
  ;; A-binary.watsup
  prod 0x69 => EXN_heaptype
  ;; A-binary.watsup
  prod 0x6A => ARRAY_heaptype
  ;; A-binary.watsup
  prod 0x6B => STRUCT_heaptype
  ;; A-binary.watsup
  prod 0x6C => I31_heaptype
  ;; A-binary.watsup
  prod 0x6D => EQ_heaptype
  ;; A-binary.watsup
  prod 0x6E => ANY_heaptype
  ;; A-binary.watsup
  prod 0x6F => EXTERN_heaptype
  ;; A-binary.watsup
  prod 0x70 => FUNC_heaptype
  ;; A-binary.watsup
  prod 0x71 => NONE_heaptype
  ;; A-binary.watsup
  prod 0x72 => NOEXTERN_heaptype
  ;; A-binary.watsup
  prod 0x73 => NOFUNC_heaptype
  ;; A-binary.watsup
  prod 0x74 => NOEXN_heaptype

;; A-binary.watsup
grammar Bheaptype : heaptype
  ;; A-binary.watsup
  prod{ht : heaptype} ht:Babsheaptype => ht
  ;; A-binary.watsup
  prod{x33 : s33} x33:Bs33 => _IDX_heaptype($s33_to_u32(x33))
    -- if (x33!`%`_s33.0 >= (0 : nat <:> int))

;; A-binary.watsup
grammar Breftype : reftype
  ;; A-binary.watsup
  prod{ht : heaptype} {0x63 ht:Bheaptype} => REF_reftype(?(NULL_NULL), ht)
  ;; A-binary.watsup
  prod{ht : heaptype} {0x64 ht:Bheaptype} => REF_reftype(?(), ht)
  ;; A-binary.watsup
  prod{ht : heaptype} ht:Babsheaptype => REF_reftype(?(NULL_NULL), ht)

;; A-binary.watsup
grammar Bvaltype : valtype
  ;; A-binary.watsup
  prod{nt : numtype} nt:Bnumtype => (nt : numtype <: valtype)
  ;; A-binary.watsup
  prod{vt : vectype} vt:Bvectype => (vt : vectype <: valtype)
  ;; A-binary.watsup
  prod{rt : reftype} rt:Breftype => (rt : reftype <: valtype)

;; A-binary.watsup
grammar Bresulttype : resulttype
  ;; A-binary.watsup
  prod{`t*` : valtype*} t*{t <- `t*`}:Blist(syntax valtype, grammar Bvaltype) => `%`_resulttype(t*{t <- `t*`})

;; A-binary.watsup
grammar Bmut : mut
  ;; A-binary.watsup
  prod 0x00 => ?()
  ;; A-binary.watsup
  prod 0x01 => ?(MUT_MUT)

;; A-binary.watsup
grammar Bpacktype : packtype
  ;; A-binary.watsup
  prod 0x77 => I16_packtype
  ;; A-binary.watsup
  prod 0x78 => I8_packtype

;; A-binary.watsup
grammar Bstoragetype : storagetype
  ;; A-binary.watsup
  prod{t : valtype} t:Bvaltype => (t : valtype <: storagetype)
  ;; A-binary.watsup
  prod{pt : packtype} pt:Bpacktype => (pt : packtype <: storagetype)

;; A-binary.watsup
grammar Bfieldtype : fieldtype
  ;; A-binary.watsup
  prod{zt : storagetype, mut : mut} {zt:Bstoragetype mut:Bmut} => `%%`_fieldtype(mut, zt)

;; A-binary.watsup
grammar Bcomptype : comptype
  ;; A-binary.watsup
  prod{yt : fieldtype} {0x5E yt:Bfieldtype} => ARRAY_comptype(yt)
  ;; A-binary.watsup
  prod{`yt*` : fieldtype*} {0x5F yt*{yt <- `yt*`}:Blist(syntax fieldtype, grammar Bfieldtype)} => STRUCT_comptype(`%`_structtype(yt*{yt <- `yt*`}))
  ;; A-binary.watsup
  prod{`t_1*` : valtype*, `t_2*` : valtype*} {0x60 `%`_resulttype(t_1*{t_1 <- `t_1*`}):Bresulttype `%`_resulttype(t_2*{t_2 <- `t_2*`}):Bresulttype} => FUNC_comptype(`%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`})))

;; A-binary.watsup
grammar Bsubtype : subtype
  ;; A-binary.watsup
  prod{`x*` : idx*, ct : comptype} {0x4F x*{x <- `x*`}:Blist(syntax typeidx, grammar Btypeidx) ct:Bcomptype} => SUB_subtype(?(FINAL_FINAL), _IDX_typeuse(x)*{x <- `x*`}, ct)
  ;; A-binary.watsup
  prod{`x*` : idx*, ct : comptype} {0x50 x*{x <- `x*`}:Blist(syntax typeidx, grammar Btypeidx) ct:Bcomptype} => SUB_subtype(?(), _IDX_typeuse(x)*{x <- `x*`}, ct)
  ;; A-binary.watsup
  prod{ct : comptype} ct:Bcomptype => SUB_subtype(?(FINAL_FINAL), [], ct)

;; A-binary.watsup
grammar Brectype : rectype
  ;; A-binary.watsup
  prod{`st*` : subtype*} {0x4E st*{st <- `st*`}:Blist(syntax subtype, grammar Bsubtype)} => REC_rectype(`%`_list(st*{st <- `st*`}))
  ;; A-binary.watsup
  prod{st : subtype} st:Bsubtype => REC_rectype(`%`_list([st]))

;; A-binary.watsup
grammar Blimits : (addrtype, limits)
  ;; A-binary.watsup
  prod{n : n} {0x00 `%`_u64(n):Bu64} => (I32_addrtype, `[%..%]`_limits(`%`_u64(n), `%`_u64(((((2 ^ 64) : nat <:> int) - (1 : nat <:> int)) : int <:> nat))))
  ;; A-binary.watsup
  prod{n : n, m : m} {0x01 `%`_u64(n):Bu64 `%`_u64(m):Bu64} => (I64_addrtype, `[%..%]`_limits(`%`_u64(n), `%`_u64(m)))
  ;; A-binary.watsup
  prod{n : n} {0x04 `%`_u64(n):Bu64} => (I32_addrtype, `[%..%]`_limits(`%`_u64(n), `%`_u64(((((2 ^ 64) : nat <:> int) - (1 : nat <:> int)) : int <:> nat))))
  ;; A-binary.watsup
  prod{n : n, m : m} {0x05 `%`_u64(n):Bu64 `%`_u64(m):Bu64} => (I64_addrtype, `[%..%]`_limits(`%`_u64(n), `%`_u64(m)))

;; A-binary.watsup
grammar Bglobaltype : globaltype
  ;; A-binary.watsup
  prod{t : valtype, mut : mut} {t:Bvaltype mut:Bmut} => `%%`_globaltype(mut, t)

;; A-binary.watsup
grammar Btabletype : tabletype
  ;; A-binary.watsup
  prod{rt : reftype, at : addrtype, lim : limits} {rt:Breftype (at, lim):Blimits} => `%%%`_tabletype(at, lim, rt)

;; A-binary.watsup
grammar Bmemtype : memtype
  ;; A-binary.watsup
  prod{at : addrtype, lim : limits} (at, lim):Blimits => `%%PAGE`_memtype(at, lim)

;; A-binary.watsup
grammar Btagtype : typeidx
  ;; A-binary.watsup
  prod{x : idx} {0x00 x:Btypeidx} => x

;; A-binary.watsup
grammar Bexterntype : externtype
  ;; A-binary.watsup
  prod{x : idx} {0x00 x:Btypeidx} => FUNC_externtype(_IDX_typeuse(x))
  ;; A-binary.watsup
  prod{tt : tabletype} {0x01 tt:Btabletype} => TABLE_externtype(tt)
  ;; A-binary.watsup
  prod{mt : memtype} {0x02 mt:Bmemtype} => MEM_externtype(mt)
  ;; A-binary.watsup
  prod{gt : globaltype} {0x03 gt:Bglobaltype} => GLOBAL_externtype(gt)
  ;; A-binary.watsup
  prod{x : idx} {0x04 x:Btagtype} => TAG_externtype(_IDX_typeuse(x))

;; A-binary.watsup
grammar Bblocktype : blocktype
  ;; A-binary.watsup
  prod 0x40 => _RESULT_blocktype(?())
  ;; A-binary.watsup
  prod{t : valtype} t:Bvaltype => _RESULT_blocktype(?(t))
  ;; A-binary.watsup
  prod{i : s33} i:Bs33 => _IDX_blocktype(`%`_funcidx((i!`%`_s33.0 : int <:> nat)))
    -- if (i!`%`_s33.0 >= (0 : nat <:> int))

;; A-binary.watsup
grammar Bcatch : catch
  ;; A-binary.watsup
  prod{x : idx, l : labelidx} {0x00 x:Btagidx l:Blabelidx} => CATCH_catch(x, l)
  ;; A-binary.watsup
  prod{x : idx, l : labelidx} {0x01 x:Btagidx l:Blabelidx} => CATCH_REF_catch(x, l)
  ;; A-binary.watsup
  prod{l : labelidx} {0x02 l:Blabelidx} => CATCH_ALL_catch(l)
  ;; A-binary.watsup
  prod{l : labelidx} {0x03 l:Blabelidx} => CATCH_ALL_REF_catch(l)

;; A-binary.watsup
syntax castop = (nul, nul)

;; A-binary.watsup
grammar Bcastop : castop
  ;; A-binary.watsup
  prod 0x00 => (?(), ?())
  ;; A-binary.watsup
  prod 0x01 => (?(NULL_NULL), ?())
  ;; A-binary.watsup
  prod 0x02 => (?(), ?(NULL_NULL))
  ;; A-binary.watsup
  prod 0x03 => (?(NULL_NULL), ?(NULL_NULL))

;; A-binary.watsup
syntax memidxop = (memidx, memarg)

;; A-binary.watsup
grammar Bmemarg : memidxop
  ;; A-binary.watsup
  prod{n : n, m : m} {`%`_u32(n):Bu32 `%`_u32(m):Bu32} => (`%`_memidx(0), {ALIGN `%`_u32(n), OFFSET `%`_u32(m)})
    -- if (n < (2 ^ 6))
  ;; A-binary.watsup
  prod{n : n, x : idx, m : m} {`%`_u32(n):Bu32 x:Bmemidx `%`_u32(m):Bu32} => (x, {ALIGN `%`_u32((((n : nat <:> int) - ((2 ^ 6) : nat <:> int)) : int <:> nat)), OFFSET `%`_u32(m)})
    -- if (((2 ^ 6) <= n) /\ (n < (2 ^ 7)))

;; A-binary.watsup
grammar Blaneidx : laneidx
  ;; A-binary.watsup
  prod{l : labelidx} `%`_byte(l!`%`_labelidx.0):Bbyte => `%`_laneidx(l!`%`_labelidx.0)

;; A-binary.watsup
rec {

;; A-binary.watsup:994.1-1008.73
grammar Binstr : instr
  ;; A-binary.watsup:216.5-216.24
  prod 0x00 => UNREACHABLE_instr
  ;; A-binary.watsup:217.5-217.16
  prod 0x01 => NOP_instr
  ;; A-binary.watsup:218.5-218.57
  prod{bt : blocktype, `in*` : instr*} {0x02 bt:Bblocktype in:Binstr*{in <- `in*`} 0x0B} => BLOCK_instr(bt, in*{in <- `in*`})
  ;; A-binary.watsup:219.5-219.56
  prod{bt : blocktype, `in*` : instr*} {0x03 bt:Bblocktype in:Binstr*{in <- `in*`} 0x0B} => LOOP_instr(bt, in*{in <- `in*`})
  ;; A-binary.watsup:220.5-220.63
  prod{bt : blocktype, `in*` : instr*} {0x04 bt:Bblocktype in:Binstr*{in <- `in*`} 0x0B} => `IF%%ELSE%`_instr(bt, in*{in <- `in*`}, [])
  ;; A-binary.watsup:221.5-222.55
  prod{bt : blocktype, `in_1*` : instr*, `in_2*` : instr*} {0x04 bt:Bblocktype in_1:Binstr*{in_1 <- `in_1*`} 0x05 in_2:Binstr*{in_2 <- `in_2*`} 0x0B} => `IF%%ELSE%`_instr(bt, in_1*{in_1 <- `in_1*`}, in_2*{in_2 <- `in_2*`})
  ;; A-binary.watsup:223.5-223.30
  prod{x : idx} {0x08 x:Btagidx} => THROW_instr(x)
  ;; A-binary.watsup:224.5-224.22
  prod 0x0A => THROW_REF_instr
  ;; A-binary.watsup:225.5-225.29
  prod{l : labelidx} {0x0C l:Blabelidx} => BR_instr(l)
  ;; A-binary.watsup:226.5-226.32
  prod{l : labelidx} {0x0D l:Blabelidx} => BR_IF_instr(l)
  ;; A-binary.watsup:227.5-227.62
  prod{`l*` : labelidx*, l_n : labelidx} {0x0E l*{l <- `l*`}:Blist(syntax labelidx, grammar Blabelidx) l_n:Blabelidx} => BR_TABLE_instr(l*{l <- `l*`}, l_n)
  ;; A-binary.watsup:228.5-228.19
  prod 0x0F => RETURN_instr
  ;; A-binary.watsup:229.5-229.30
  prod{x : idx} {0x10 x:Bfuncidx} => CALL_instr(x)
  ;; A-binary.watsup:230.5-230.60
  prod{y : idx, x : idx} {0x11 y:Btypeidx x:Btableidx} => CALL_INDIRECT_instr(x, _IDX_typeuse(y))
  ;; A-binary.watsup:231.5-231.37
  prod{x : idx} {0x12 x:Bfuncidx} => RETURN_CALL_instr(x)
  ;; A-binary.watsup:232.5-232.67
  prod{y : idx, x : idx} {0x13 y:Btypeidx x:Btableidx} => RETURN_CALL_INDIRECT_instr(x, _IDX_typeuse(y))
  ;; A-binary.watsup:233.5-233.81
  prod{bt : blocktype, `c*` : catch*, `in*` : instr*} {0x1F bt:Bblocktype c*{c <- `c*`}:Blist(syntax catch, grammar Bcatch) in:Binstr*{in <- `in*`} 0x0B} => TRY_TABLE_instr(bt, `%`_list(c*{c <- `c*`}), in*{in <- `in*`})
  ;; A-binary.watsup:254.5-254.37
  prod{ht : heaptype} {0xD0 ht:Bheaptype} => REF.NULL_instr(ht)
  ;; A-binary.watsup:255.5-255.24
  prod 0xD1 => REF.IS_NULL_instr
  ;; A-binary.watsup:256.5-256.34
  prod{x : idx} {0xD2 x:Bfuncidx} => REF.FUNC_instr(x)
  ;; A-binary.watsup:257.5-257.19
  prod 0xD3 => REF.EQ_instr
  ;; A-binary.watsup:258.5-258.28
  prod 0xD4 => REF.AS_NON_NULL_instr
  ;; A-binary.watsup:259.5-259.37
  prod{l : labelidx} {0xD5 l:Blabelidx} => BR_ON_NULL_instr(l)
  ;; A-binary.watsup:260.5-260.41
  prod{l : labelidx} {0xD6 l:Blabelidx} => BR_ON_NON_NULL_instr(l)
  ;; A-binary.watsup:264.5-264.43
  prod{x : idx} {0xFB `%`_u32(0):Bu32 x:Btypeidx} => STRUCT.NEW_instr(x)
  ;; A-binary.watsup:265.5-265.51
  prod{x : idx} {0xFB `%`_u32(1):Bu32 x:Btypeidx} => STRUCT.NEW_DEFAULT_instr(x)
  ;; A-binary.watsup:266.5-266.52
  prod{x : idx, i : u32} {0xFB `%`_u32(2):Bu32 x:Btypeidx i:Bu32} => STRUCT.GET_instr(?(), x, i)
  ;; A-binary.watsup:267.5-267.54
  prod{x : idx, i : u32} {0xFB `%`_u32(3):Bu32 x:Btypeidx i:Bu32} => STRUCT.GET_instr(?(S_sx), x, i)
  ;; A-binary.watsup:268.5-268.54
  prod{x : idx, i : u32} {0xFB `%`_u32(4):Bu32 x:Btypeidx i:Bu32} => STRUCT.GET_instr(?(U_sx), x, i)
  ;; A-binary.watsup:269.5-269.52
  prod{x : idx, i : u32} {0xFB `%`_u32(5):Bu32 x:Btypeidx i:Bu32} => STRUCT.SET_instr(x, i)
  ;; A-binary.watsup:273.5-273.42
  prod{x : idx} {0xFB `%`_u32(6):Bu32 x:Btypeidx} => ARRAY.NEW_instr(x)
  ;; A-binary.watsup:274.5-274.50
  prod{x : idx} {0xFB `%`_u32(7):Bu32 x:Btypeidx} => ARRAY.NEW_DEFAULT_instr(x)
  ;; A-binary.watsup:275.5-275.57
  prod{x : idx, n : n} {0xFB `%`_u32(8):Bu32 x:Btypeidx `%`_u32(n):Bu32} => ARRAY.NEW_FIXED_instr(x, `%`_u32(n))
  ;; A-binary.watsup:276.5-276.60
  prod{x : idx, y : idx} {0xFB `%`_u32(9):Bu32 x:Btypeidx y:Bdataidx} => ARRAY.NEW_DATA_instr(x, y)
  ;; A-binary.watsup:277.5-277.61
  prod{x : idx, y : idx} {0xFB `%`_u32(10):Bu32 x:Btypeidx y:Belemidx} => ARRAY.NEW_ELEM_instr(x, y)
  ;; A-binary.watsup:278.5-278.43
  prod{x : idx} {0xFB `%`_u32(11):Bu32 x:Btypeidx} => ARRAY.GET_instr(?(), x)
  ;; A-binary.watsup:279.5-279.45
  prod{x : idx} {0xFB `%`_u32(12):Bu32 x:Btypeidx} => ARRAY.GET_instr(?(S_sx), x)
  ;; A-binary.watsup:280.5-280.45
  prod{x : idx} {0xFB `%`_u32(13):Bu32 x:Btypeidx} => ARRAY.GET_instr(?(U_sx), x)
  ;; A-binary.watsup:281.5-281.43
  prod{x : idx} {0xFB `%`_u32(14):Bu32 x:Btypeidx} => ARRAY.SET_instr(x)
  ;; A-binary.watsup:282.5-282.30
  prod {0xFB `%`_u32(15):Bu32} => ARRAY.LEN_instr
  ;; A-binary.watsup:283.5-283.44
  prod{x : idx} {0xFB `%`_u32(16):Bu32 x:Btypeidx} => ARRAY.FILL_instr(x)
  ;; A-binary.watsup:284.5-284.65
  prod{x_1 : idx, x_2 : idx} {0xFB `%`_u32(17):Bu32 x_1:Btypeidx x_2:Btypeidx} => ARRAY.COPY_instr(x_1, x_2)
  ;; A-binary.watsup:285.5-285.62
  prod{x : idx, y : idx} {0xFB `%`_u32(18):Bu32 x:Btypeidx y:Bdataidx} => ARRAY.INIT_DATA_instr(x, y)
  ;; A-binary.watsup:286.5-286.62
  prod{x : idx, y : idx} {0xFB `%`_u32(19):Bu32 x:Btypeidx y:Belemidx} => ARRAY.INIT_ELEM_instr(x, y)
  ;; A-binary.watsup:290.5-290.51
  prod{ht : heaptype} {0xFB `%`_u32(20):Bu32 ht:Bheaptype} => REF.TEST_instr(REF_reftype(?(), ht))
  ;; A-binary.watsup:291.5-291.56
  prod{ht : heaptype} {0xFB `%`_u32(21):Bu32 ht:Bheaptype} => REF.TEST_instr(REF_reftype(?(NULL_NULL), ht))
  ;; A-binary.watsup:292.5-292.51
  prod{ht : heaptype} {0xFB `%`_u32(22):Bu32 ht:Bheaptype} => REF.CAST_instr(REF_reftype(?(), ht))
  ;; A-binary.watsup:293.5-293.56
  prod{ht : heaptype} {0xFB `%`_u32(23):Bu32 ht:Bheaptype} => REF.CAST_instr(REF_reftype(?(NULL_NULL), ht))
  ;; A-binary.watsup:294.5-295.94
  prod{nul1 : nul1, nul2 : nul2, l : labelidx, ht_1 : heaptype, ht_2 : heaptype} {0xFB `%`_u32(24):Bu32 (nul1, nul2):Bcastop l:Blabelidx ht_1:Bheaptype ht_2:Bheaptype} => BR_ON_CAST_instr(l, REF_reftype(nul1, ht_1), REF_reftype(nul2, ht_2))
  ;; A-binary.watsup:296.5-297.99
  prod{nul1 : nul1, nul2 : nul2, l : labelidx, ht_1 : heaptype, ht_2 : heaptype} {0xFB `%`_u32(25):Bu32 (nul1, nul2):Bcastop l:Blabelidx ht_1:Bheaptype ht_2:Bheaptype} => BR_ON_CAST_FAIL_instr(l, REF_reftype(nul1, ht_1), REF_reftype(nul2, ht_2))
  ;; A-binary.watsup:301.5-301.39
  prod {0xFB `%`_u32(26):Bu32} => ANY.CONVERT_EXTERN_instr
  ;; A-binary.watsup:302.5-302.39
  prod {0xFB `%`_u32(27):Bu32} => EXTERN.CONVERT_ANY_instr
  ;; A-binary.watsup:306.5-306.28
  prod {0xFB `%`_u32(28):Bu32} => REF.I31_instr
  ;; A-binary.watsup:307.5-307.30
  prod {0xFB `%`_u32(29):Bu32} => I31.GET_instr(S_sx)
  ;; A-binary.watsup:308.5-308.30
  prod {0xFB `%`_u32(30):Bu32} => I31.GET_instr(U_sx)
  ;; A-binary.watsup:315.5-315.17
  prod 0x1A => DROP_instr
  ;; A-binary.watsup:316.5-316.19
  prod 0x1B => SELECT_instr(?())
  ;; A-binary.watsup:317.5-317.41
  prod{ts : valtype} {0x1C [ts]:Blist(syntax valtype, grammar Bvaltype)} => SELECT_instr(?([ts]))
  ;; A-binary.watsup:324.5-324.36
  prod{x : idx} {0x20 x:Blocalidx} => LOCAL.GET_instr(x)
  ;; A-binary.watsup:325.5-325.36
  prod{x : idx} {0x21 x:Blocalidx} => LOCAL.SET_instr(x)
  ;; A-binary.watsup:326.5-326.36
  prod{x : idx} {0x22 x:Blocalidx} => LOCAL.TEE_instr(x)
  ;; A-binary.watsup:330.5-330.38
  prod{x : idx} {0x23 x:Bglobalidx} => GLOBAL.GET_instr(x)
  ;; A-binary.watsup:331.5-331.38
  prod{x : idx} {0x24 x:Bglobalidx} => GLOBAL.SET_instr(x)
  ;; A-binary.watsup:338.5-338.36
  prod{x : idx} {0x25 x:Btableidx} => TABLE.GET_instr(x)
  ;; A-binary.watsup:339.5-339.36
  prod{x : idx} {0x26 x:Btableidx} => TABLE.SET_instr(x)
  ;; A-binary.watsup:340.5-340.58
  prod{y : idx, x : idx} {0xFC `%`_u32(12):Bu32 y:Belemidx x:Btableidx} => TABLE.INIT_instr(x, y)
  ;; A-binary.watsup:341.5-341.43
  prod{x : idx} {0xFC `%`_u32(13):Bu32 x:Belemidx} => ELEM.DROP_instr(x)
  ;; A-binary.watsup:342.5-342.67
  prod{x_1 : idx, x_2 : idx} {0xFC `%`_u32(14):Bu32 x_1:Btableidx x_2:Btableidx} => TABLE.COPY_instr(x_1, x_2)
  ;; A-binary.watsup:343.5-343.45
  prod{x : idx} {0xFC `%`_u32(15):Bu32 x:Btableidx} => TABLE.GROW_instr(x)
  ;; A-binary.watsup:344.5-344.45
  prod{x : idx} {0xFC `%`_u32(16):Bu32 x:Btableidx} => TABLE.SIZE_instr(x)
  ;; A-binary.watsup:345.5-345.45
  prod{x : idx} {0xFC `%`_u32(17):Bu32 x:Btableidx} => TABLE.FILL_instr(x)
  ;; A-binary.watsup:358.5-358.41
  prod{x : idx, ao : memarg} {0x28 (x, ao):Bmemarg} => LOAD_instr(I32_numtype, ?(), x, ao)
  ;; A-binary.watsup:359.5-359.41
  prod{x : idx, ao : memarg} {0x29 (x, ao):Bmemarg} => LOAD_instr(I64_numtype, ?(), x, ao)
  ;; A-binary.watsup:360.5-360.41
  prod{x : idx, ao : memarg} {0x2A (x, ao):Bmemarg} => LOAD_instr(F32_numtype, ?(), x, ao)
  ;; A-binary.watsup:361.5-361.41
  prod{x : idx, ao : memarg} {0x2B (x, ao):Bmemarg} => LOAD_instr(F64_numtype, ?(), x, ao)
  ;; A-binary.watsup:362.5-362.50
  prod{x : idx, ao : memarg} {0x2C (x, ao):Bmemarg} => LOAD_instr(I32_numtype, ?(`%_%`_loadop_(`%`_sz(8), S_sx)), x, ao)
  ;; A-binary.watsup:363.5-363.50
  prod{x : idx, ao : memarg} {0x2D (x, ao):Bmemarg} => LOAD_instr(I32_numtype, ?(`%_%`_loadop_(`%`_sz(8), U_sx)), x, ao)
  ;; A-binary.watsup:364.5-364.51
  prod{x : idx, ao : memarg} {0x2E (x, ao):Bmemarg} => LOAD_instr(I32_numtype, ?(`%_%`_loadop_(`%`_sz(16), S_sx)), x, ao)
  ;; A-binary.watsup:365.5-365.51
  prod{x : idx, ao : memarg} {0x2F (x, ao):Bmemarg} => LOAD_instr(I32_numtype, ?(`%_%`_loadop_(`%`_sz(16), U_sx)), x, ao)
  ;; A-binary.watsup:366.5-366.50
  prod{x : idx, ao : memarg} {0x30 (x, ao):Bmemarg} => LOAD_instr(I64_numtype, ?(`%_%`_loadop_(`%`_sz(8), S_sx)), x, ao)
  ;; A-binary.watsup:367.5-367.50
  prod{x : idx, ao : memarg} {0x31 (x, ao):Bmemarg} => LOAD_instr(I64_numtype, ?(`%_%`_loadop_(`%`_sz(8), U_sx)), x, ao)
  ;; A-binary.watsup:368.5-368.51
  prod{x : idx, ao : memarg} {0x32 (x, ao):Bmemarg} => LOAD_instr(I64_numtype, ?(`%_%`_loadop_(`%`_sz(16), S_sx)), x, ao)
  ;; A-binary.watsup:369.5-369.51
  prod{x : idx, ao : memarg} {0x33 (x, ao):Bmemarg} => LOAD_instr(I64_numtype, ?(`%_%`_loadop_(`%`_sz(16), U_sx)), x, ao)
  ;; A-binary.watsup:370.5-370.51
  prod{x : idx, ao : memarg} {0x34 (x, ao):Bmemarg} => LOAD_instr(I64_numtype, ?(`%_%`_loadop_(`%`_sz(32), S_sx)), x, ao)
  ;; A-binary.watsup:371.5-371.51
  prod{x : idx, ao : memarg} {0x35 (x, ao):Bmemarg} => LOAD_instr(I64_numtype, ?(`%_%`_loadop_(`%`_sz(32), U_sx)), x, ao)
  ;; A-binary.watsup:372.5-372.42
  prod{x : idx, ao : memarg} {0x36 (x, ao):Bmemarg} => STORE_instr(I32_numtype, ?(), x, ao)
  ;; A-binary.watsup:373.5-373.42
  prod{x : idx, ao : memarg} {0x37 (x, ao):Bmemarg} => STORE_instr(I64_numtype, ?(), x, ao)
  ;; A-binary.watsup:374.5-374.42
  prod{x : idx, ao : memarg} {0x38 (x, ao):Bmemarg} => STORE_instr(F32_numtype, ?(), x, ao)
  ;; A-binary.watsup:375.5-375.42
  prod{x : idx, ao : memarg} {0x39 (x, ao):Bmemarg} => STORE_instr(F64_numtype, ?(), x, ao)
  ;; A-binary.watsup:376.5-376.45
  prod{x : idx, ao : memarg} {0x3A (x, ao):Bmemarg} => STORE_instr(I32_numtype, ?(`%`_storeop_(`%`_sz(8))), x, ao)
  ;; A-binary.watsup:377.5-377.46
  prod{x : idx, ao : memarg} {0x3B (x, ao):Bmemarg} => STORE_instr(I32_numtype, ?(`%`_storeop_(`%`_sz(16))), x, ao)
  ;; A-binary.watsup:378.5-378.45
  prod{x : idx, ao : memarg} {0x3C (x, ao):Bmemarg} => STORE_instr(I64_numtype, ?(`%`_storeop_(`%`_sz(8))), x, ao)
  ;; A-binary.watsup:379.5-379.46
  prod{x : idx, ao : memarg} {0x3D (x, ao):Bmemarg} => STORE_instr(I64_numtype, ?(`%`_storeop_(`%`_sz(16))), x, ao)
  ;; A-binary.watsup:380.5-380.46
  prod{x : idx, ao : memarg} {0x3E (x, ao):Bmemarg} => STORE_instr(I64_numtype, ?(`%`_storeop_(`%`_sz(32))), x, ao)
  ;; A-binary.watsup:381.5-381.36
  prod{x : idx} {0x3F x:Bmemidx} => MEMORY.SIZE_instr(x)
  ;; A-binary.watsup:382.5-382.36
  prod{x : idx} {0x40 x:Bmemidx} => MEMORY.GROW_instr(x)
  ;; A-binary.watsup:383.5-383.56
  prod{y : idx, x : idx} {0xFC `%`_u32(8):Bu32 y:Bdataidx x:Bmemidx} => MEMORY.INIT_instr(x, y)
  ;; A-binary.watsup:384.5-384.42
  prod{x : idx} {0xFC `%`_u32(9):Bu32 x:Bdataidx} => DATA.DROP_instr(x)
  ;; A-binary.watsup:385.5-385.64
  prod{x_1 : idx, x_2 : idx} {0xFC `%`_u32(10):Bu32 x_1:Bmemidx x_2:Bmemidx} => MEMORY.COPY_instr(x_1, x_2)
  ;; A-binary.watsup:386.5-386.44
  prod{x : idx} {0xFC `%`_u32(11):Bu32 x:Bmemidx} => MEMORY.FILL_instr(x)
  ;; A-binary.watsup:394.5-394.31
  prod{n : n} {0x41 `%`_u32(n):Bu32} => CONST_instr(I32_numtype, `%`_num_(n))
  ;; A-binary.watsup:395.5-395.31
  prod{n : n} {0x42 `%`_u64(n):Bu64} => CONST_instr(I64_numtype, `%`_num_(n))
  ;; A-binary.watsup:396.5-396.31
  prod{p : f32} {0x43 p:Bf32} => CONST_instr(F32_numtype, p)
  ;; A-binary.watsup:397.5-397.31
  prod{p : f64} {0x44 p:Bf64} => CONST_instr(F64_numtype, p)
  ;; A-binary.watsup:401.5-401.27
  prod 0x45 => TESTOP_instr(I32_numtype, EQZ_testop_)
  ;; A-binary.watsup:405.5-405.25
  prod 0x46 => RELOP_instr(I32_numtype, EQ_relop_)
  ;; A-binary.watsup:406.5-406.25
  prod 0x47 => RELOP_instr(I32_numtype, NE_relop_)
  ;; A-binary.watsup:407.5-407.29
  prod 0x48 => RELOP_instr(I32_numtype, LT_relop_(S_sx))
  ;; A-binary.watsup:408.5-408.29
  prod 0x49 => RELOP_instr(I32_numtype, LT_relop_(U_sx))
  ;; A-binary.watsup:409.5-409.29
  prod 0x4A => RELOP_instr(I32_numtype, GT_relop_(S_sx))
  ;; A-binary.watsup:410.5-410.29
  prod 0x4B => RELOP_instr(I32_numtype, GT_relop_(U_sx))
  ;; A-binary.watsup:411.5-411.29
  prod 0x4C => RELOP_instr(I32_numtype, LE_relop_(S_sx))
  ;; A-binary.watsup:412.5-412.29
  prod 0x4D => RELOP_instr(I32_numtype, LE_relop_(U_sx))
  ;; A-binary.watsup:413.5-413.29
  prod 0x4E => RELOP_instr(I32_numtype, GE_relop_(S_sx))
  ;; A-binary.watsup:414.5-414.29
  prod 0x4F => RELOP_instr(I32_numtype, GE_relop_(U_sx))
  ;; A-binary.watsup:418.5-418.27
  prod 0x50 => TESTOP_instr(I64_numtype, EQZ_testop_)
  ;; A-binary.watsup:422.5-422.25
  prod 0x51 => RELOP_instr(I64_numtype, EQ_relop_)
  ;; A-binary.watsup:423.5-423.25
  prod 0x52 => RELOP_instr(I64_numtype, NE_relop_)
  ;; A-binary.watsup:424.5-424.29
  prod 0x53 => RELOP_instr(I64_numtype, LT_relop_(S_sx))
  ;; A-binary.watsup:425.5-425.29
  prod 0x54 => RELOP_instr(I64_numtype, LT_relop_(U_sx))
  ;; A-binary.watsup:426.5-426.29
  prod 0x55 => RELOP_instr(I64_numtype, GT_relop_(S_sx))
  ;; A-binary.watsup:427.5-427.29
  prod 0x56 => RELOP_instr(I64_numtype, GT_relop_(U_sx))
  ;; A-binary.watsup:428.5-428.29
  prod 0x57 => RELOP_instr(I64_numtype, LE_relop_(S_sx))
  ;; A-binary.watsup:429.5-429.29
  prod 0x58 => RELOP_instr(I64_numtype, LE_relop_(U_sx))
  ;; A-binary.watsup:430.5-430.29
  prod 0x59 => RELOP_instr(I64_numtype, GE_relop_(S_sx))
  ;; A-binary.watsup:431.5-431.29
  prod 0x5A => RELOP_instr(I64_numtype, GE_relop_(U_sx))
  ;; A-binary.watsup:435.5-435.25
  prod 0x5B => RELOP_instr(F32_numtype, EQ_relop_)
  ;; A-binary.watsup:436.5-436.25
  prod 0x5C => RELOP_instr(F32_numtype, NE_relop_)
  ;; A-binary.watsup:437.5-437.25
  prod 0x5D => RELOP_instr(F32_numtype, LT_relop_)
  ;; A-binary.watsup:438.5-438.25
  prod 0x5E => RELOP_instr(F32_numtype, GT_relop_)
  ;; A-binary.watsup:439.5-439.25
  prod 0x5F => RELOP_instr(F32_numtype, LE_relop_)
  ;; A-binary.watsup:440.5-440.25
  prod 0x60 => RELOP_instr(F32_numtype, GE_relop_)
  ;; A-binary.watsup:444.5-444.25
  prod 0x61 => RELOP_instr(F64_numtype, EQ_relop_)
  ;; A-binary.watsup:445.5-445.25
  prod 0x62 => RELOP_instr(F64_numtype, NE_relop_)
  ;; A-binary.watsup:446.5-446.25
  prod 0x63 => RELOP_instr(F64_numtype, LT_relop_)
  ;; A-binary.watsup:447.5-447.25
  prod 0x64 => RELOP_instr(F64_numtype, GT_relop_)
  ;; A-binary.watsup:448.5-448.25
  prod 0x65 => RELOP_instr(F64_numtype, LE_relop_)
  ;; A-binary.watsup:449.5-449.25
  prod 0x66 => RELOP_instr(F64_numtype, GE_relop_)
  ;; A-binary.watsup:453.5-453.25
  prod 0x67 => UNOP_instr(I32_numtype, CLZ_unop_)
  ;; A-binary.watsup:454.5-454.25
  prod 0x68 => UNOP_instr(I32_numtype, CTZ_unop_)
  ;; A-binary.watsup:455.5-455.28
  prod 0x69 => UNOP_instr(I32_numtype, POPCNT_unop_)
  ;; A-binary.watsup:459.5-459.26
  prod 0x6A => BINOP_instr(I32_numtype, ADD_binop_)
  ;; A-binary.watsup:460.5-460.26
  prod 0x6B => BINOP_instr(I32_numtype, SUB_binop_)
  ;; A-binary.watsup:461.5-461.26
  prod 0x6C => BINOP_instr(I32_numtype, MUL_binop_)
  ;; A-binary.watsup:462.5-462.30
  prod 0x6D => BINOP_instr(I32_numtype, DIV_binop_(S_sx))
  ;; A-binary.watsup:463.5-463.30
  prod 0x6E => BINOP_instr(I32_numtype, DIV_binop_(U_sx))
  ;; A-binary.watsup:464.5-464.30
  prod 0x6F => BINOP_instr(I32_numtype, REM_binop_(S_sx))
  ;; A-binary.watsup:465.5-465.30
  prod 0x70 => BINOP_instr(I32_numtype, REM_binop_(U_sx))
  ;; A-binary.watsup:466.5-466.26
  prod 0x71 => BINOP_instr(I32_numtype, AND_binop_)
  ;; A-binary.watsup:467.5-467.25
  prod 0x72 => BINOP_instr(I32_numtype, OR_binop_)
  ;; A-binary.watsup:468.5-468.26
  prod 0x73 => BINOP_instr(I32_numtype, XOR_binop_)
  ;; A-binary.watsup:469.5-469.26
  prod 0x74 => BINOP_instr(I32_numtype, SHL_binop_)
  ;; A-binary.watsup:470.5-470.30
  prod 0x75 => BINOP_instr(I32_numtype, SHR_binop_(S_sx))
  ;; A-binary.watsup:471.5-471.30
  prod 0x76 => BINOP_instr(I32_numtype, SHR_binop_(U_sx))
  ;; A-binary.watsup:472.5-472.27
  prod 0x77 => BINOP_instr(I32_numtype, ROTL_binop_)
  ;; A-binary.watsup:473.5-473.27
  prod 0x78 => BINOP_instr(I32_numtype, ROTR_binop_)
  ;; A-binary.watsup:477.5-477.25
  prod 0x79 => UNOP_instr(I64_numtype, CLZ_unop_)
  ;; A-binary.watsup:478.5-478.25
  prod 0x7A => UNOP_instr(I64_numtype, CTZ_unop_)
  ;; A-binary.watsup:479.5-479.28
  prod 0x7B => UNOP_instr(I64_numtype, POPCNT_unop_)
  ;; A-binary.watsup:483.5-483.33
  prod 0xC0 => UNOP_instr(I32_numtype, EXTEND_unop_(`%`_sz(8)))
  ;; A-binary.watsup:484.5-484.34
  prod 0xC1 => UNOP_instr(I32_numtype, EXTEND_unop_(`%`_sz(16)))
  ;; A-binary.watsup:488.5-488.33
  prod 0xC2 => UNOP_instr(I64_numtype, EXTEND_unop_(`%`_sz(8)))
  ;; A-binary.watsup:489.5-489.34
  prod 0xC3 => UNOP_instr(I64_numtype, EXTEND_unop_(`%`_sz(16)))
  ;; A-binary.watsup:490.5-490.34
  prod 0xC4 => UNOP_instr(I64_numtype, EXTEND_unop_(`%`_sz(32)))
  ;; A-binary.watsup:494.5-494.26
  prod 0x7C => BINOP_instr(I64_numtype, ADD_binop_)
  ;; A-binary.watsup:495.5-495.26
  prod 0x7D => BINOP_instr(I64_numtype, SUB_binop_)
  ;; A-binary.watsup:496.5-496.26
  prod 0x7E => BINOP_instr(I64_numtype, MUL_binop_)
  ;; A-binary.watsup:497.5-497.30
  prod 0x7F => BINOP_instr(I64_numtype, DIV_binop_(S_sx))
  ;; A-binary.watsup:498.5-498.30
  prod 0x80 => BINOP_instr(I64_numtype, DIV_binop_(U_sx))
  ;; A-binary.watsup:499.5-499.30
  prod 0x81 => BINOP_instr(I64_numtype, REM_binop_(S_sx))
  ;; A-binary.watsup:500.5-500.30
  prod 0x82 => BINOP_instr(I64_numtype, REM_binop_(U_sx))
  ;; A-binary.watsup:501.5-501.26
  prod 0x83 => BINOP_instr(I64_numtype, AND_binop_)
  ;; A-binary.watsup:502.5-502.25
  prod 0x84 => BINOP_instr(I64_numtype, OR_binop_)
  ;; A-binary.watsup:503.5-503.26
  prod 0x85 => BINOP_instr(I64_numtype, XOR_binop_)
  ;; A-binary.watsup:504.5-504.26
  prod 0x86 => BINOP_instr(I64_numtype, SHL_binop_)
  ;; A-binary.watsup:505.5-505.30
  prod 0x87 => BINOP_instr(I64_numtype, SHR_binop_(S_sx))
  ;; A-binary.watsup:506.5-506.30
  prod 0x88 => BINOP_instr(I64_numtype, SHR_binop_(U_sx))
  ;; A-binary.watsup:507.5-507.27
  prod 0x89 => BINOP_instr(I64_numtype, ROTL_binop_)
  ;; A-binary.watsup:508.5-508.27
  prod 0x8A => BINOP_instr(I64_numtype, ROTR_binop_)
  ;; A-binary.watsup:512.5-512.25
  prod 0x8B => UNOP_instr(F32_numtype, ABS_unop_)
  ;; A-binary.watsup:513.5-513.25
  prod 0x8C => UNOP_instr(F32_numtype, NEG_unop_)
  ;; A-binary.watsup:514.5-514.26
  prod 0x8D => UNOP_instr(F32_numtype, CEIL_unop_)
  ;; A-binary.watsup:515.5-515.27
  prod 0x8E => UNOP_instr(F32_numtype, FLOOR_unop_)
  ;; A-binary.watsup:516.5-516.27
  prod 0x8F => UNOP_instr(F32_numtype, TRUNC_unop_)
  ;; A-binary.watsup:517.5-517.29
  prod 0x90 => UNOP_instr(F32_numtype, NEAREST_unop_)
  ;; A-binary.watsup:518.5-518.26
  prod 0x91 => UNOP_instr(F32_numtype, SQRT_unop_)
  ;; A-binary.watsup:522.5-522.26
  prod 0x92 => BINOP_instr(F32_numtype, ADD_binop_)
  ;; A-binary.watsup:523.5-523.26
  prod 0x93 => BINOP_instr(F32_numtype, SUB_binop_)
  ;; A-binary.watsup:524.5-524.26
  prod 0x94 => BINOP_instr(F32_numtype, MUL_binop_)
  ;; A-binary.watsup:525.5-525.26
  prod 0x95 => BINOP_instr(F32_numtype, DIV_binop_)
  ;; A-binary.watsup:526.5-526.26
  prod 0x96 => BINOP_instr(F32_numtype, MIN_binop_)
  ;; A-binary.watsup:527.5-527.26
  prod 0x97 => BINOP_instr(F32_numtype, MAX_binop_)
  ;; A-binary.watsup:528.5-528.31
  prod 0x98 => BINOP_instr(F32_numtype, COPYSIGN_binop_)
  ;; A-binary.watsup:532.5-532.25
  prod 0x99 => UNOP_instr(F64_numtype, ABS_unop_)
  ;; A-binary.watsup:533.5-533.25
  prod 0x9A => UNOP_instr(F64_numtype, NEG_unop_)
  ;; A-binary.watsup:534.5-534.26
  prod 0x9B => UNOP_instr(F64_numtype, CEIL_unop_)
  ;; A-binary.watsup:535.5-535.27
  prod 0x9C => UNOP_instr(F64_numtype, FLOOR_unop_)
  ;; A-binary.watsup:536.5-536.27
  prod 0x9D => UNOP_instr(F64_numtype, TRUNC_unop_)
  ;; A-binary.watsup:537.5-537.29
  prod 0x9E => UNOP_instr(F64_numtype, NEAREST_unop_)
  ;; A-binary.watsup:538.5-538.26
  prod 0x9F => UNOP_instr(F64_numtype, SQRT_unop_)
  ;; A-binary.watsup:542.5-542.26
  prod 0xA0 => BINOP_instr(F64_numtype, ADD_binop_)
  ;; A-binary.watsup:543.5-543.26
  prod 0xA1 => BINOP_instr(F64_numtype, SUB_binop_)
  ;; A-binary.watsup:544.5-544.26
  prod 0xA2 => BINOP_instr(F64_numtype, MUL_binop_)
  ;; A-binary.watsup:545.5-545.26
  prod 0xA3 => BINOP_instr(F64_numtype, DIV_binop_)
  ;; A-binary.watsup:546.5-546.26
  prod 0xA4 => BINOP_instr(F64_numtype, MIN_binop_)
  ;; A-binary.watsup:547.5-547.26
  prod 0xA5 => BINOP_instr(F64_numtype, MAX_binop_)
  ;; A-binary.watsup:548.5-548.31
  prod 0xA6 => BINOP_instr(F64_numtype, COPYSIGN_binop_)
  ;; A-binary.watsup:553.5-553.31
  prod 0xA7 => CVTOP_instr(I32_numtype, I64_numtype, WRAP_cvtop__)
  ;; A-binary.watsup:554.5-554.36
  prod 0xA8 => CVTOP_instr(I32_numtype, F32_numtype, TRUNC_cvtop__(S_sx))
  ;; A-binary.watsup:555.5-555.36
  prod 0xA9 => CVTOP_instr(I32_numtype, F32_numtype, TRUNC_cvtop__(U_sx))
  ;; A-binary.watsup:556.5-556.36
  prod 0xAA => CVTOP_instr(I32_numtype, F64_numtype, TRUNC_cvtop__(S_sx))
  ;; A-binary.watsup:557.5-557.36
  prod 0xAB => CVTOP_instr(I32_numtype, F64_numtype, TRUNC_cvtop__(U_sx))
  ;; A-binary.watsup:558.5-558.37
  prod 0xAC => CVTOP_instr(I64_numtype, I32_numtype, EXTEND_cvtop__(S_sx))
  ;; A-binary.watsup:559.5-559.37
  prod 0xAD => CVTOP_instr(I64_numtype, I32_numtype, EXTEND_cvtop__(U_sx))
  ;; A-binary.watsup:560.5-560.36
  prod 0xAE => CVTOP_instr(I64_numtype, F32_numtype, TRUNC_cvtop__(S_sx))
  ;; A-binary.watsup:561.5-561.36
  prod 0xAF => CVTOP_instr(I64_numtype, F32_numtype, TRUNC_cvtop__(U_sx))
  ;; A-binary.watsup:562.5-562.36
  prod 0xB0 => CVTOP_instr(I64_numtype, F64_numtype, TRUNC_cvtop__(S_sx))
  ;; A-binary.watsup:563.5-563.36
  prod 0xB1 => CVTOP_instr(I64_numtype, F64_numtype, TRUNC_cvtop__(U_sx))
  ;; A-binary.watsup:564.5-564.38
  prod 0xB2 => CVTOP_instr(F32_numtype, I32_numtype, CONVERT_cvtop__(S_sx))
  ;; A-binary.watsup:565.5-565.38
  prod 0xB3 => CVTOP_instr(F32_numtype, I32_numtype, CONVERT_cvtop__(U_sx))
  ;; A-binary.watsup:566.5-566.38
  prod 0xB4 => CVTOP_instr(F32_numtype, I64_numtype, CONVERT_cvtop__(S_sx))
  ;; A-binary.watsup:567.5-567.38
  prod 0xB5 => CVTOP_instr(F32_numtype, I64_numtype, CONVERT_cvtop__(U_sx))
  ;; A-binary.watsup:568.5-568.33
  prod 0xB6 => CVTOP_instr(F32_numtype, F64_numtype, DEMOTE_cvtop__)
  ;; A-binary.watsup:569.5-569.38
  prod 0xB7 => CVTOP_instr(F64_numtype, I32_numtype, CONVERT_cvtop__(S_sx))
  ;; A-binary.watsup:570.5-570.38
  prod 0xB8 => CVTOP_instr(F64_numtype, I32_numtype, CONVERT_cvtop__(U_sx))
  ;; A-binary.watsup:571.5-571.38
  prod 0xB9 => CVTOP_instr(F64_numtype, I64_numtype, CONVERT_cvtop__(S_sx))
  ;; A-binary.watsup:572.5-572.38
  prod 0xBA => CVTOP_instr(F64_numtype, I64_numtype, CONVERT_cvtop__(U_sx))
  ;; A-binary.watsup:573.5-573.34
  prod 0xBB => CVTOP_instr(F32_numtype, F64_numtype, PROMOTE_cvtop__)
  ;; A-binary.watsup:574.5-574.38
  prod 0xBC => CVTOP_instr(I32_numtype, F32_numtype, REINTERPRET_cvtop__)
  ;; A-binary.watsup:575.5-575.38
  prod 0xBD => CVTOP_instr(I64_numtype, F64_numtype, REINTERPRET_cvtop__)
  ;; A-binary.watsup:576.5-576.38
  prod 0xBE => CVTOP_instr(F32_numtype, I32_numtype, REINTERPRET_cvtop__)
  ;; A-binary.watsup:577.5-577.38
  prod 0xBF => CVTOP_instr(F64_numtype, I64_numtype, REINTERPRET_cvtop__)
  ;; A-binary.watsup:581.5-581.47
  prod {0xFC `%`_u32(0):Bu32} => CVTOP_instr(I32_numtype, F32_numtype, TRUNC_SAT_cvtop__(S_sx))
  ;; A-binary.watsup:582.5-582.47
  prod {0xFC `%`_u32(1):Bu32} => CVTOP_instr(I32_numtype, F32_numtype, TRUNC_SAT_cvtop__(U_sx))
  ;; A-binary.watsup:583.5-583.47
  prod {0xFC `%`_u32(2):Bu32} => CVTOP_instr(I32_numtype, F64_numtype, TRUNC_SAT_cvtop__(S_sx))
  ;; A-binary.watsup:584.5-584.47
  prod {0xFC `%`_u32(3):Bu32} => CVTOP_instr(I32_numtype, F64_numtype, TRUNC_SAT_cvtop__(U_sx))
  ;; A-binary.watsup:585.5-585.47
  prod {0xFC `%`_u32(4):Bu32} => CVTOP_instr(I64_numtype, F32_numtype, TRUNC_SAT_cvtop__(S_sx))
  ;; A-binary.watsup:586.5-586.47
  prod {0xFC `%`_u32(5):Bu32} => CVTOP_instr(I64_numtype, F32_numtype, TRUNC_SAT_cvtop__(U_sx))
  ;; A-binary.watsup:587.5-587.47
  prod {0xFC `%`_u32(6):Bu32} => CVTOP_instr(I64_numtype, F64_numtype, TRUNC_SAT_cvtop__(S_sx))
  ;; A-binary.watsup:588.5-588.47
  prod {0xFC `%`_u32(7):Bu32} => CVTOP_instr(I64_numtype, F64_numtype, TRUNC_SAT_cvtop__(U_sx))
  ;; A-binary.watsup:598.5-598.50
  prod{x : idx, ao : memarg} {0xFD `%`_u32(0):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(), x, ao)
  ;; A-binary.watsup:599.5-599.70
  prod{x : idx, ao : memarg} {0xFD `%`_u32(1):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(`SHAPE%X%_%`_vloadop_(`%`_sz(8), 8, S_sx)), x, ao)
  ;; A-binary.watsup:600.5-600.70
  prod{x : idx, ao : memarg} {0xFD `%`_u32(2):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(`SHAPE%X%_%`_vloadop_(`%`_sz(8), 8, U_sx)), x, ao)
  ;; A-binary.watsup:601.5-601.71
  prod{x : idx, ao : memarg} {0xFD `%`_u32(3):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(`SHAPE%X%_%`_vloadop_(`%`_sz(16), 4, S_sx)), x, ao)
  ;; A-binary.watsup:602.5-602.71
  prod{x : idx, ao : memarg} {0xFD `%`_u32(4):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(`SHAPE%X%_%`_vloadop_(`%`_sz(16), 4, U_sx)), x, ao)
  ;; A-binary.watsup:603.5-603.71
  prod{x : idx, ao : memarg} {0xFD `%`_u32(5):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(`SHAPE%X%_%`_vloadop_(`%`_sz(32), 2, S_sx)), x, ao)
  ;; A-binary.watsup:604.5-604.71
  prod{x : idx, ao : memarg} {0xFD `%`_u32(6):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(`SHAPE%X%_%`_vloadop_(`%`_sz(32), 2, U_sx)), x, ao)
  ;; A-binary.watsup:605.5-605.61
  prod{x : idx, ao : memarg} {0xFD `%`_u32(7):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(SPLAT_vloadop_(`%`_sz(8))), x, ao)
  ;; A-binary.watsup:606.5-606.62
  prod{x : idx, ao : memarg} {0xFD `%`_u32(8):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(SPLAT_vloadop_(`%`_sz(16))), x, ao)
  ;; A-binary.watsup:607.5-607.62
  prod{x : idx, ao : memarg} {0xFD `%`_u32(9):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(SPLAT_vloadop_(`%`_sz(32))), x, ao)
  ;; A-binary.watsup:608.5-608.63
  prod{x : idx, ao : memarg} {0xFD `%`_u32(10):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(SPLAT_vloadop_(`%`_sz(64))), x, ao)
  ;; A-binary.watsup:609.5-609.52
  prod{x : idx, ao : memarg} {0xFD `%`_u32(11):Bu32 (x, ao):Bmemarg} => VSTORE_instr(V128_vectype, x, ao)
  ;; A-binary.watsup:610.5-610.72
  prod{x : idx, ao : memarg, l : labelidx} {0xFD `%`_u32(84):Bu32 (x, ao):Bmemarg `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VLOAD_LANE_instr(V128_vectype, `%`_sz(8), x, ao, `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:611.5-611.73
  prod{x : idx, ao : memarg, l : labelidx} {0xFD `%`_u32(85):Bu32 (x, ao):Bmemarg `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VLOAD_LANE_instr(V128_vectype, `%`_sz(16), x, ao, `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:612.5-612.73
  prod{x : idx, ao : memarg, l : labelidx} {0xFD `%`_u32(86):Bu32 (x, ao):Bmemarg `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VLOAD_LANE_instr(V128_vectype, `%`_sz(32), x, ao, `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:613.5-613.73
  prod{x : idx, ao : memarg, l : labelidx} {0xFD `%`_u32(87):Bu32 (x, ao):Bmemarg `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VLOAD_LANE_instr(V128_vectype, `%`_sz(64), x, ao, `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:614.5-614.73
  prod{x : idx, ao : memarg, l : labelidx} {0xFD `%`_u32(88):Bu32 (x, ao):Bmemarg `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VSTORE_LANE_instr(V128_vectype, `%`_sz(8), x, ao, `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:615.5-615.74
  prod{x : idx, ao : memarg, l : labelidx} {0xFD `%`_u32(89):Bu32 (x, ao):Bmemarg `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VSTORE_LANE_instr(V128_vectype, `%`_sz(16), x, ao, `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:616.5-616.74
  prod{x : idx, ao : memarg, l : labelidx} {0xFD `%`_u32(90):Bu32 (x, ao):Bmemarg `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VSTORE_LANE_instr(V128_vectype, `%`_sz(32), x, ao, `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:617.5-617.74
  prod{x : idx, ao : memarg, l : labelidx} {0xFD `%`_u32(91):Bu32 (x, ao):Bmemarg `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VSTORE_LANE_instr(V128_vectype, `%`_sz(64), x, ao, `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:618.5-618.62
  prod{x : idx, ao : memarg} {0xFD `%`_u32(92):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(ZERO_vloadop_(`%`_sz(32))), x, ao)
  ;; A-binary.watsup:619.5-619.62
  prod{x : idx, ao : memarg} {0xFD `%`_u32(93):Bu32 (x, ao):Bmemarg} => VLOAD_instr(V128_vectype, ?(ZERO_vloadop_(`%`_sz(64))), x, ao)
  ;; A-binary.watsup:623.5-623.71
  prod{`b*` : byte*} {0xFD `%`_u32(12):Bu32 b:Bbyte^16{b <- `b*`}} => VCONST_instr(V128_vectype, $invibytes_(128, b^16{b <- `b*`}))
  ;; A-binary.watsup:627.5-627.61
  prod{`l*` : labelidx*} {0xFD `%`_u32(13):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx^16{l <- `l*`}} => VSHUFFLE_instr(`%`_bshape(`%X%`_shape(I8_lanetype, `%`_dim(16))), `%`_laneidx(l!`%`_labelidx.0)^16{l <- `l*`})
  ;; A-binary.watsup:628.5-628.49
  prod {0xFD `%`_u32(14):Bu32} => VSWIZZLOP_instr(`%`_bshape(`%X%`_shape(I8_lanetype, `%`_dim(16))), SWIZZLE_vswizzlop_)
  ;; A-binary.watsup:629.5-629.58
  prod {0xFD `%`_u32(256):Bu32} => VSWIZZLOP_instr(`%`_bshape(`%X%`_shape(I8_lanetype, `%`_dim(16))), RELAXED_SWIZZLE_vswizzlop_)
  ;; A-binary.watsup:633.5-633.38
  prod {0xFD `%`_u32(15):Bu32} => VSPLAT_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)))
  ;; A-binary.watsup:634.5-634.38
  prod {0xFD `%`_u32(16):Bu32} => VSPLAT_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)))
  ;; A-binary.watsup:635.5-635.38
  prod {0xFD `%`_u32(17):Bu32} => VSPLAT_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)))
  ;; A-binary.watsup:636.5-636.38
  prod {0xFD `%`_u32(18):Bu32} => VSPLAT_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)))
  ;; A-binary.watsup:637.5-637.38
  prod {0xFD `%`_u32(19):Bu32} => VSPLAT_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)))
  ;; A-binary.watsup:638.5-638.38
  prod {0xFD `%`_u32(20):Bu32} => VSPLAT_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)))
  ;; A-binary.watsup:642.5-642.60
  prod{l : labelidx} {0xFD `%`_u32(21):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VEXTRACT_LANE_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), ?(S_sx), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:643.5-643.60
  prod{l : labelidx} {0xFD `%`_u32(22):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VEXTRACT_LANE_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), ?(U_sx), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:644.5-644.58
  prod{l : labelidx} {0xFD `%`_u32(23):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VREPLACE_LANE_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:645.5-645.60
  prod{l : labelidx} {0xFD `%`_u32(24):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VEXTRACT_LANE_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), ?(S_sx), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:646.5-646.60
  prod{l : labelidx} {0xFD `%`_u32(25):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VEXTRACT_LANE_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), ?(U_sx), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:647.5-647.58
  prod{l : labelidx} {0xFD `%`_u32(26):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VREPLACE_LANE_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:648.5-648.58
  prod{l : labelidx} {0xFD `%`_u32(27):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VEXTRACT_LANE_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), ?(), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:649.5-649.58
  prod{l : labelidx} {0xFD `%`_u32(28):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VREPLACE_LANE_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:650.5-650.58
  prod{l : labelidx} {0xFD `%`_u32(29):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VEXTRACT_LANE_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), ?(), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:651.5-651.58
  prod{l : labelidx} {0xFD `%`_u32(30):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VREPLACE_LANE_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:652.5-652.58
  prod{l : labelidx} {0xFD `%`_u32(31):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VEXTRACT_LANE_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), ?(), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:653.5-653.58
  prod{l : labelidx} {0xFD `%`_u32(32):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VREPLACE_LANE_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:654.5-654.58
  prod{l : labelidx} {0xFD `%`_u32(33):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VEXTRACT_LANE_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), ?(), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:655.5-655.58
  prod{l : labelidx} {0xFD `%`_u32(34):Bu32 `%`_laneidx(l!`%`_labelidx.0):Blaneidx} => VREPLACE_LANE_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), `%`_laneidx(l!`%`_labelidx.0))
  ;; A-binary.watsup:659.5-659.41
  prod {0xFD `%`_u32(35):Bu32} => VRELOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), EQ_vrelop_)
  ;; A-binary.watsup:660.5-660.41
  prod {0xFD `%`_u32(36):Bu32} => VRELOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), NE_vrelop_)
  ;; A-binary.watsup:661.5-661.45
  prod {0xFD `%`_u32(37):Bu32} => VRELOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), LT_vrelop_(S_sx))
  ;; A-binary.watsup:662.5-662.45
  prod {0xFD `%`_u32(38):Bu32} => VRELOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), LT_vrelop_(U_sx))
  ;; A-binary.watsup:663.5-663.45
  prod {0xFD `%`_u32(39):Bu32} => VRELOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), GT_vrelop_(S_sx))
  ;; A-binary.watsup:664.5-664.45
  prod {0xFD `%`_u32(40):Bu32} => VRELOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), GT_vrelop_(U_sx))
  ;; A-binary.watsup:665.5-665.45
  prod {0xFD `%`_u32(41):Bu32} => VRELOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), LE_vrelop_(S_sx))
  ;; A-binary.watsup:666.5-666.45
  prod {0xFD `%`_u32(42):Bu32} => VRELOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), LE_vrelop_(U_sx))
  ;; A-binary.watsup:667.5-667.45
  prod {0xFD `%`_u32(43):Bu32} => VRELOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), GE_vrelop_(S_sx))
  ;; A-binary.watsup:668.5-668.45
  prod {0xFD `%`_u32(44):Bu32} => VRELOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), GE_vrelop_(U_sx))
  ;; A-binary.watsup:672.5-672.41
  prod {0xFD `%`_u32(45):Bu32} => VRELOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), EQ_vrelop_)
  ;; A-binary.watsup:673.5-673.41
  prod {0xFD `%`_u32(46):Bu32} => VRELOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), NE_vrelop_)
  ;; A-binary.watsup:674.5-674.45
  prod {0xFD `%`_u32(47):Bu32} => VRELOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), LT_vrelop_(S_sx))
  ;; A-binary.watsup:675.5-675.45
  prod {0xFD `%`_u32(48):Bu32} => VRELOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), LT_vrelop_(U_sx))
  ;; A-binary.watsup:676.5-676.45
  prod {0xFD `%`_u32(49):Bu32} => VRELOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), GT_vrelop_(S_sx))
  ;; A-binary.watsup:677.5-677.45
  prod {0xFD `%`_u32(50):Bu32} => VRELOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), GT_vrelop_(U_sx))
  ;; A-binary.watsup:678.5-678.45
  prod {0xFD `%`_u32(51):Bu32} => VRELOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), LE_vrelop_(S_sx))
  ;; A-binary.watsup:679.5-679.45
  prod {0xFD `%`_u32(52):Bu32} => VRELOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), LE_vrelop_(U_sx))
  ;; A-binary.watsup:680.5-680.45
  prod {0xFD `%`_u32(53):Bu32} => VRELOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), GE_vrelop_(S_sx))
  ;; A-binary.watsup:681.5-681.45
  prod {0xFD `%`_u32(54):Bu32} => VRELOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), GE_vrelop_(U_sx))
  ;; A-binary.watsup:685.5-685.41
  prod {0xFD `%`_u32(55):Bu32} => VRELOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), EQ_vrelop_)
  ;; A-binary.watsup:686.5-686.41
  prod {0xFD `%`_u32(56):Bu32} => VRELOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), NE_vrelop_)
  ;; A-binary.watsup:687.5-687.45
  prod {0xFD `%`_u32(57):Bu32} => VRELOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), LT_vrelop_(S_sx))
  ;; A-binary.watsup:688.5-688.45
  prod {0xFD `%`_u32(58):Bu32} => VRELOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), LT_vrelop_(U_sx))
  ;; A-binary.watsup:689.5-689.45
  prod {0xFD `%`_u32(59):Bu32} => VRELOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), GT_vrelop_(S_sx))
  ;; A-binary.watsup:690.5-690.45
  prod {0xFD `%`_u32(60):Bu32} => VRELOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), GT_vrelop_(U_sx))
  ;; A-binary.watsup:691.5-691.45
  prod {0xFD `%`_u32(61):Bu32} => VRELOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), LE_vrelop_(S_sx))
  ;; A-binary.watsup:692.5-692.45
  prod {0xFD `%`_u32(62):Bu32} => VRELOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), LE_vrelop_(U_sx))
  ;; A-binary.watsup:693.5-693.45
  prod {0xFD `%`_u32(63):Bu32} => VRELOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), GE_vrelop_(S_sx))
  ;; A-binary.watsup:694.5-694.45
  prod {0xFD `%`_u32(64):Bu32} => VRELOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), GE_vrelop_(U_sx))
  ;; A-binary.watsup:698.5-698.41
  prod {0xFD `%`_u32(65):Bu32} => VRELOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), EQ_vrelop_)
  ;; A-binary.watsup:699.5-699.41
  prod {0xFD `%`_u32(66):Bu32} => VRELOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), NE_vrelop_)
  ;; A-binary.watsup:700.5-700.41
  prod {0xFD `%`_u32(67):Bu32} => VRELOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), LT_vrelop_)
  ;; A-binary.watsup:701.5-701.41
  prod {0xFD `%`_u32(68):Bu32} => VRELOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), GT_vrelop_)
  ;; A-binary.watsup:702.5-702.41
  prod {0xFD `%`_u32(69):Bu32} => VRELOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), LE_vrelop_)
  ;; A-binary.watsup:703.5-703.41
  prod {0xFD `%`_u32(70):Bu32} => VRELOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), GE_vrelop_)
  ;; A-binary.watsup:707.5-707.41
  prod {0xFD `%`_u32(71):Bu32} => VRELOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), EQ_vrelop_)
  ;; A-binary.watsup:708.5-708.41
  prod {0xFD `%`_u32(72):Bu32} => VRELOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), NE_vrelop_)
  ;; A-binary.watsup:709.5-709.41
  prod {0xFD `%`_u32(73):Bu32} => VRELOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), LT_vrelop_)
  ;; A-binary.watsup:710.5-710.41
  prod {0xFD `%`_u32(74):Bu32} => VRELOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), GT_vrelop_)
  ;; A-binary.watsup:711.5-711.41
  prod {0xFD `%`_u32(75):Bu32} => VRELOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), LE_vrelop_)
  ;; A-binary.watsup:712.5-712.41
  prod {0xFD `%`_u32(76):Bu32} => VRELOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), GE_vrelop_)
  ;; A-binary.watsup:716.5-716.36
  prod {0xFD `%`_u32(77):Bu32} => VVUNOP_instr(V128_vectype, NOT_vvunop)
  ;; A-binary.watsup:720.5-720.37
  prod {0xFD `%`_u32(78):Bu32} => VVBINOP_instr(V128_vectype, AND_vvbinop)
  ;; A-binary.watsup:721.5-721.40
  prod {0xFD `%`_u32(79):Bu32} => VVBINOP_instr(V128_vectype, ANDNOT_vvbinop)
  ;; A-binary.watsup:722.5-722.36
  prod {0xFD `%`_u32(80):Bu32} => VVBINOP_instr(V128_vectype, OR_vvbinop)
  ;; A-binary.watsup:723.5-723.37
  prod {0xFD `%`_u32(81):Bu32} => VVBINOP_instr(V128_vectype, XOR_vvbinop)
  ;; A-binary.watsup:727.5-727.44
  prod {0xFD `%`_u32(82):Bu32} => VVTERNOP_instr(V128_vectype, BITSELECT_vvternop)
  ;; A-binary.watsup:731.5-731.43
  prod {0xFD `%`_u32(83):Bu32} => VVTESTOP_instr(V128_vectype, ANY_TRUE_vvtestop)
  ;; A-binary.watsup:735.5-735.41
  prod {0xFD `%`_u32(96):Bu32} => VUNOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), ABS_vunop_)
  ;; A-binary.watsup:736.5-736.41
  prod {0xFD `%`_u32(97):Bu32} => VUNOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), NEG_vunop_)
  ;; A-binary.watsup:737.5-737.44
  prod {0xFD `%`_u32(98):Bu32} => VUNOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), POPCNT_vunop_)
  ;; A-binary.watsup:741.5-741.48
  prod {0xFD `%`_u32(99):Bu32} => VTESTOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), ALL_TRUE_vtestop_)
  ;; A-binary.watsup:745.5-745.41
  prod {0xFD `%`_u32(100):Bu32} => VBITMASK_instr(`%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))))
  ;; A-binary.watsup:749.5-749.53
  prod {0xFD `%`_u32(101):Bu32} => VNARROW_instr(`%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), `%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), S_sx)
  ;; A-binary.watsup:750.5-750.53
  prod {0xFD `%`_u32(102):Bu32} => VNARROW_instr(`%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), `%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), U_sx)
  ;; A-binary.watsup:754.5-754.45
  prod {0xFD `%`_u32(107):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), SHL_vshiftop_)
  ;; A-binary.watsup:755.5-755.49
  prod {0xFD `%`_u32(108):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), SHR_vshiftop_(S_sx))
  ;; A-binary.watsup:756.5-756.49
  prod {0xFD `%`_u32(109):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), SHR_vshiftop_(U_sx))
  ;; A-binary.watsup:760.5-760.43
  prod {0xFD `%`_u32(110):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), ADD_vbinop_)
  ;; A-binary.watsup:761.5-761.51
  prod {0xFD `%`_u32(111):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), ADD_SAT_vbinop_(S_sx))
  ;; A-binary.watsup:762.5-762.51
  prod {0xFD `%`_u32(112):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), ADD_SAT_vbinop_(U_sx))
  ;; A-binary.watsup:763.5-763.43
  prod {0xFD `%`_u32(113):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), SUB_vbinop_)
  ;; A-binary.watsup:764.5-764.51
  prod {0xFD `%`_u32(114):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), SUB_SAT_vbinop_(S_sx))
  ;; A-binary.watsup:765.5-765.51
  prod {0xFD `%`_u32(115):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), SUB_SAT_vbinop_(U_sx))
  ;; A-binary.watsup:766.5-766.47
  prod {0xFD `%`_u32(118):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), MIN_vbinop_(S_sx))
  ;; A-binary.watsup:767.5-767.47
  prod {0xFD `%`_u32(119):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), MIN_vbinop_(U_sx))
  ;; A-binary.watsup:768.5-768.47
  prod {0xFD `%`_u32(120):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), MAX_vbinop_(S_sx))
  ;; A-binary.watsup:769.5-769.47
  prod {0xFD `%`_u32(121):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), MAX_vbinop_(U_sx))
  ;; A-binary.watsup:770.5-770.48
  prod {0xFD `%`_u32(123):Bu32} => VBINOP_instr(`%X%`_shape(I8_lanetype, `%`_dim(16)), `AVGRU`_vbinop_)
  ;; A-binary.watsup:774.5-774.72
  prod {0xFD `%`_u32(124):Bu32} => VEXTUNOP_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), EXTADD_PAIRWISE_vextunop__(S_sx))
  ;; A-binary.watsup:775.5-775.72
  prod {0xFD `%`_u32(125):Bu32} => VEXTUNOP_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), EXTADD_PAIRWISE_vextunop__(U_sx))
  ;; A-binary.watsup:779.5-779.42
  prod {0xFD `%`_u32(128):Bu32} => VUNOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), ABS_vunop_)
  ;; A-binary.watsup:780.5-780.42
  prod {0xFD `%`_u32(129):Bu32} => VUNOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), NEG_vunop_)
  ;; A-binary.watsup:784.5-784.55
  prod {0xFD `%`_u32(130):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), `Q15MULR_SATS`_vbinop_)
  ;; A-binary.watsup:785.5-785.59
  prod {0xFD `%`_u32(273):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), `RELAXED_Q15MULRS`_vbinop_)
  ;; A-binary.watsup:789.5-789.49
  prod {0xFD `%`_u32(131):Bu32} => VTESTOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), ALL_TRUE_vtestop_)
  ;; A-binary.watsup:793.5-793.41
  prod {0xFD `%`_u32(132):Bu32} => VBITMASK_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))))
  ;; A-binary.watsup:797.5-797.53
  prod {0xFD `%`_u32(133):Bu32} => VNARROW_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), S_sx)
  ;; A-binary.watsup:798.5-798.53
  prod {0xFD `%`_u32(134):Bu32} => VNARROW_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), U_sx)
  ;; A-binary.watsup:802.5-802.65
  prod {0xFD `%`_u32(135):Bu32} => VCVTOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), `%X%`_shape(I8_lanetype, `%`_dim(16)), EXTEND_vcvtop__(S_sx), ?(LOW_half__), ?())
  ;; A-binary.watsup:803.5-803.66
  prod {0xFD `%`_u32(136):Bu32} => VCVTOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), `%X%`_shape(I8_lanetype, `%`_dim(16)), EXTEND_vcvtop__(S_sx), ?(HIGH_half__), ?())
  ;; A-binary.watsup:804.5-804.65
  prod {0xFD `%`_u32(137):Bu32} => VCVTOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), `%X%`_shape(I8_lanetype, `%`_dim(16)), EXTEND_vcvtop__(U_sx), ?(LOW_half__), ?())
  ;; A-binary.watsup:805.5-805.66
  prod {0xFD `%`_u32(138):Bu32} => VCVTOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), `%X%`_shape(I8_lanetype, `%`_dim(16)), EXTEND_vcvtop__(U_sx), ?(HIGH_half__), ?())
  ;; A-binary.watsup:809.5-809.45
  prod {0xFD `%`_u32(139):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), SHL_vshiftop_)
  ;; A-binary.watsup:810.5-810.49
  prod {0xFD `%`_u32(140):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), SHR_vshiftop_(S_sx))
  ;; A-binary.watsup:811.5-811.49
  prod {0xFD `%`_u32(141):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), SHR_vshiftop_(U_sx))
  ;; A-binary.watsup:815.5-815.43
  prod {0xFD `%`_u32(142):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), ADD_vbinop_)
  ;; A-binary.watsup:816.5-816.51
  prod {0xFD `%`_u32(143):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), ADD_SAT_vbinop_(S_sx))
  ;; A-binary.watsup:817.5-817.51
  prod {0xFD `%`_u32(144):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), ADD_SAT_vbinop_(U_sx))
  ;; A-binary.watsup:818.5-818.43
  prod {0xFD `%`_u32(145):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), SUB_vbinop_)
  ;; A-binary.watsup:819.5-819.51
  prod {0xFD `%`_u32(146):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), SUB_SAT_vbinop_(S_sx))
  ;; A-binary.watsup:820.5-820.51
  prod {0xFD `%`_u32(147):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), SUB_SAT_vbinop_(U_sx))
  ;; A-binary.watsup:821.5-821.43
  prod {0xFD `%`_u32(149):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), MUL_vbinop_)
  ;; A-binary.watsup:822.5-822.47
  prod {0xFD `%`_u32(150):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), MIN_vbinop_(S_sx))
  ;; A-binary.watsup:823.5-823.47
  prod {0xFD `%`_u32(151):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), MIN_vbinop_(U_sx))
  ;; A-binary.watsup:824.5-824.47
  prod {0xFD `%`_u32(152):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), MAX_vbinop_(S_sx))
  ;; A-binary.watsup:825.5-825.47
  prod {0xFD `%`_u32(153):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), MAX_vbinop_(U_sx))
  ;; A-binary.watsup:826.5-826.48
  prod {0xFD `%`_u32(155):Bu32} => VBINOP_instr(`%X%`_shape(I16_lanetype, `%`_dim(8)), `AVGRU`_vbinop_)
  ;; A-binary.watsup:830.5-830.68
  prod {0xFD `%`_u32(156):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), EXTMUL_vextbinop__(S_sx, LOW_half__))
  ;; A-binary.watsup:831.5-831.69
  prod {0xFD `%`_u32(157):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), EXTMUL_vextbinop__(S_sx, HIGH_half__))
  ;; A-binary.watsup:832.5-832.68
  prod {0xFD `%`_u32(158):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), EXTMUL_vextbinop__(U_sx, LOW_half__))
  ;; A-binary.watsup:833.5-833.69
  prod {0xFD `%`_u32(159):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), EXTMUL_vextbinop__(U_sx, HIGH_half__))
  ;; A-binary.watsup:834.5-834.69
  prod {0xFD `%`_u32(274):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `%`_ishape(`%X%`_shape(I8_lanetype, `%`_dim(16))), `RELAXED_DOTS`_vextbinop__)
  ;; A-binary.watsup:838.5-838.72
  prod {0xFD `%`_u32(126):Bu32} => VEXTUNOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), `%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), EXTADD_PAIRWISE_vextunop__(S_sx))
  ;; A-binary.watsup:839.5-839.72
  prod {0xFD `%`_u32(127):Bu32} => VEXTUNOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), `%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), EXTADD_PAIRWISE_vextunop__(U_sx))
  ;; A-binary.watsup:843.5-843.42
  prod {0xFD `%`_u32(160):Bu32} => VUNOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), ABS_vunop_)
  ;; A-binary.watsup:844.5-844.42
  prod {0xFD `%`_u32(161):Bu32} => VUNOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), NEG_vunop_)
  ;; A-binary.watsup:848.5-848.49
  prod {0xFD `%`_u32(163):Bu32} => VTESTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), ALL_TRUE_vtestop_)
  ;; A-binary.watsup:852.5-852.41
  prod {0xFD `%`_u32(164):Bu32} => VBITMASK_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))))
  ;; A-binary.watsup:856.5-856.65
  prod {0xFD `%`_u32(167):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(I16_lanetype, `%`_dim(8)), EXTEND_vcvtop__(S_sx), ?(LOW_half__), ?())
  ;; A-binary.watsup:857.5-857.66
  prod {0xFD `%`_u32(168):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(I16_lanetype, `%`_dim(8)), EXTEND_vcvtop__(S_sx), ?(HIGH_half__), ?())
  ;; A-binary.watsup:858.5-858.65
  prod {0xFD `%`_u32(169):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(I16_lanetype, `%`_dim(8)), EXTEND_vcvtop__(U_sx), ?(LOW_half__), ?())
  ;; A-binary.watsup:859.5-859.66
  prod {0xFD `%`_u32(170):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(I16_lanetype, `%`_dim(8)), EXTEND_vcvtop__(U_sx), ?(HIGH_half__), ?())
  ;; A-binary.watsup:863.5-863.45
  prod {0xFD `%`_u32(171):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), SHL_vshiftop_)
  ;; A-binary.watsup:864.5-864.49
  prod {0xFD `%`_u32(172):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), SHR_vshiftop_(S_sx))
  ;; A-binary.watsup:865.5-865.49
  prod {0xFD `%`_u32(173):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), SHR_vshiftop_(U_sx))
  ;; A-binary.watsup:869.5-869.43
  prod {0xFD `%`_u32(174):Bu32} => VBINOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), ADD_vbinop_)
  ;; A-binary.watsup:870.5-870.43
  prod {0xFD `%`_u32(177):Bu32} => VBINOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), SUB_vbinop_)
  ;; A-binary.watsup:871.5-871.43
  prod {0xFD `%`_u32(181):Bu32} => VBINOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), MUL_vbinop_)
  ;; A-binary.watsup:872.5-872.47
  prod {0xFD `%`_u32(182):Bu32} => VBINOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), MIN_vbinop_(S_sx))
  ;; A-binary.watsup:873.5-873.47
  prod {0xFD `%`_u32(183):Bu32} => VBINOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), MIN_vbinop_(U_sx))
  ;; A-binary.watsup:874.5-874.47
  prod {0xFD `%`_u32(184):Bu32} => VBINOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), MAX_vbinop_(S_sx))
  ;; A-binary.watsup:875.5-875.47
  prod {0xFD `%`_u32(185):Bu32} => VBINOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), MAX_vbinop_(U_sx))
  ;; A-binary.watsup:879.5-879.61
  prod {0xFD `%`_u32(186):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), `%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `DOTS`_vextbinop__)
  ;; A-binary.watsup:880.5-880.68
  prod {0xFD `%`_u32(188):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), `%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), EXTMUL_vextbinop__(S_sx, LOW_half__))
  ;; A-binary.watsup:881.5-881.69
  prod {0xFD `%`_u32(189):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), `%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), EXTMUL_vextbinop__(S_sx, HIGH_half__))
  ;; A-binary.watsup:882.5-882.68
  prod {0xFD `%`_u32(190):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), `%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), EXTMUL_vextbinop__(U_sx, LOW_half__))
  ;; A-binary.watsup:883.5-883.69
  prod {0xFD `%`_u32(191):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), `%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), EXTMUL_vextbinop__(U_sx, HIGH_half__))
  ;; A-binary.watsup:887.5-887.74
  prod {0xFD `%`_u32(275):Bu32} => VEXTTERNOP_instr(`%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), `%`_ishape(`%X%`_shape(I16_lanetype, `%`_dim(8))), `RELAXED_DOT_ADDS`_vextternop__)
  ;; A-binary.watsup:891.5-891.42
  prod {0xFD `%`_u32(192):Bu32} => VUNOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), ABS_vunop_)
  ;; A-binary.watsup:892.5-892.42
  prod {0xFD `%`_u32(193):Bu32} => VUNOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), NEG_vunop_)
  ;; A-binary.watsup:896.5-896.49
  prod {0xFD `%`_u32(195):Bu32} => VTESTOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), ALL_TRUE_vtestop_)
  ;; A-binary.watsup:900.5-900.41
  prod {0xFD `%`_u32(196):Bu32} => VBITMASK_instr(`%`_ishape(`%X%`_shape(I64_lanetype, `%`_dim(2))))
  ;; A-binary.watsup:904.5-904.65
  prod {0xFD `%`_u32(199):Bu32} => VCVTOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), `%X%`_shape(I32_lanetype, `%`_dim(4)), EXTEND_vcvtop__(S_sx), ?(LOW_half__), ?())
  ;; A-binary.watsup:905.5-905.66
  prod {0xFD `%`_u32(200):Bu32} => VCVTOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), `%X%`_shape(I32_lanetype, `%`_dim(4)), EXTEND_vcvtop__(S_sx), ?(HIGH_half__), ?())
  ;; A-binary.watsup:906.5-906.65
  prod {0xFD `%`_u32(201):Bu32} => VCVTOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), `%X%`_shape(I32_lanetype, `%`_dim(4)), EXTEND_vcvtop__(U_sx), ?(LOW_half__), ?())
  ;; A-binary.watsup:907.5-907.66
  prod {0xFD `%`_u32(202):Bu32} => VCVTOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), `%X%`_shape(I32_lanetype, `%`_dim(4)), EXTEND_vcvtop__(U_sx), ?(HIGH_half__), ?())
  ;; A-binary.watsup:911.5-911.45
  prod {0xFD `%`_u32(203):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I64_lanetype, `%`_dim(2))), SHL_vshiftop_)
  ;; A-binary.watsup:912.5-912.49
  prod {0xFD `%`_u32(204):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I64_lanetype, `%`_dim(2))), SHR_vshiftop_(S_sx))
  ;; A-binary.watsup:913.5-913.49
  prod {0xFD `%`_u32(205):Bu32} => VSHIFTOP_instr(`%`_ishape(`%X%`_shape(I64_lanetype, `%`_dim(2))), SHR_vshiftop_(U_sx))
  ;; A-binary.watsup:917.5-917.43
  prod {0xFD `%`_u32(206):Bu32} => VBINOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), ADD_vbinop_)
  ;; A-binary.watsup:918.5-918.43
  prod {0xFD `%`_u32(209):Bu32} => VBINOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), SUB_vbinop_)
  ;; A-binary.watsup:919.5-919.43
  prod {0xFD `%`_u32(213):Bu32} => VBINOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), MUL_vbinop_)
  ;; A-binary.watsup:923.5-923.42
  prod {0xFD `%`_u32(214):Bu32} => VRELOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), EQ_vrelop_)
  ;; A-binary.watsup:924.5-924.42
  prod {0xFD `%`_u32(215):Bu32} => VRELOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), NE_vrelop_)
  ;; A-binary.watsup:925.5-925.46
  prod {0xFD `%`_u32(216):Bu32} => VRELOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), LT_vrelop_(S_sx))
  ;; A-binary.watsup:926.5-926.46
  prod {0xFD `%`_u32(217):Bu32} => VRELOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), GT_vrelop_(S_sx))
  ;; A-binary.watsup:927.5-927.46
  prod {0xFD `%`_u32(218):Bu32} => VRELOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), LE_vrelop_(S_sx))
  ;; A-binary.watsup:928.5-928.46
  prod {0xFD `%`_u32(219):Bu32} => VRELOP_instr(`%X%`_shape(I64_lanetype, `%`_dim(2)), GE_vrelop_(S_sx))
  ;; A-binary.watsup:932.5-932.68
  prod {0xFD `%`_u32(220):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I64_lanetype, `%`_dim(2))), `%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), EXTMUL_vextbinop__(S_sx, LOW_half__))
  ;; A-binary.watsup:933.5-933.69
  prod {0xFD `%`_u32(221):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I64_lanetype, `%`_dim(2))), `%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), EXTMUL_vextbinop__(S_sx, HIGH_half__))
  ;; A-binary.watsup:934.5-934.68
  prod {0xFD `%`_u32(222):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I64_lanetype, `%`_dim(2))), `%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), EXTMUL_vextbinop__(U_sx, LOW_half__))
  ;; A-binary.watsup:935.5-935.69
  prod {0xFD `%`_u32(223):Bu32} => VEXTBINOP_instr(`%`_ishape(`%X%`_shape(I64_lanetype, `%`_dim(2))), `%`_ishape(`%X%`_shape(I32_lanetype, `%`_dim(4))), EXTMUL_vextbinop__(U_sx, HIGH_half__))
  ;; A-binary.watsup:939.5-939.43
  prod {0xFD `%`_u32(103):Bu32} => VUNOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), CEIL_vunop_)
  ;; A-binary.watsup:940.5-940.44
  prod {0xFD `%`_u32(104):Bu32} => VUNOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), FLOOR_vunop_)
  ;; A-binary.watsup:941.5-941.44
  prod {0xFD `%`_u32(105):Bu32} => VUNOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), TRUNC_vunop_)
  ;; A-binary.watsup:942.5-942.46
  prod {0xFD `%`_u32(106):Bu32} => VUNOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), NEAREST_vunop_)
  ;; A-binary.watsup:943.5-943.42
  prod {0xFD `%`_u32(224):Bu32} => VUNOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), ABS_vunop_)
  ;; A-binary.watsup:944.5-944.42
  prod {0xFD `%`_u32(225):Bu32} => VUNOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), NEG_vunop_)
  ;; A-binary.watsup:945.5-945.43
  prod {0xFD `%`_u32(227):Bu32} => VUNOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), SQRT_vunop_)
  ;; A-binary.watsup:949.5-949.43
  prod {0xFD `%`_u32(228):Bu32} => VBINOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), ADD_vbinop_)
  ;; A-binary.watsup:950.5-950.43
  prod {0xFD `%`_u32(229):Bu32} => VBINOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), SUB_vbinop_)
  ;; A-binary.watsup:951.5-951.43
  prod {0xFD `%`_u32(230):Bu32} => VBINOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), MUL_vbinop_)
  ;; A-binary.watsup:952.5-952.43
  prod {0xFD `%`_u32(231):Bu32} => VBINOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), DIV_vbinop_)
  ;; A-binary.watsup:953.5-953.43
  prod {0xFD `%`_u32(232):Bu32} => VBINOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), MIN_vbinop_)
  ;; A-binary.watsup:954.5-954.43
  prod {0xFD `%`_u32(233):Bu32} => VBINOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), MAX_vbinop_)
  ;; A-binary.watsup:955.5-955.44
  prod {0xFD `%`_u32(234):Bu32} => VBINOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), PMIN_vbinop_)
  ;; A-binary.watsup:956.5-956.44
  prod {0xFD `%`_u32(235):Bu32} => VBINOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), PMAX_vbinop_)
  ;; A-binary.watsup:957.5-957.51
  prod {0xFD `%`_u32(269):Bu32} => VBINOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), RELAXED_MIN_vbinop_)
  ;; A-binary.watsup:958.5-958.51
  prod {0xFD `%`_u32(270):Bu32} => VBINOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), RELAXED_MAX_vbinop_)
  ;; A-binary.watsup:962.5-962.53
  prod {0xFD `%`_u32(261):Bu32} => VTERNOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), RELAXED_MADD_vternop_)
  ;; A-binary.watsup:963.5-963.54
  prod {0xFD `%`_u32(262):Bu32} => VTERNOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), RELAXED_NMADD_vternop_)
  ;; A-binary.watsup:967.5-967.43
  prod {0xFD `%`_u32(116):Bu32} => VUNOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), CEIL_vunop_)
  ;; A-binary.watsup:968.5-968.44
  prod {0xFD `%`_u32(117):Bu32} => VUNOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), FLOOR_vunop_)
  ;; A-binary.watsup:969.5-969.44
  prod {0xFD `%`_u32(122):Bu32} => VUNOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), TRUNC_vunop_)
  ;; A-binary.watsup:970.5-970.46
  prod {0xFD `%`_u32(148):Bu32} => VUNOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), NEAREST_vunop_)
  ;; A-binary.watsup:971.5-971.42
  prod {0xFD `%`_u32(236):Bu32} => VUNOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), ABS_vunop_)
  ;; A-binary.watsup:972.5-972.42
  prod {0xFD `%`_u32(237):Bu32} => VUNOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), NEG_vunop_)
  ;; A-binary.watsup:973.5-973.43
  prod {0xFD `%`_u32(239):Bu32} => VUNOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), SQRT_vunop_)
  ;; A-binary.watsup:977.5-977.43
  prod {0xFD `%`_u32(240):Bu32} => VBINOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), ADD_vbinop_)
  ;; A-binary.watsup:978.5-978.43
  prod {0xFD `%`_u32(241):Bu32} => VBINOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), SUB_vbinop_)
  ;; A-binary.watsup:979.5-979.43
  prod {0xFD `%`_u32(242):Bu32} => VBINOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), MUL_vbinop_)
  ;; A-binary.watsup:980.5-980.43
  prod {0xFD `%`_u32(243):Bu32} => VBINOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), DIV_vbinop_)
  ;; A-binary.watsup:981.5-981.43
  prod {0xFD `%`_u32(244):Bu32} => VBINOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), MIN_vbinop_)
  ;; A-binary.watsup:982.5-982.43
  prod {0xFD `%`_u32(245):Bu32} => VBINOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), MAX_vbinop_)
  ;; A-binary.watsup:983.5-983.44
  prod {0xFD `%`_u32(246):Bu32} => VBINOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), PMIN_vbinop_)
  ;; A-binary.watsup:984.5-984.44
  prod {0xFD `%`_u32(247):Bu32} => VBINOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), PMAX_vbinop_)
  ;; A-binary.watsup:985.5-985.51
  prod {0xFD `%`_u32(271):Bu32} => VBINOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), RELAXED_MIN_vbinop_)
  ;; A-binary.watsup:986.5-986.51
  prod {0xFD `%`_u32(272):Bu32} => VBINOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), RELAXED_MAX_vbinop_)
  ;; A-binary.watsup:990.5-990.53
  prod {0xFD `%`_u32(263):Bu32} => VTERNOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), RELAXED_MADD_vternop_)
  ;; A-binary.watsup:991.5-991.54
  prod {0xFD `%`_u32(264):Bu32} => VTERNOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), RELAXED_NMADD_vternop_)
  ;; A-binary.watsup:995.5-995.61
  prod {0xFD `%`_u32(94):Bu32} => VCVTOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), `%X%`_shape(F64_lanetype, `%`_dim(2)), DEMOTE_vcvtop__, ?(), ?(ZERO_zero__))
  ;; A-binary.watsup:996.5-996.61
  prod {0xFD `%`_u32(95):Bu32} => VCVTOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), `%X%`_shape(F32_lanetype, `%`_dim(4)), PROMOTE_vcvtop__, ?(LOW_half__), ?())
  ;; A-binary.watsup:997.5-997.64
  prod {0xFD `%`_u32(248):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(F32_lanetype, `%`_dim(4)), TRUNC_SAT_vcvtop__(S_sx), ?(), ?())
  ;; A-binary.watsup:998.5-998.64
  prod {0xFD `%`_u32(249):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(F32_lanetype, `%`_dim(4)), TRUNC_SAT_vcvtop__(U_sx), ?(), ?())
  ;; A-binary.watsup:999.5-999.62
  prod {0xFD `%`_u32(250):Bu32} => VCVTOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), `%X%`_shape(I32_lanetype, `%`_dim(4)), CONVERT_vcvtop__(S_sx), ?(), ?())
  ;; A-binary.watsup:1000.5-1000.62
  prod {0xFD `%`_u32(251):Bu32} => VCVTOP_instr(`%X%`_shape(F32_lanetype, `%`_dim(4)), `%X%`_shape(I32_lanetype, `%`_dim(4)), CONVERT_vcvtop__(U_sx), ?(), ?())
  ;; A-binary.watsup:1001.5-1001.69
  prod {0xFD `%`_u32(252):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(F64_lanetype, `%`_dim(2)), TRUNC_SAT_vcvtop__(S_sx), ?(), ?(ZERO_zero__))
  ;; A-binary.watsup:1002.5-1002.69
  prod {0xFD `%`_u32(253):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(F64_lanetype, `%`_dim(2)), TRUNC_SAT_vcvtop__(U_sx), ?(), ?(ZERO_zero__))
  ;; A-binary.watsup:1003.5-1003.66
  prod {0xFD `%`_u32(254):Bu32} => VCVTOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), `%X%`_shape(I32_lanetype, `%`_dim(4)), CONVERT_vcvtop__(S_sx), ?(LOW_half__), ?())
  ;; A-binary.watsup:1004.5-1004.66
  prod {0xFD `%`_u32(255):Bu32} => VCVTOP_instr(`%X%`_shape(F64_lanetype, `%`_dim(2)), `%X%`_shape(I32_lanetype, `%`_dim(4)), CONVERT_vcvtop__(U_sx), ?(LOW_half__), ?())
  ;; A-binary.watsup:1005.5-1005.68
  prod {0xFD `%`_u32(257):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(F32_lanetype, `%`_dim(4)), RELAXED_TRUNC_vcvtop__(S_sx), ?(), ?())
  ;; A-binary.watsup:1006.5-1006.68
  prod {0xFD `%`_u32(258):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(F32_lanetype, `%`_dim(4)), RELAXED_TRUNC_vcvtop__(U_sx), ?(), ?())
  ;; A-binary.watsup:1007.5-1007.73
  prod {0xFD `%`_u32(259):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(F64_lanetype, `%`_dim(2)), RELAXED_TRUNC_vcvtop__(S_sx), ?(), ?(ZERO_zero__))
  ;; A-binary.watsup:1008.5-1008.73
  prod {0xFD `%`_u32(260):Bu32} => VCVTOP_instr(`%X%`_shape(I32_lanetype, `%`_dim(4)), `%X%`_shape(F64_lanetype, `%`_dim(2)), RELAXED_TRUNC_vcvtop__(U_sx), ?(), ?(ZERO_zero__))
}

;; A-binary.watsup
grammar Bexpr : expr
  ;; A-binary.watsup
  prod{`in*` : instr*} {in:Binstr*{in <- `in*`} 0x0B} => in*{in <- `in*`}

;; A-binary.watsup
grammar Bsection_(N : N, syntax en, grammar BX : en*) : en*
  ;; A-binary.watsup
  prod{len : nat, `en*` : en*} {`%`_byte(N):Bbyte `%`_u32(len):Bu32 en*{en <- `en*`}:BX} => en*{en <- `en*`}
    -- if (len = 0)
  ;; A-binary.watsup
  prod eps => []

;; A-binary.watsup
grammar Bcustom : ()*
  ;; A-binary.watsup
  prod {Bname Bbyte*{}} => [()]

;; A-binary.watsup
grammar Bcustomsec : ()
  ;; A-binary.watsup
  prod Bsection_(0, syntax (), grammar Bcustom) => ()

;; A-binary.watsup
grammar Btype : type
  ;; A-binary.watsup
  prod{qt : rectype} qt:Brectype => TYPE_type(qt)

;; A-binary.watsup
grammar Btypesec : type*
  ;; A-binary.watsup
  prod{`ty*` : type*} ty*{ty <- `ty*`}:Bsection_(1, syntax type, grammar Blist(syntax type, grammar Btype)) => ty*{ty <- `ty*`}

;; A-binary.watsup
grammar Bimport : import
  ;; A-binary.watsup
  prod{nm_1 : name, nm_2 : name, xt : externtype} {nm_1:Bname nm_2:Bname xt:Bexterntype} => IMPORT_import(nm_1, nm_2, xt)

;; A-binary.watsup
grammar Bimportsec : import*
  ;; A-binary.watsup
  prod{`im*` : import*} im*{im <- `im*`}:Bsection_(2, syntax import, grammar Blist(syntax import, grammar Bimport)) => im*{im <- `im*`}

;; A-binary.watsup
grammar Bfuncsec : typeidx*
  ;; A-binary.watsup
  prod{`x*` : idx*} x*{x <- `x*`}:Bsection_(3, syntax typeidx, grammar Blist(syntax typeidx, grammar Btypeidx)) => x*{x <- `x*`}

;; A-binary.watsup
grammar Btable : table
  ;; A-binary.watsup
  prod{tt : tabletype, ht : heaptype, at : addrtype, lim : limits} tt:Btabletype => TABLE_table(tt, [REF.NULL_instr(ht)])
    -- if (tt = `%%%`_tabletype(at, lim, REF_reftype(NULL_NULL?{}, ht)))
  ;; A-binary.watsup
  prod{tt : tabletype, e : expr} {0x40 0x00 tt:Btabletype e:Bexpr} => TABLE_table(tt, e)

;; A-binary.watsup
grammar Btablesec : table*
  ;; A-binary.watsup
  prod{`tab*` : table*} tab*{tab <- `tab*`}:Bsection_(4, syntax table, grammar Blist(syntax table, grammar Btable)) => tab*{tab <- `tab*`}

;; A-binary.watsup
grammar Bmem : mem
  ;; A-binary.watsup
  prod{mt : memtype} mt:Bmemtype => MEMORY_mem(mt)

;; A-binary.watsup
grammar Bmemsec : mem*
  ;; A-binary.watsup
  prod{`mem*` : mem*} mem*{mem <- `mem*`}:Bsection_(5, syntax mem, grammar Blist(syntax mem, grammar Bmem)) => mem*{mem <- `mem*`}

;; A-binary.watsup
grammar Bglobal : global
  ;; A-binary.watsup
  prod{gt : globaltype, e : expr} {gt:Bglobaltype e:Bexpr} => GLOBAL_global(gt, e)

;; A-binary.watsup
grammar Bglobalsec : global*
  ;; A-binary.watsup
  prod{`glob*` : global*} glob*{glob <- `glob*`}:Bsection_(6, syntax global, grammar Blist(syntax global, grammar Bglobal)) => glob*{glob <- `glob*`}

;; A-binary.watsup
grammar Bexport : export
  ;; A-binary.watsup
  prod{nm : name, xx : externidx} {nm:Bname xx:Bexternidx} => EXPORT_export(nm, xx)

;; A-binary.watsup
grammar Bexportsec : export*
  ;; A-binary.watsup
  prod{`ex*` : export*} ex*{ex <- `ex*`}:Bsection_(7, syntax export, grammar Blist(syntax export, grammar Bexport)) => ex*{ex <- `ex*`}

;; A-binary.watsup
grammar Bstart : start*
  ;; A-binary.watsup
  prod{x : idx} x:Bfuncidx => [START_start(x)]

;; A-binary.watsup
syntax startopt = start*

;; A-binary.watsup
grammar Bstartsec : start?
  ;; A-binary.watsup
  prod{startopt : startopt} startopt:Bsection_(8, syntax start, grammar Bstart) => $opt_(syntax start, startopt)

;; A-binary.watsup
grammar Belemkind : reftype
  ;; A-binary.watsup
  prod 0x00 => REF_reftype(?(NULL_NULL), FUNC_heaptype)

;; A-binary.watsup
grammar Belem : elem
  ;; A-binary.watsup
  prod{e_o : expr, `y*` : idx*} {`%`_u32(0):Bu32 e_o:Bexpr y*{y <- `y*`}:Blist(syntax funcidx, grammar Bfuncidx)} => ELEM_elem(REF_reftype(?(), FUNC_heaptype), [REF.FUNC_instr(y)*{y <- `y*`}], ACTIVE_elemmode(`%`_tableidx(0), e_o))
  ;; A-binary.watsup
  prod{rt : reftype, `y*` : idx*} {`%`_u32(1):Bu32 rt:Belemkind y*{y <- `y*`}:Blist(syntax funcidx, grammar Bfuncidx)} => ELEM_elem(rt, [REF.FUNC_instr(y)*{y <- `y*`}], PASSIVE_elemmode)
  ;; A-binary.watsup
  prod{x : idx, e : expr, rt : reftype, `y*` : idx*} {`%`_u32(2):Bu32 x:Btableidx e:Bexpr rt:Belemkind y*{y <- `y*`}:Blist(syntax funcidx, grammar Bfuncidx)} => ELEM_elem(rt, [REF.FUNC_instr(y)*{y <- `y*`}], ACTIVE_elemmode(x, e))
  ;; A-binary.watsup
  prod{rt : reftype, `y*` : idx*} {`%`_u32(3):Bu32 rt:Belemkind y*{y <- `y*`}:Blist(syntax funcidx, grammar Bfuncidx)} => ELEM_elem(rt, [REF.FUNC_instr(y)*{y <- `y*`}], DECLARE_elemmode)
  ;; A-binary.watsup
  prod{e_O : expr, `e*` : expr*} {`%`_u32(4):Bu32 e_O:Bexpr e*{e <- `e*`}:Blist(syntax expr, grammar Bexpr)} => ELEM_elem(REF_reftype(?(NULL_NULL), FUNC_heaptype), e*{e <- `e*`}, ACTIVE_elemmode(`%`_tableidx(0), e_O))
  ;; A-binary.watsup
  prod{rt : reftype, `e*` : expr*} {`%`_u32(5):Bu32 rt:Breftype e*{e <- `e*`}:Blist(syntax expr, grammar Bexpr)} => ELEM_elem(rt, e*{e <- `e*`}, PASSIVE_elemmode)
  ;; A-binary.watsup
  prod{x : idx, e_O : expr, `e*` : expr*} {`%`_u32(6):Bu32 x:Btableidx e_O:Bexpr e*{e <- `e*`}:Blist(syntax expr, grammar Bexpr)} => ELEM_elem(REF_reftype(?(NULL_NULL), FUNC_heaptype), e*{e <- `e*`}, ACTIVE_elemmode(x, e_O))
  ;; A-binary.watsup
  prod{rt : reftype, `e*` : expr*} {`%`_u32(7):Bu32 rt:Breftype e*{e <- `e*`}:Blist(syntax expr, grammar Bexpr)} => ELEM_elem(rt, e*{e <- `e*`}, DECLARE_elemmode)

;; A-binary.watsup
grammar Belemsec : elem*
  ;; A-binary.watsup
  prod{`elem*` : elem*} elem*{elem <- `elem*`}:Bsection_(9, syntax elem, grammar Blist(syntax elem, grammar Belem)) => elem*{elem <- `elem*`}

;; A-binary.watsup
syntax code = (local*, expr)

;; A-binary.watsup
grammar Blocals : local*
  ;; A-binary.watsup
  prod{n : n, t : valtype} {`%`_u32(n):Bu32 t:Bvaltype} => LOCAL_local(t)^n{}

;; A-binary.watsup
grammar Bfunc : code
  ;; A-binary.watsup
  prod{`loc**` : local**, e : expr} {loc*{loc <- `loc*`}*{`loc*` <- `loc**`}:Blist(syntax local*, grammar Blocals) e:Bexpr} => ($concat_(syntax local, loc*{loc <- `loc*`}*{`loc*` <- `loc**`}), e)
    -- if (|$concat_(syntax local, loc*{loc <- `loc*`}*{`loc*` <- `loc**`})| < (2 ^ 32))

;; A-binary.watsup
grammar Bcode : code
  ;; A-binary.watsup
  prod{len : nat, code : code} {`%`_u32(len):Bu32 code:Bfunc} => code
    -- if (len = 0)

;; A-binary.watsup
grammar Bcodesec : code*
  ;; A-binary.watsup
  prod{`code*` : code*} code*{code <- `code*`}:Bsection_(10, syntax code, grammar Blist(syntax code, grammar Bcode)) => code*{code <- `code*`}

;; A-binary.watsup
grammar Bdata : data
  ;; A-binary.watsup
  prod{e : expr, `b*` : byte*} {`%`_u32(0):Bu32 e:Bexpr b*{b <- `b*`}:Blist(syntax byte, grammar Bbyte)} => DATA_data(b*{b <- `b*`}, ACTIVE_datamode(`%`_memidx(0), e))
  ;; A-binary.watsup
  prod{`b*` : byte*} {`%`_u32(1):Bu32 b*{b <- `b*`}:Blist(syntax byte, grammar Bbyte)} => DATA_data(b*{b <- `b*`}, PASSIVE_datamode)
  ;; A-binary.watsup
  prod{x : idx, e : expr, `b*` : byte*} {`%`_u32(2):Bu32 x:Bmemidx e:Bexpr b*{b <- `b*`}:Blist(syntax byte, grammar Bbyte)} => DATA_data(b*{b <- `b*`}, ACTIVE_datamode(x, e))

;; A-binary.watsup
grammar Bdatasec : data*
  ;; A-binary.watsup
  prod{`data*` : data*} data*{data <- `data*`}:Bsection_(11, syntax data, grammar Blist(syntax data, grammar Bdata)) => data*{data <- `data*`}

;; A-binary.watsup
grammar Bdatacnt : u32*
  ;; A-binary.watsup
  prod{n : n} `%`_u32(n):Bu32 => [`%`_u32(n)]

;; A-binary.watsup
syntax nopt = u32*

;; A-binary.watsup
grammar Bdatacntsec : u32?
  ;; A-binary.watsup
  prod{nopt : nopt} nopt:Bsection_(12, syntax u32, grammar Bdatacnt) => $opt_(syntax u32, nopt)

;; A-binary.watsup
grammar Btag : tag
  ;; A-binary.watsup
  prod{x : idx} x:Btypeidx => TAG_tag(x)

;; A-binary.watsup
grammar Btagsec : tag*
  ;; A-binary.watsup
  prod{`tag*` : tag*} tag*{tag <- `tag*`}:Bsection_(13, syntax tag, grammar Blist(syntax tag, grammar Btag)) => tag*{tag <- `tag*`}

;; A-binary.watsup
grammar Bmagic : ()
  ;; A-binary.watsup
  prod {0x00 0x61 0x73 0x6D} => ()

;; A-binary.watsup
grammar Bversion : ()
  ;; A-binary.watsup
  prod {0x01 0x00 0x00 0x00} => ()

;; A-binary.watsup
grammar Bmodule : module
  ;; A-binary.watsup
  prod{`type*` : type*, `import*` : import*, `typeidx*` : typeidx*, `table*` : table*, `mem*` : mem*, `tag*` : tag*, `global*` : global*, `export*` : export*, `start?` : start?, `elem*` : elem*, `n?` : n?, `local**` : local**, `expr*` : expr*, `data*` : data*, `func*` : func*} {Bmagic Bversion Bcustomsec*{} type*{type <- `type*`}:Btypesec Bcustomsec*{} import*{import <- `import*`}:Bimportsec Bcustomsec*{} typeidx*{typeidx <- `typeidx*`}:Bfuncsec Bcustomsec*{} table*{table <- `table*`}:Btablesec Bcustomsec*{} mem*{mem <- `mem*`}:Bmemsec Bcustomsec*{} tag*{tag <- `tag*`}:Btagsec Bcustomsec*{} global*{global <- `global*`}:Bglobalsec Bcustomsec*{} export*{export <- `export*`}:Bexportsec Bcustomsec*{} start?{start <- `start?`}:Bstartsec Bcustomsec*{} elem*{elem <- `elem*`}:Belemsec Bcustomsec*{} `%`_u32(n)?{n <- `n?`}:Bdatacntsec Bcustomsec*{} (local*{local <- `local*`}, expr)*{expr <- `expr*`, `local*` <- `local**`}:Bcodesec Bcustomsec*{} data*{data <- `data*`}:Bdatasec Bcustomsec*{}} => MODULE_module(type*{type <- `type*`}, import*{import <- `import*`}, func*{func <- `func*`}, global*{global <- `global*`}, table*{table <- `table*`}, mem*{mem <- `mem*`}, tag*{tag <- `tag*`}, elem*{elem <- `elem*`}, data*{data <- `data*`}, start?{start <- `start?`}, export*{export <- `export*`})
    -- (if (n = |data*{data <- `data*`}|))?{n <- `n?`}
    -- if ((n?{n <- `n?`} =/= ?()) \/ ($dataidx_funcs(func*{func <- `func*`}) = []))
    -- (if (func = FUNC_func(typeidx, local*{local <- `local*`}, expr)))*{expr <- `expr*`, func <- `func*`, `local*` <- `local**`, typeidx <- `typeidx*`}

;; C-conventions.watsup
syntax A = nat

;; C-conventions.watsup
syntax B = nat

;; C-conventions.watsup
syntax sym =
  | _FIRST{A_1 : A}(A_1 : A)
  | _DOTS
  | _LAST{A_n : A}(A_n : A)

;; C-conventions.watsup
syntax symsplit =
  | _FIRST{A_1 : A}(A_1 : A)
  | _LAST{A_2 : A}(A_2 : A)

;; C-conventions.watsup
syntax recorddots = ()

;; C-conventions.watsup
syntax record =
{
  FIELD_1{A_1 : A} A,
  FIELD_2{A_2 : A} A,
  `...`{recorddots : recorddots} recorddots
}

;; C-conventions.watsup
syntax pth =
  | PTHSYNTAX

;; C-conventions.watsup
syntax T = nat

;; C-conventions.watsup
relation NotationTypingPremise: `%`(nat)

;; C-conventions.watsup
relation NotationTypingPremisedots: `...`

;; C-conventions.watsup
relation NotationTypingScheme: `%`(nat)
  ;; C-conventions.watsup
  rule _{conclusion : nat, premise_1 : nat, premise_2 : nat, premise_n : nat}:
    `%`(conclusion)
    -- NotationTypingPremise: `%`(premise_1)
    -- NotationTypingPremise: `%`(premise_2)
    -- NotationTypingPremisedots: `...`
    -- NotationTypingPremise: `%`(premise_n)

;; C-conventions.watsup
rec {

;; C-conventions.watsup:38.1-38.82
relation NotationTypingInstrScheme: `%|-%:%`(context, instr*, functype)
  ;; C-conventions.watsup:40.1-41.38
  rule i32.add{C : context}:
    `%|-%:%`(C, [BINOP_instr(I32_numtype, ADD_binop_)], `%->%`_functype(`%`_resulttype([I32_valtype I32_valtype]), `%`_resulttype([I32_valtype])))

  ;; C-conventions.watsup:43.1-45.29
  rule global.get{C : context, x : idx, t : valtype, mut : mut}:
    `%|-%:%`(C, [GLOBAL.GET_instr(x)], `%->%`_functype(`%`_resulttype([]), `%`_resulttype([t])))
    -- if (C.GLOBALS_context[x!`%`_idx.0] = `%%`_globaltype(mut, t))

  ;; C-conventions.watsup:47.1-50.78
  rule block{C : context, blocktype : blocktype, `instr*` : instr*, `t_1*` : valtype*, `t_2*` : valtype*}:
    `%|-%:%`(C, [BLOCK_instr(blocktype, instr*{instr <- `instr*`})], `%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- Blocktype_ok: `%|-%:%`(C, blocktype, `%->_%%`_instrtype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), [], `%`_resulttype(t_2*{t_2 <- `t_2*`})))
    -- NotationTypingInstrScheme: `%|-%:%`({TYPES [], RECS [], FUNCS [], GLOBALS [], TABLES [], MEMS [], TAGS [], ELEMS [], DATAS [], LOCALS [], LABELS [`%`_resulttype(t_2*{t_2 <- `t_2*`})], RETURN ?(), REFS []} +++ C, instr*{instr <- `instr*`}, `%->%`_functype(`%`_resulttype(t_1*{t_1 <- `t_1*`}), `%`_resulttype(t_2*{t_2 <- `t_2*`})))
}

;; C-conventions.watsup
relation NotationReduct: `~>%`(instr*)
  ;; C-conventions.watsup
  rule 2{q_1 : num_(F64_numtype), q_4 : num_(F64_numtype), q_3 : num_(F64_numtype)}:
    `~>%`([CONST_instr(F64_numtype, q_1) CONST_instr(F64_numtype, q_4) CONST_instr(F64_numtype, q_3) BINOP_instr(F64_numtype, ADD_binop_) BINOP_instr(F64_numtype, MUL_binop_)])

  ;; C-conventions.watsup
  rule 3{q_1 : num_(F64_numtype), q_5 : num_(F64_numtype)}:
    `~>%`([CONST_instr(F64_numtype, q_1) CONST_instr(F64_numtype, q_5) BINOP_instr(F64_numtype, MUL_binop_)])

  ;; C-conventions.watsup
  rule 4{q_6 : num_(F64_numtype)}:
    `~>%`([CONST_instr(F64_numtype, q_6)])

;; C-conventions.watsup
def $instrdots : instr*

;; C-conventions.watsup
syntax label =
  | `LABEL_%{%}`{n : n, `instr*` : instr*}(n : n, instr*{instr <- `instr*`} : instr*)

;; C-conventions.watsup
syntax callframe =
  | `FRAME_%{%}`{n : n, frame : frame}(n : n, frame : frame)

;; C-conventions.watsup
def $allocX(syntax X, syntax Y, store : store, X : X, Y : Y) : (store, addr)

;; C-conventions.watsup
rec {

;; C-conventions.watsup:80.1-80.117
def $allocXs(syntax X, syntax Y, store : store, X*, Y*) : (store, addr*)
  ;; C-conventions.watsup:81.1-81.57
  def $allocXs{syntax X, syntax Y, s : store}(syntax X, syntax Y, s, [], []) = (s, [])
  ;; C-conventions.watsup:82.1-84.65
  def $allocXs{syntax X, syntax Y, s : store, X : X, `X'*` : X*, Y : Y, `Y'*` : Y*, s_2 : store, a : addr, `a'*` : addr*, s_1 : store}(syntax X, syntax Y, s, [X] ++ X'*{X' <- `X'*`}, [Y] ++ Y'*{Y' <- `Y'*`}) = (s_2, [a] ++ a'*{a' <- `a'*`})
    -- if ((s_1, a) = $allocX(syntax X, syntax Y, s, X, Y))
    -- if ((s_2, a'*{a' <- `a'*`}) = $allocXs(syntax X, syntax Y, s_1, X'*{X' <- `X'*`}, Y'*{Y' <- `Y'*`}))
}

;; C-conventions.watsup
grammar Btypewriter : ()
  ;; C-conventions.watsup
  prod 0x00 => ()

;; C-conventions.watsup
syntax symdots =
  | `%`{i : nat}(i : nat)
    -- if (i = 0)

;; C-conventions.watsup
def $var(syntax X) : nat
  ;; C-conventions.watsup
  def $var{syntax X}(syntax X) = 0

;; C-conventions.watsup
grammar Bvar(syntax X) : ()
  ;; C-conventions.watsup
  prod 0x00 => ()

;; C-conventions.watsup
grammar Bsym : A
  ;; C-conventions.watsup
  prod Bvar(syntax B) => $var(syntax A)
  ;; C-conventions.watsup
  prod (Bvar(syntax symdots) | Bvar(syntax B)) => $var(syntax A)

== IL Validation...
== Complete.
```
