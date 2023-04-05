> We saw in Section 1.3.3 that attempting to compute square roots by naively
> finding a fixed point of $y \matpsto x/y$ does not converge, and that this can
> be fixed by average damping. The same method works for finding cube roots as
> fixed points of the average-damped $y \mapsto x/y^2$. Unfortunately, the process
> does not work for fourth roots (a single average damp is not enough to make a
> fixed-point search for $y \mapsto x/y^3$ converge). On the other hand, if we
> average damp twice (i.e., use the average damp of the average damp of $y \mapsto
> x/y^3$) the fixed-point search does converge. Do some experiments to determine
> how many average damps are required to compute $n^{th}$ roots as a fixed-point
> search based upon repeated average damping of $y \mapsto x/y^{n−1}$. Use this to
> implement a simple procedure for computing $n^{th}$ roots using =fixed-point=,
> =average-damp=, and the =repeated= procedure of Exercise 1.43. Assume that any
> arithmetic operations you need are available as primitives.
```scheme
(define tolerance 0.00001)

(define (fixed-point f first-guess)
  (define (close-enough? v1 v2)
    (< (abs (- v1 v2))
       tolerance))
  (define (try guess)
    (let ((next (f guess)))
      (if (close-enough? guess next)
          next
          (try next))))
  (try first-guess))

(define (average x y)
  (/ (+ x y) 2))

(define (average-damp f)
  (lambda (x) (average x (f x))))

(define (fixed-point-of-transform g transform guess)
  (fixed-point (transform g) guess))

(define (compose f g) (lambda (x) (f (g x))))

(define (repeated f n)
  (define (repeated-iter f-iter n)
    (if (= n 0)
        f-iter
        (repeated-iter (compose f f-iter) (- n 1))))
  (repeated-iter (lambda (x) x) n))

(define (square x)
  (fixed-point (lambda (y) (/ x y)) 1))

(square 4)
```

