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

The arguments for a function require a type, but `var` can be used as a type
to indicate a generic function.  

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

Note that with nested functions, we don't have access to `bar` from the global
scope!

## Inline Functions

Orange also supports inline (read: one-line) functions:

    def add(int a, int b): return a + b 

## Multiple functions with the same name

Orange supports having multiple functions with the same name, as long as they
have different parameters.  
