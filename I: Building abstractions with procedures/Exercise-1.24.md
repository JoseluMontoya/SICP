> Modify the `timed-prime-test` procedure of Exercise 1.22 to use `fast-prime?` (the
> Fermat method), and test each of the 12 primes you found in that exercise. Since
> the Fermat test has $\Theta(\log n)$ growth, how would you expect the time to
> test primes near 1,000,000 to compare with the time needed to test primes near
> 1000? Do your data bear this out? Can you explain any discrepancy you find?

``` scheme :session "1.24" :exports none
(define (fermat-test n)
  (define (try-it a)
    (= (expmod a n n) a))
  (try-it (+ 1 (random (- n 1)))))

(define (fast-prime? n times)
  (cond ((= times 0) true)
        ((fermat-test n) (fast-prime? n (- times 1)))
        (else false)))

(define (expmod base exp m)
  (cond ((= exp 0) 1)
        ((even? exp)
         (remainder
          (square (expmod base (/ exp 2) m))
          m))
        (else
         (remainder
          (* base (expmod base (- exp 1) m))
          m))))

(define (square a) (* a a))
```

``` scheme :session "1.24" :exports none
(define (timed-prime-test n)
  (start-prime-test n (runtime)))

(define (start-prime-test n start-time)
  (if (fast-prime? n 100)
      (report-prime n (- (runtime) start-time))))

(define (report-prime n elapsed-time)
  (display n)
  (display " *** ")
  (display elapsed-time)
  (newline))
```

|  Number | Time without Fermat | Time with Fermat |
|---------|---------------------|------------------|
|    1009 |                   1 |               87 |
|    1013 |                   1 |               90 |
|    1019 |                   1 |               95 |
|   10007 |                   5 |              110 |
|   10009 |                   4 |              110 |
|   10037 |                   4 |              112 |
|  100003 |                  13 |              135 |
|  100019 |                  12 |              133 |
|  100043 |                  12 |              131 |
| 1000003 |                  40 |              155 |
| 1000033 |                  38 |              149 |
| 1000037 |                  38 |              141 |

As we can see, without Fermat, increasing the number 10 times makes the procces
3.16 times slower, but with Femat it only increases by 20 micro seconds, which
is a logaritmic order of growth. Since the Fermat test takes a set ammount of
times to be performed to increase the likelihood of the number being prime,
that explains the increase in base time and the over all slowness of the
procedure for numbers this small.
