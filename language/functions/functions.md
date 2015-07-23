# Functions
**STATUS**: Implemented

    def _functionName_ ( [[ _arg1_ [[, _arg2_ ]]* [[, ...]] ]] ) [ -> _returnType_ ]
        [[ _code_ ]]
        [[ return [[ _expression_ ]] ]]
    end

The syntax for a function here may be confusing here, but all it states is that:

1. A function must have a name.
2. A function can have zero or more arguments
3. The last argument can be ..., indicating that it uses a variable amount of arguments.
4. A function can have a return statement at any point, which can return an expression.
5. A function can provide a return type. It is optional as the return type is induced from the return statements.

The arguments for a function can just be a variable name. If this is the case, generics are employed. Otherwise, if you provide an argument with a type, then the function is not generic and the types of the parameters will not change. 

Calling a function is very easy: 

    _functionName_ ( _argList_ )

Functions can also be nested in Orange.

    def foo()
        def bar()
            return 1
        end

        return bar()
    end

    foo() 

Note that with nested functions, we don't have access to `bar` from the global scope!

## Multiple functions with the same name 
**STATUS**: [Implemented](https://github.com/rfratto/orange/commit/d6c5ea), but not merged

Orange supports having multiple functions with the same name, as long as they have different parameters.