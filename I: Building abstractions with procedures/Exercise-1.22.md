> Most Lisp implementations include a primitive called `runtime` that returns an
> integer that specifies the amount of time the system has been running (measured,
> for example, in microseconds). The following `timed-prime-test` procedure, when
> called with an integer $n$, prints $n$ and checks to see if $n$ is prime. If $n$
> is prime, the procedure prints three asterisks followed by the amount of time
> used in performing the test.
> 
> ``` scheme
> (define (timed-prime-test n)
>   (newline)
>   (display n)
>   (start-prime-test n (runtime)))
> 
> (define (start-prime-test n start-time)
>   (if (prime? n)
>       (report-prime (- (runtime) start-time))))
> 
> (define (report-prime elapsed-time)
>   (display " *** ")
>   (display elapsed-time))
> ```
> 
> Using this procedure, write a procedure `search-for-primes` that checks the
> primality of consecutive odd integers in a specified range. Use your procedure
> to find the three smallest primes larger than 1000; larger than 10,000; larger
> than 100,000; larger than 1,000,000. Note the time needed to test each prime.
> Since the testing algorithm has order of growth of $\Theta(\sqrt{n})$, you
> should expect that testing for primes around 10,000 should take about
> $\sqrt{10}$ times as long as testing for primes around 1000. Do your timing data
> bear this out? How well do the data for 100,000 and 1,000,000 support the
> $\Theta(\sqrt{n})$ prediction? Is your result compatible with the notion that
> programs on your machine run in time proportional to the number of steps
> required for the computation?

``` scheme :session "1.22" :exports none
(define (timed-prime-test n)
  (start-prime-test n (runtime)))

(define (start-prime-test n start-time)
  (if (prime? n)
      (report-prime n (- (runtime) start-time))))

(define (report-prime n elapsed-time)
  (display n)
  (display " *** ")
  (display elapsed-time)
  (newline))

(define (prime? n)
  (= n (smallest-divisor n)))

(define (smallest-divisor n) (find-divisor n 2))

(define (find-divisor n test-divisor)
  (cond ((> (square test-divisor) n) n)
        ((divides? test-divisor n) test-divisor)
        (else (find-divisor n (+ test-divisor 1)))))

(define (divides? a b) (= (remainder b a) 0))

(define (square a) (* a a))

(define (even? a)
  (= (remainder a 2) 0))
```

``` scheme :session "1.22"
(define (search-for-primes a b)
  (define (search-for-primes-iter a b)
    (cond ((<= a b) ;; a is assumed to be odd
           (timed-prime-test a)
           (search-for-primes-iter (+ a 2) b))))
  (if (even? a)
      (search-for-primes-iter (+ a 1) b)
      (search-for-primes-iter a b)))
```

``` scheme :session "1.22"
(search-for-primes 1000 1050)
```

```
1009 *** 1
1013 *** 1
1019 *** 1
1021 *** 2
1031 *** 2
1033 *** 2
1039 *** 1
1049 *** 2
```


``` scheme :session "1.22"
(search-for-primes 10000 10050)
```

```
10007 *** 5
10009 *** 4
10037 *** 4
10039 *** 4
```


``` scheme :session "1.22"
(search-for-primes 100000 100050)
```

```
100003 *** 13
100019 *** 12
100043 *** 12
100049 *** 12
```


``` scheme :session "1.22"
(search-for-primes 1000000 1000050)
```

```
1000003 *** 40
1000033 *** 38
1000037 *** 38
1000039 *** 41
```

As we can see, when searching primes, the distribution between the theoretical
times and the real times is the following:

| Beginning of searc | Theoretical proportion | Real proportion |
|--------------------|------------------------|-----------------|
|               1000 |                      1 |               1 |
|              10000 |                   3.16 |            4.33 |
|             100000 |                     10 |           12.33 |
|            1000000 |                  31.62 |           38.67 |

Which line up pretty nicely, considering that $\Theta$ notation is an
aproximation, so we can be confident that the time grows proportionally with
the ammount of steps.
