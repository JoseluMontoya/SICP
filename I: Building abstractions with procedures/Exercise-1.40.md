> Define a procedure cubic that can be used together with the `newtons-method` procedure in expressions of the form
> ```scheme
> (newtons-method (cubic a b c) 1)
> ```
> to approximate zeros of the cubic $x^3 + a x^2 + bx + c$.

```scheme 
(define (cubic a b c)
  (lambda (x) (+ (* x x x) (* a x x) (* b x) c)))
```

