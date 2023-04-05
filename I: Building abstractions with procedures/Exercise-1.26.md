> Louis Reasoner is having great difficulty do- ing Exercise 1.24. His =fast-prime?=
> test seems to run more slowly than his =prime?= test. Louis calls his friend Eva
> Lu Ator over to help. When they examine Louis’s code, they find that he has
> rewritten the =expmod= procedure to use an explicit multiplication, rather than
> calling square:
> #+begin_src scheme
> (define (expmod base exp m)
>   (cond ((= exp 0) 1)
>         ((even? exp)
>          (remainder (* (expmod base (/ exp 2) m)
>                        (expmod base (/ exp 2) m))
>                     m))
>         (else
>          (remainder (* base
>                        (expmod base (- exp 1) m))
>                     m))))
> #+end_src
> “I don’t see what difference that could make,” says Louis. “I do.” says Eva.
> “By writing the procedure like that, you have transformed the $\Theta(\log n)$
> process into a $\Theta(n)$ process.” Explain.
That is because, instead of applying `expmod` and then multiplying the result by itself, now it is calculated twice, so insted of $n$ steps, it uses $n^2$.

