> Translate the following expression into prefix form:

$$
\frac{5 + 4 + (2 - (3 - (6 + \frac{4}{5})))}{3(6 - 2)(2 - 7)}
$$

What we are going to do is find the outermost operation, and change his notation to prefix. We start with the fraction

$$ (/\\ (5 + 4 + (2 - (3 - (6 + \\frac{4}{5}))))\\ (3(6 - 2)(2 - 7))) $$

Then, the sum of the numerator and the product in the denominator

$$ (/\\ (+\\ 5\\ 4\\ (2 - (3 - (6 + \\frac{4}{5}))))\\ (\*\\ 3\\ (6 - 2)\\ (2 - 7))) $$

And so on and so forth

\\begin{gather\*} (/\\ (+\\ 5\\ 4\\ (-\\ 2\\ (3 - (6 + \\frac{4}{5}))))\\ (\*\\ 3\\ (-\\ 6\\ 2)\\ (-\\ 2\\ 7)))\\\\ (/\\ (+\\ 5\\ 4\\ (-\\ 2\\ (-\\ 3\\ (6 + \\frac{4}{5}))))\\ (\*\\ 3\\ (-\\ 6\\ 2)\\ (-\\ 2\\ 7)))\\\\ (/\\ (+\\ 5\\ 4\\ (-\\ 2\\ (-\\ 3\\ (+\\ 6\\ \\frac{4}{5}))))\\ (\*\\ 3\\ (-\\ 6\\ 2)\\ (-\\ 2\\ 7)))\\\\ (/\\ (+\\ 5\\ 4\\ (-\\ 2\\ (-\\ 3\\ (+\\ 6\\ (/\\ 4\\ 5)))))\\ (\*\\ 3\\ (-\\ 6\\ 2)\\ (-\\ 2\\ 7))) \\end{gather\*}

And finally, we use pretty-printing

```scheme 
    (/ (+ 5
        4
        (- 2
            (- 3
                (+ 6
                (/ 4 5)))))
    (* 3
        (- 6 2)
        (- 2 7)))
```

