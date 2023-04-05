> Using the results of Exercise 1.16 and Exercise 1.17, devise a procedure that
> generates an iterative process for multiplying two integers in terms of adding,
> doubling, and halving and uses a logarithmic number of steps
```scheme 
(define (fast-* a b)
  (define (even? b)
    (= (remainder b 2) 0))
  (define (double b)
    (+ b b))
  (define (halve b)
    (/ b 2))
  (define (fast-*-iter a b c)
    (cond ((= b 0) c)
          ((even? b)
           (fast-*-iter (double a) (halve b) c))
          (else
           (fast-*-iter a (- b 1) (+ a c)))))
  (fast-*-iter a b 0))
```

