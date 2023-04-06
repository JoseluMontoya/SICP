> Show that the golden ratio $\phi$ (Section 1.2.2) is a fixed point of the
> transformation $x \mapsto 1 + 1/x$, and use this fact to compute $\phi$ by means
> of the fixed-point procedure.

```scheme :session,"1.35"
(define tolerance 0.00001)
(define (fixed-point f first-guess)
  (define (close-enough? v1 v2)
    (< (abs (- v1 v2))
       tolerance))
  (define (try guess)
    (let ((next (f guess)))
      (if (close-enough? guess next)
          next
          (try next))))
  (try first-guess))
```


```scheme :session,"1.35",:exports,both
(fixed-point (lambda (x) (+ 1 (/ 1 x))) 1.0)
```
```
1.6180327868852458
```
And $\\phi$ is 1.618033, which means that our result deviates exactly the ammount associated with `tolerance`.

