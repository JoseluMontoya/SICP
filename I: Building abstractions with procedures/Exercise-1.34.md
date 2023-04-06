> Suppose we define the procedure
> ```scheme
> (define (f g) (g 2))
> ```
> Then we have
> ```scheme
> (f square)
> 4
> (f (lambda (z) (* z (+ z 1)))) 6
> ```
> What happens if we (perversely) ask the interpreter to evaluate the combination
> `(f f)`? Explain.

```scheme 
(f f)
(f 2)
(2 2)
```

Since 2 isn't a procedure, the interpreter will trow out an error.

