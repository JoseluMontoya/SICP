    The following procedure computes a mathematical function called Ackermann’s
    function.

    #+begin_src scheme
    (define (A x y)
      (cond ((= y 0) 0)
            ((= x 0) (* 2 y))
            ((= y 1) 2)
            (else (A (- x 1) (A x (- y 1))))))
    #+end_src

    What are the values of the following expressions?

    #+begin_src scheme
    (A 1 10)
    (A 2 4)
    (A 3 3)
    #+end_src

    Consider the following procedures, where A is the procedure defined above:

    #+begin_src scheme
    (define (f n) (A 0 n))
    (define (g n) (A 1 n))
    (define (h n) (A 2 n))
    (define (k n) (* 5 n n))
    #+end_src

    Give concise mathematical definitions for the functions computed by the
    procedures =f=, =g=, and =h= for positive integer values of =n=. For example,
    =(k n)= computes $5n^{2}$.

\\newpage Let's use the substitution model to get the values of the expressions

```scheme 
(A 1 10)
(A 0 (A 1 9))
(A 0 (A 0 (A 1 8)))
(A 0 (A 0 (A 0 (A 1 7))))
(A 0 (A 0 (A 0 (A 0 (A 1 6)))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 1 5))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 1 4)))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 1 3))))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 1 2)))))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 1 1))))))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 2)))))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 4))))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 8)))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 16))))))
(A 0 (A 0 (A 0 (A 0 (A 0 32)))))
(A 0 (A 0 (A 0 (A 0 64))))
(A 0 (A 0 (A 0 128)))
(A 0 (A 0 256))
(A 0 512)
1024
```

Which is $2^{10}$.

```scheme 
(A 2 4)
(A 1 (A 2 3))
(A 1 (A 1 (A 2 2)))
(A 1 (A 1 (A 1 (A 2 1))))
(A 1 (A 1 (A 1 2)))
(A 1 (A 1 (A 0 (A 1 1))))
(A 1 (A 1 (A 0 2)))
(A 1 (A 1 4))
(A 1 (A 0 (A 1 3)))
(A 1 (A 0 (A 0 (A 1 2))))
(A 1 (A 0 (A 0 (A 0 (A 1 1)))))
(A 1 (A 0 (A 0 (A 0 2))))
(A 1 (A 0 (A 0 4)))
(A 1 (A 0 8))
(A 1 16)
```

And thanks to the analysis of the previous expression, we know that (A 1 16) equals 2^{16} = $2 \\uparrow\\uparrow 4$ = $^4 2 = 65536$, with $2 \\uparrow\\uparrow 4$ and $^4 2$ being the notation for the [tetration](http://en.wikipedia.org/wiki/Tetration).

```scheme 
(A 3 3)
(A 2 (A 3 2))
(A 2 (A 2 (A 3 1)))
(A 2 (A 2 2))
(A 2 (A 1 (A 2 1)))
(A 2 (A 1 2))
(A 2 (A 0 (A 1 1)))
(A 2 (A 0 2))
(A 2 4)
```

Which is the same expression as the last one.

Given what we have seen, we can safely state that:

$$ f(n) = 2n $$

$$ g(n) = 2^n $$

$$ k(n) = 2 \\uparrow\\uparrow n $$

