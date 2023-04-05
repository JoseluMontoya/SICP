> Ben Bitdiddle has invented a test to determine whether the interpreter he is faced with is using applicative-order evaluation or normal-order evaluation. He defines the following two procedures:
> ```scheme
> (define (p) (p))
> (define (test x y)
>   (if (= x 0) 0 y))
> ```
> Then he evaluates the expression
> ```scheme
> (test 0 (p))
> ```
> What behavior will Ben observe with an interpreter that uses applicative-order evaluation? What behavior will he observe with an interpreter that uses normal-order evaluation? Explain your answer. (Assume that the evaluation rule for the special form if is the same whether the interpreter is using normal or applicative order: The predicate expression is evaluated first, and the result determines whether to evaluate the consequent or the alternative expression.)
Correction of the markdown

With applicative-order evaluation, the first step that the interpreter takes is to evaluate the inner most procedures. In this case, that includes `p`, which evaluates to itself. Therefore, the test will never end.

On the other hand, with normal order evaluation, the first step is to expand everything, which includes `test`. Then, as the question statement says, `if` first evaluates the predicate, and the decides what to execute. Because of that, the procedure will return 0, and not get stuck.

