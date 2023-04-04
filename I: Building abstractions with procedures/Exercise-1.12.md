    The following pattern of numbers is called Pascal’s triangle.

    \begin{tabular}{rccccccccc}
    &    &    &    &    &  1\\\noalign{\smallskip\smallskip}
    &    &    &    &  1 &    &  1\\\noalign{\smallskip\smallskip}
    &    &    &  1 &    &  2 &    &  1\\\noalign{\smallskip\smallskip}
    &    &  1 &    &  3 &    &  3 &    &  1\\\noalign{\smallskip\smallskip}
    &  1 &    &  4 &    &  6 &    &  4 &    &  1\\\noalign{\smallskip\smallskip}
    \end{tabular}

    The numbers at the edge of the triangle are all 1, and each number inside the
    triangle is the sum of the two numbers above it. Write a procedure that
    computes elements of Pascal’s triangle by means of a recursive process.

```scheme 
(define (pascal-triangle row number)
  (cond ((or (< number 1) (> number row)) 0)
        ((or (= number 1) (= number row)) 1)
        (else (+ (pascal-triangle (- row 1) number)
                 (pascal-triangle (- row 1) (- number 1))))))
```

