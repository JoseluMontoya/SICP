    Define a procedure =double= that takes a procedure of one argument as argument and returns a procedure that applies the original procedure twice. For example, if =inc= is a procedure that adds 1 to its argument, then =(double inc)= should be a procedure that adds 2. What value is returned by
    #+begin_src scheme
    (((double (double double)) inc) 5)
    #+end_src

```scheme 
(define (double f) (lambda (x) (f (f x))))
```

Let's write the trace to see what the expression yields

```scheme 
(((double
   (double
    double))
  inc) 5)

(((double
   (lambda (x) (double
                (double
                 x))))
  inc) 5)

(((lambda (x) (double
               (double
                (double
                 (double x)))))
  inc)
 5)

((double
  (double
   (double
    (double
     inc))))
 5)

((double
  (double
   (double
    (lambda (x)
      (inc
       (inc x))))))
 5)

((double
  (double
    (lambda (x)
      (inc
       (inc
        (inc
         (inc x)))))))
 5)

((double
    (lambda (x)
      (inc
       (inc
        (inc
         (inc
          (inc
           (inc
            (inc
             (inc x))))))))))
 5)

((lambda (x)
   (inc
    (inc
     (inc
      (inc
       (inc
        (inc
         (inc
          (inc
           (inc
            (inc
             (inc
              (inc
               (inc
                (inc
                 (inc
                  (inc x)))))))))))))))))
 5)

21
```

