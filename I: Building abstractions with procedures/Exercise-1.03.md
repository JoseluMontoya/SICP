> Define a procedure that takes three numbers as arguments and returns the sum of the squares of the two larger numbers.

```scheme 
(define (f a b c)
  (cond ((and (> a c) (> b c)) (+ (* a a) (* b b)))
        ((and (> a b) (> c b)) (+ (* a a) (* c c)))
        ((and (> b a) (> c a)) (+ (* b b) (* c c)))))
```
