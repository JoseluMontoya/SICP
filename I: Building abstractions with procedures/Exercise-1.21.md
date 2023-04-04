    Use the =smallest-divisor= procedure to find the smallest divisor of each of the
    following numbers: 199, 1999, 19999.

```scheme :session,"1.21"

(define (smallest-divisor n) (find-divisor n 2))

(define (find-divisor n test-divisor)
  (cond ((> (square test-divisor) n) n)
        ((divides? test-divisor n) test-divisor)
        (else (find-divisor n (+ test-divisor 1)))))

(define (divides? a b) (= (remainder b a) 0))

(define (square a) (* a a))
```

Let's start with 199

```scheme :session,"1.21",:exports,both
(smallest-divisor 199)
```

Then 1999

```scheme :session,"1.21",:exports,both
(smallest-divisor 1999)
```

And finally 19999

```scheme :session,"1.21",:exports,both
(smallest-divisor 19999)
```

