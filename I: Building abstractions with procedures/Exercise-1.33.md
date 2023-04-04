    You can obtain an even more general version of =accumulate= (Exercise 1.32) by
    introducing the notion of a =filter= on the terms to be combined. That is, combine
    only those terms derived from values in the range that satisfy a specified
    condition. The resulting =filtered-accumulate= abstraction takes the same
    arguments as accumulate, together with an additional predicate of one argument
    that specifies the filter. Write =filtered-accumulate= as a procedure. Show how to
    express the following using =filtered-accumulate=:

    a) The sum of the squares of the prime numbers in the interval $a$ to $b$
       (assuming that you have a =prime?= predicate already written)

    b) The product of all the positive integers less than $n$ that are relatively
       prime to $n$ (i.e., all positive integers $i < n$ such that $\text{gdc}(i,n) = 1$)

```scheme 
(define (filtered-accumulate combiner null-value filter term a next b)
  (cond ((> a b) null-value)
        ((filter a) (combiner (term a) (product term (next a) next b)))
        (else (combiner null-value (product term (next a) next b)))))
```

a)

```scheme 
   (define (sum-square-primes a b)
     (filtered-accumulate + 0 prime? square a inc b))
```

b)

```scheme 
   (define (product-rel-prime n)
     (define (rel-prime? i) (= 1 (gdc i n)))
     (filtered-accumulate * 0 rel-prime? identity 1 inc (- n 1)))
```

