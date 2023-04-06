> A continued fraction representation of the tangent function was published in
> 1770 by the German math- ematician J.H. Lambert:
> $$
> \tan x=\frac{x}{1-\frac{x^{2}}{3-\frac{x^{2}}{5-\ldots}}}
> $$
> where $x$ is in radians. Define a procedure `(tan-cf x k)` that computes an
> approximation to the tangent function based on Lambert’s formula. `k` specifies
> the number of terms to compute, as in Exercise 1.37.

```scheme :session,"1.39"
(define (cont-frac n d k)
    (define (iter i)
    (if (= i (+ k 1))
        0
        (/ (n i) (+ (d i) (iter (+ i 1))))))
    (iter 1))
```

: #&lt;void>

```scheme :session,"1.39"
(define (tan-cf x k)
  (define (d i) (- (* 2 i) 1))
  (define (n i)
    (if (= i 1)
        ((lambda (j) j) x)
        (- (square x))))
  (* (cont-frac n
                d
                k) 1.0))
```

: #&lt;void>

