> If $f$ is a numerical function and $n$ is a positive integer, then we can form
> the $n^{th}$ repeated application of $f$, which is defined to be the function
> whose value at $x$ is $f(f(...(f(x))...))$. For example, if $f$ is the function
> $x \mapsto x + 1$, then the $n^{th}$ repeated application of $f$ is the function
> $x \mapsto x +n$.  If $f$ is the operation of squaring a number, then the
> $n^{th}$ repeated application of $f$ is the function that raises its argument to
> the $2^n-th$ power. Write a procedure that takes as inputs a procedure that
> computes $f$ and a positive integer $n$ and returns the procedure that computes
> the $n^{th}$ repeated application of $f$. Your procedure should be able to be
> used as follows:
> ```scheme
> ((repeated square 2) 5)
> 625
> ```
> Hint: You may find it convenient to use `compose` from Exercise 1.42.

```scheme :exports,none,:session,"1.43"
(define (compose f g) (lambda (x) (f (g x))))
```

```scheme :session,"1.43"
(define (repeated f n)
  (define (repeated-iter f-iter n)
    (if (= n 0)
        f-iter
        (repeated-iter (compose f f-iter) (- n 1))))
  (repeated-iter (lambda (x) x) n))
```


