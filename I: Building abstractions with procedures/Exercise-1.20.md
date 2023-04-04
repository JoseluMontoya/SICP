    The process that a procedure generates is of course dependent on the rules used
    by the interpreter. As an example, consider the iterative =gcd= procedure given
    above. Suppose we were to interpret this procedure using normal-order
    evaluation, as discussed in Section 1.1.5. (The normal-order-evaluation rule for
    if is described in Exercise 1.5.) Using the substitution method (for normal
    order), illustrate the process generated in evaluating =(gcd 206 40)= and indicate
    the =remainder= operations that are actually performed. How many remainder
    operations are actually performed in the normal-order evaluation of =(gcd 206
    40)=? In the applicative-order evaluation?

Let's follow the evaluation with normal order

```scheme 
(gcd 206 40)

(gcd 40
     (remainder 206 40))
;; execute 1 remainder for the if
(gcd (remainder 206 40)
     (remainder 40 (remainder 206 40)))
;; executes 2 remainder for the if
(gcd (remainder 40 (remainder 206 40))
     (remainder (remainder 206 40) (remainder 40 (remainder 206 40))))
;; executes 4 remainder for the if
(gcd (remainder (remainder 206 40) (remainder 40 (remainder 206 40)))
     (remainder (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40)))))
;; executes 8 remainder for the if
(remainder (remainder 206 40) (remainder 40 (remainder 206 40)))

(remainder 6 (remainder 40 (remainder 206 40)))

(remainder 6 (remainder 40 6))

(remainder 6 4)

2
```

If we count the `remainder` evaluated explicitly in the trace, and the evaluated for the if, in total `remainder` has been evaluated 19 times. Since with) applicative-order, the `remainder` will be evaluated before the `if` statement, the evaluations due to `if` won't occur, and won't be accumulation of`remainder` either. This will reduce the evaluation of `remainder` to 4

```scheme 
(gcd 206 40)

(gcd 40 (remainder 206 40))

(gcd 40 6)

(gcd 6 (remainder 40 6))

(gcd 6 4)

(gcd 4 (remainder 6 4))

(gcd 4 2)

(gcd 2 (remainder 4 2))

(gcd 2 20

2
```

