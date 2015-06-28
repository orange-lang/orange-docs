# For Loops 
**STATUS**: Implemented

`for` loops, like in C, have an initializer, condition, and afterthought component before the body of code. 

    for ( _initializer_ ; _condition_ ; _afterthought_ )
        [[ _code_ ]] 
    end 

For example:

    var sum = 0
    
    for (var i = 0; i < 10; i++)
        sum += i
    end 

Will sum up all of the numbers from `0` to `10`. Note that the condition component of the for loop must be a boolean value, but the initializer and afterthought can be any statement. 

Orange also supports a single-line `for` loop where the body is placed before the `for` component:

    _code_ for ( _initializer_ ; _condition_ ; _afterthought_ )

Or, with our example:

    var sum = 0
    sum += i for (var i = 0; i < 10; i++)

