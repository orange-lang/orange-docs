# If Statement
**STATUS**: Implemented

    if _condition_
        [[ _code_ ]]
    end

    # or 

    _code_ if _condition_

Like all if statements, the code will be conditionally executed if and only if the condition (which must be a boolean type) is true. 

For example, 

    var a = -6
    a = -a if a < 0

There are also `elif` statements, and `else` statements. Both `elif` and `else` are optional, but I'll provide the full syntax below for completing an `if...elif...else` statement:

    if _condition_
        [[ _code_ ]]
    elif _condition_
        [[ _code_ ]]
    [[ _more elifs, if needed_ ]]
    else 
        [[ _code_ ]]
    end 

Note that there is no one-line form for `elif` and `else` statements.