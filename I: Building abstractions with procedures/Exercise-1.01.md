> Below is a sequence of expressions. What is the result printed by the interpreter in response to each expression? Assume that the sequence is to be evaluated in the order in which it is presented.

-   Expression ​#1

```scheme 
    10
```

Because it is only a number, the interpreter will return 10


-   Expression ​#2

```scheme 
    (+ 5 3 4)
```

If we apply + to 5, 3 and 4, we get 5 + 3 + 4 = 12


-   Expression ​#3

```scheme 
    (- 9 1)
```

If we apply - to 9 and 1 we get 9 - 1 = 8


-   Expression ​#4

```scheme 
    (/ 6 2)
```

If we apply / to 6 and 2 we get 6/2 = 3


-   Expression ​#5

```scheme 
    (+ (* 2 4) (- 4 6))
```

First, we evaluate the inner expressions

-   (\* 2 4) = 2 \* 4 = 8
-   (- 4 6) = 4 - 6 = -2

Then, we substitute and evaluate the final one

-   (+ 8 -2) = 8 + -2 = 6


-   Expression ​#6

```scheme :session,"1.1"
    (define a 3)
```

Since we have defined a variable, the interpreter won't return anything


-   Expression ​#7

```scheme :session,"1.1"
    (define b (+ a 1))
```

The interpreter will return the same as in the previous expression: nothing


-   Expression ​#8

```scheme :session,"1.1"
    (+ a b (* a b))
```

The interpreter will calculate first (\* a b) = a \* b = 3 \* 4 = 12, and then (+ a b 12) = a + b + 12 = 3 + 4 + 12 = 19


-   Expression ​#9

```scheme :session,"1.1"
    (= a b)
```

Since a = 3 and b = 4, the interpreter will return #t (False)


-   Expression ​#10

```scheme :session,"1.1"
    (if (and (> b a) (< b (* a b)))
        b
        a)
```

Since b > a and b &lt; (a \* b), what the interpreter will return is 4


-   Expression ​#11

```scheme :session,"1.1"
    (cond ((= a 4) 6)
        ((= b 4) (+ 6 7 a))
        (else 25))
```

a doesn't equal 4, but b does, so the interpreter is going to return 6 + 7 + a = 16


-   Expression ​#12

```scheme :session,"1.1"
    (+ 2 (if (> b a) b a))
```

Since b > a, the interpreter is going to return 2 + b = 6


-   Expression ​#13

```scheme :session,"1.1"
    (* (cond ((> a b) a)
            ((< a b) b)
            (else -1))
    (+ a 1))
```

Since a &lt; b, the cond is going to evaluate t b, so the interpreter is gonna return (\* b (+ a 1)) = b \* (a + 1) = 16


