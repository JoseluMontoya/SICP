    Let $f$ and $g$ be two one-argument functions. The composition $f$ after $g$ is defined to be the function $x \mapsto f(g(x))$. Define a procedure =compose= that implements composition. For example, if =inc= is a procedure that adds 1 to its argument,
    #+begin_src scheme
    ((compose square inc) 6)
    49
    #+end_src

```scheme 
(define (compose f g) (lambda (x) (f (g x))))
```

