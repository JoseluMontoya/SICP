    The =good-enough?= test used in computing square roots will not be very effective
    for finding the square roots of very small numbers. Also, in real computers,
    arithmetic operations are almost always performed with limited precision.
    This makes our test inadequate for very large numbers. Explain these statements,
    with examples showing how the test fails for small and large numbers. An
    alternative strategy for implementing =good-enough?= is to watch how guess changes
    from one iteration to the next and to stop when the change is a very small
    fraction of the guess. Design a square-root procedure that uses this kind of end
    test. Does this work better for small and large numbers?

`good-enough?` is going to be bad for small numbers because as the value of `x` gets closer to, in this case, 0.001, the differences between `x` and `(square guess)` are going to be around the same size as `x` itself. For example, if `x` is indeed 0.001, his square root is going to be approximately 0.0316, but `good-enough?` is going to give the green light to values as low as 0.01 (one third of the correct answer) and as big as 0.0439 (1.38 times the original answer) (those aren't exact extreme values because it is an open set, but my point came across).

`good-enough?` is going to be bad for large numbers because, if the precision in the calculations itself is bigger than our threshold because of its size, only if the guess is precisely `x` is `good-enough?` goung to return `#t`. For example, if `guess` has gotten to a point in which the smallest digit is the unit, that means that the only allowed values of`(abs (- (square guess) x))` are going to be the decimals of `x` plus an integer. If thats decimal part is greater than 0.001, its going to be literally imposible for `good-enough?` to return a `#t`.

```scheme 
(define (good-enough? guess impr-guess)
  (< (abs (/ (- guess impr-guess) guess)) 0.1))

(define (sqrt-iter guess x)
  (if (good-enough? guess (improve guess x))
      guess
      (sqrt-iter (improve guess x) x)))
```

