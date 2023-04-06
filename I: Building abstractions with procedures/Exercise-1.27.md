> Demonstrate that the Carmichael numbers listed in Footnote 1.47 really do fool
> the Fermat test. That is, write a procedure that takes an integer $n$ and tests
> whether $a^n$ is congruent to $a$ modulo $n$ for every $a < n$, and try your
> procedure on the given Carmichael numbers.

```scheme :session,"1.27",:exports,none
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

```scheme :session,"1.27"
(define (fermat-test n)
  (define (try-it-iter a)
    (cond ((and (= (expmod a n n) a) (= n (+ a 1)))
           true)
          ((and (= (expmod a n n) a) (> n a))
           (try-it-iter (+ a 1)))
          (else false)))
    (try-it-iter 1))
```

Let's try the new Fermat test with the Carmichael numbers in footnote 47

```scheme :session,"1.27",:exports,both
(fermat-test 561)
```
```
#t
```
```scheme :session,"1.27",:exports,both
(fermat-test 1105)
```
```
#t
```
```scheme :session,"1.27",:exports,both
(fermat-test 1729)
```
```
#t
```
```scheme :session,"1.27",:exports,both
(fermat-test 2465)
```
```
#t
```
```scheme :session,"1.27",:exports,both
(fermat-test 2821)
```
```
#t
```
```scheme :session,"1.27",:exports,both
(fermat-test 6601)
```
```
#t
```
