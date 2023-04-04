    Alyssa P. Hacker complains that we went to a lot of extra work in writing
    =expmod=. After all, she says, since we already know how to compute exponentials,
    we could have simply written
    #+begin_src scheme
    (define (expmod base exp m)
      (remainder (fast-expt base exp) m))
    #+end_src
    Is she correct? Would this procedure serve as well for our fast prime tester?
    Explain.

It would work, but at a great computational cost. As the footnote number 46 says, computing the remainder constantly instead of at the end, ensures us that the size of the numbers doesn't get out of hand.

