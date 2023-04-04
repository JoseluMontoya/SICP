    Simpson’s Rule is a more accurate method of numerical integration than the
    method illustrated above. Using Simpson’s Rule, the integral of a function $f$
    between $a$ and $b$ is approximated as

    $$
    \frac{h}{3}\left(y_{0}+4 y_{1}+2 y_{2}+4 y_{3}+2 y_{4}+\cdots+2 y_{n-2}+4
    y_{n-1}+y_{n}\right)
    $$

    where $h = (b − a)/n$, for some even integer $n$, and $y_k = f (a + kh)$.
    (Increasing $n$ increases the accuracy of the approximation.) Define a
    procedure that takes as arguments $f$ , $a$, $b$, and $n$ and returns the value
    of the integral, computed using Simpson’s Rule. Use your procedure to
    integrate cube between 0 and 1 (with $n = 100$ and $n = 1000$), and compare the
    results to those of the integral procedure shown above.

Since it's a sum over term, where going to use the procedure `sum`

```scheme :session,"1.29"
(define (sum term a next b)
  (if (> a b)
      0
      (+ (term a)
         (sum term (next a) next b))))
```

: #&lt;void>

The `next` procedure will be simply `inc`

```scheme :session,"1.29"
(define (inc n) (+ n 1))
```

: #&lt;void>

And `term` will be $\\frac{h}{3}A_k y_k$, with $A_k$ being equal to 1 if $k = 1$ or $k = n$, 4 if $k$ is odd and 2 if $k$ is even

```scheme :session,"1.29"
(define (even? a)
  (= (remainder a 2) 0))

(define (int-term a b n f k)
  (define h (/ (- b a) n))
  (define (A i)
    (cond ((or (= i 1) (= i n)) 1)
          ((even? i) 2)
          (else 4)))
  (* (/ h 3) (A k) (f (+ a (* h k)))))
```

: #&lt;void>

And with this, we can build the procedure

```scheme :session,"1.29"
(define (Simpson-Int a b n f)
  (define (term k)
    (int-term a b n f k))
  (sum term 0 inc n))
```

: #&lt;void>

Since we want to integrate `cube` between 0 and 1 we implement it

```scheme :session,"1.29",:exports,both
(define (cube a) (* a a a))
```

And it should give us 0.25

```scheme :session,"1.29"
(Simpson-Int 0 1.0 100 cube)
```

: 0.24999999000000012

```scheme :session,"1.29",:exports,both
(Simpson-Int 0 1.0 1000 cube)
```

: 0.24999999999900005

