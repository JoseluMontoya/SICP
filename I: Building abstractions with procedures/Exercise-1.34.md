> Suppose we define the procedure
> #+begin_src scheme
> (define (f g) (g 2))
> #+end_src
> Then we have
> #+begin_src scheme
> (f square)
> 4
> (f (lambda (z) (* z (+ z 1)))) 6
> #+end_src
> What happens if we (perversely) ask the interpreter to evaluate the combination
> =(f f)=? Explain.
```scheme 
(f f)
(f 2)
(2 2)
```

Since 2 isn't a procedure, the interpreter will trow out an error.

