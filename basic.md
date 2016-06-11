# Basic Operations

Orange provides your common basic mathematical operations to use between values:

	addition       -> expression "+" expression
	subtraction    -> expression "-" expression
	division       -> expression "/" expression
	multiplication -> expression "*" expression
	remainder      -> expression "%" expression

Orange also gives you basic bitwise operators:

	bit_or         -> expression "|" expression
	bit_and        -> expression "&" expression
	bit_xor        -> expression "^" expression
	bitshift_left  -> expression "<<" expression
	bitshift_right -> expression ">>" expression

These operations equate to _expressions_, which are statements with values. A regular non-expression statement ends in a semicolon.

For example, `5 + 3` is an expression with the value of `8`, whereas `5 + 3;` is a statement that evaluated to `8`, but has no referencable value. Note that this doesn't mean code like `a = 5 + 3;` won't work, since that evaluates to `(a = (5 + 3));`.

## Variables

	var_decl -> type variable_name ( "=" expression )?

In Orange, variables are mutable named values. They can be made immutable if their type is `const data_type`.

Variables are a type of `lvalue`, which means that they are valid on the left-hand side of an expression that assigns. The list of expressions that require an l-value operate similary to the ones that do not:

	expression     -> lvalue | const_value | other_expression
	assign         -> lvalue "=" expression
	plus_assign    -> lvalue "+=" expression
	minus_assign   -> lvalue "-=" expression
	times_assign   -> lvalue "*=" expression
	div_assign     -> lvalue "/=" expression
	rem_assign     -> lvalue "%=" expression
	bsleft_assign  -> lvalue "<<=" expression
	bsright_assign -> lvalue ">>=" expression
	or_assign      -> lvalue "|=" expression
	and_assign     -> lvalue "&=" expression
	xor_assign     -> lvalue "^=" expression

Some example of creating variables are:

    int aNumber = 953;
    float some_float = 53.2;
    uint32 aHexNum = 0xDEADBEEFu32;
	var a_variable = 0b1111000011111u16;

If a variable in Orange is given an initial value, the typename may be omitted and replaced with `var`.

Using the previous example, `var aNumber = 953;` is valid but `var aNumber;` is not, since the latter does not have an initial value, and Orange can't determine the type of aNumber.

### Shadowing Variables

A variable can be redefined with a new type at any point:

    int myVariable = 3;
    float myVariable = 2.1;
    // any reference to myVariable now uses the redefined float

Unlike the C-family of languages, shadowing variables is perfectly valid in the original scope that the shadowed variable is declared.

## Boolean Expressions

Another class of expressions are ones that resolve to a boolean `false` or `true` value:

	boolean_expr   -> less_than | greater_than | less_eq_to
	boolean_expr   -> greater_eq_to | not_equal | equal
	boolean_expr   -> boolean_and | boolean_or

	less_than      -> expression "<" expression
	greater_than   -> expression ">" expression
	less_eq_to     -> expression "<=" expression
	greater_eq_to  -> expression ">=" expression
	not_equal      -> expression "!=" expression
	equal          -> expression "=" expression
	boolean_and    -> boolean_expr "&&" boolean_expr
	boolean_or     -> boolean_expr "||" boolean_expr

Note that those last two operations requore both sides of the expression to be boolean values, since `true || false` is a valid statement, but `3 || 5` wouldn't make much sense. Unlike C, non-greater values are not truthy values.

## Unary Expressions

The final class of expressions are those that operate on a single lvalue.

	pre_increment -> "++" lvalue
	post_increment -> lvalue "++"
	pre_decrement -> "--" lvalue
	post_decrement -> lvalue "--"
	deference -> "*" lvalue
	reference -> "&" lvalue

The pre-increment and pre-decrement's value will be the modified lvalue, whereas the post-increment and post-decrement will be equal to the lvalue before modification.

For more information on deference and reference, see [Pointers](pointers.md).

## Interpreted Strings

Orange supports interpreting expressions inside of a string if a sequence of `${expression}` is found. The expression will be evaluated and concatenated in the proper place to the string at runtime.

    var year = 2016; 
    "I think ${year} will be a great year!"; 
    "I think ${ year + 1 } will be even better!";
    
If you want to put a `${` inside of a string, escape the dollar sign with `\`.