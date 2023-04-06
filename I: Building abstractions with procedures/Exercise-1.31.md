> a) The `sum` procedure is only the simplest of a vast number of similar abstractions
>    that can be captured as higher-order procedures. Write an analogous procedure
>    called `product` that returns the product of the values of a function at points
>    over a given range. Show how to define `factorial` in terms of `product`. Also use
>    `product` to compute approximations to $\pi$ using the formula
>    $$
>    \frac{\pi}{4}=\frac{2 \cdot 4 \cdot 4 \cdot 6 \cdot 6 \cdot 8 \cdots}{3 \cdot 3
>    \cdot 5 \cdot 5 \cdot 7 \cdot 7 \cdots}
>    $$
> b) If your `product` procedure generates a recursive process, write one that
>    generates an iterative process. If it generates an iterative process, write one
>    that gen- erates a recursive process.

a)

```scheme 
   (define (product term a next b)
   (if (> a b)

       1
       (* (term a)
           (product term (next a) next b))))
```

```scheme 
   (define (factorial n)
     (product identity 1 inc n))
```

```scheme 
   (define (pi-Wallis n)
     (define (term-Wallis k)
       (if (even? k)
           (/ (+ k 2) (+ k 1))
           (/ (+ k 1) (+ k 2))))
     (* 4 (product term-wallis 1 inc n)))
```

b)

```scheme 
   (define (product term a next b)
     (define (iter a result)
       (if (> a b)
           result
           (iter (next a) (* result (term a)))))
     (iter a 1))
```

