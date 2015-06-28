# Ternary Operator
**STATUS**: Implemented

The ternary operator works exactly like it does in C:

    _condition_ ? _true expression_ : _false expression_ 

For example, 

    var a = (3 == 5) ? true : false

In this example, parenthesis were added to the condition to improve readability. `a` will be `true` if `3 == 5`. Since it doesn't, `a == false`.

Casting occurs on each potential value of the ternary operator. If you were to do the following expression:

    var a = true ? 3 : 5.0 

It would compile down to

    var a = true ? 3.0 : 5.0

As `double`. have a higher type precedence than `int`s. The types must be compatible, however. You can not mix, say, arrays and numbers.

    var a = true ? [0, 1, 2] : 5.03     # this is invalid! 
