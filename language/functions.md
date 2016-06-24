# Functions

    function   -> "def" fn_name? generics? "(" param_list ")" ("->" type)? block
    type       -> func_type
    func_type  -> "(" type_list? ")" "->" type
    param_list -> var_decl? | var_decl ("," var_decl)*

    type_list  -> type (COMMA type)*

    statement  -> function

Functions are anonymous or named expressions that can be called at any point to execute code. The parameters in function signatures work like normal variable declarations, so they can be given initial values and ommited from an argument list upon calling the function.

Note that if a function parameter is declared with an initial value, then all parameters after it must also have an initial value.

The optional type at the end of the function indicates the functions return type. If a return type is specified, a return statement must be present in the function. `yield` is not valid in the context of a function, but implicit returns can still be achieved by using the one-line block `:` syntax.

Here are some examples of functions:

    def add(int a, int b) -> int: a + b

    def subtract(int a, int b) {
        return a - b
    }

    def doNothing() { }

The type of a function is `(type_list) -> type`.

If a function does not return anything, its type is `void`. If void is defined explicitly as the functions return type, `return` can not be used with a value. Implicit `yield` values will execute, but will be ignored.

The body of a function can define other functions, if so desired.

## Calling functions

    fn_call    -> expression "(" arg_list ")"
    arg_list   -> arg? | arg ("," arg)*
    arg        -> expression | named_expr

    expression -> fn_call

Functions can be called by placing the name of the function to call before parenthesis that contain the function arguments. Our `subtract` from the previous example can be called by using `subtract(9, 5)` as an expression.

Note that the arguments can also be specified out-of-order via named expressions. The names must match the name of the parameter of the function. If a named expression is used as an argument, subsequent expressions that are not named will map to the following paramaters after the named one.

All non-optional parameters (i.e., parameters without an initial value) must have their own argument for a function call to be semantically valid.

## Yield and Return

Its worthwhile to touch base base on the differences between `yield` and `return`. `yield` can be present in absolutely any block, and will be used as the value for that block. However, yield does not stop execution of the block (i.e., statements following a yield will always execute). On the other hand, `return` will always stop execution of the function we're currently in.

## Anonymous functions

An anonymous function can be constructed simply by ommitting its function name. Like other functions, it can be used as a value.

    var add = def(int a, int b): a + b
    var res = add(12, 95)

## Aggregate functions

    aggregate -> "aggregate" identifier? block
    statement -> aggregate

Common code for functions can be shared using an aggregate definition:

    aggregate {
       // code and functions
    }

For the following example, pretend a `println` is defined that will print a line to the console. Then:

    aggregate {
       println("Calculating...")
       int result = 0

       def add(int a, int b) {
           result = a + b
           return result
       }

       def subtract(int a, int b) {
           result = a - b
           return result
       }

       // prints the result in a string
       println("Result: ${result}")
    }

Any code before a function will be ran before that function executes. Likewise, any code after a function will run after that function's return statement is called.

Aggregate blocks also define a `value` which represent the return value of the functions. Using `value`, we can replace the previous example with the much simpler code:

    aggregate {
       println("Calculating...")

       def add(int a, int b): a + b
       def subtract(int a, int b): a - b

       println("Result: ${value}")
    }

    var b = 16
    add(3, b)
    // => Calculating...
    // => Result: 19


`value` is _not_ a constant and can be modified, if so desired. However, note that if `value` is used, none of the functions defined in the aggregate block can return `void`. The functions in an aggregate block can, however, have different return types, since the statements inside an aggregate block are just templates.

Note that although aggregate blocks support the one-line block syntax, it's pointless in the context of an aggregate, since aggregate statements are only called when a function declared inside an aggregate is called.

Aggregates can also be named, which is only used for extensions. 

## Calling C functions

    extern_fn -> "extern" "def" fn_name "(" param_list ")" "->" type
    statement -> extern_fn

An external C function can be declared by prefixing the `def` with `extern`. Note that there are some limitations to this:

1. The function name is not optional.
2. Parameters cannot have default values.
3. The type cannot be ommited.

For example, if we wanted to call `printf`:

    extern def printf(char* s, ...) -> int32
    printf("Hello, world! The year is %d\n", 2016)
