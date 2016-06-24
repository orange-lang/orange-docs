# Basic Operations

Orange provides your common basic mathematical operations to use between values:

	term           -> "\n" | ";"
	statement      -> expression

	addition       -> expression "+" expression
	subtraction    -> expression "-" expression
	division       -> expression "/" expression
	multiplication -> expression "*" expression
	remainder      -> expression "%" expression

	expression     -> addition | subtraction | division | multiplication
	expression     -> remainder
	expression     -> "(" expression ")"

Orange also gives you basic bitwise operators:

	bit_or         -> expression "|" expression
	bit_and        -> expression "&" expression
	bit_xor        -> expression "^" expression
	bitshift_left  -> expression "<<" expression
	bitshift_right -> expression ">>" expression

	expression     -> bit_or | bit_and | bit_xor | bitshift_left
	expression     -> bitshift_right

These operations equate to _expressions_, which are statements with values.


## Variables

	statement   -> var_decl
	var_decl    -> "const"? "var" identifiers (":" type_list)?
	               ( "=" expression )?
	identifiers -> identifier | "(" identifier ("," identifier)* ")"
	type_list   -> type ("," type)*

In Orange, variables are mutable named values. They can be made immutable if the variable is prefixed with "const".

Variables are a type of `lvalue`, which means that they are valid on the left-hand side of an expression that assigns. The list of expressions that require an l-value operate similary to the ones that do not:

	assign         -> expression "=" expression
	plus_assign    -> expression "+=" expression
	minus_assign   -> expression "-=" expression
	times_assign   -> expression "*=" expression
	div_assign     -> expression "/=" expression
	rem_assign     -> expression "%=" expression
	bsleft_assign  -> expression "<<=" expression
	bsright_assign -> expression ">>=" expression
	or_assign      -> expression "|=" expression
	and_assign     -> expression "&=" expression
	xor_assign     -> expression "^=" expression

	expression     -> assign | plus_assign | minus_assign | times_assign
	expression     -> div_assign | rem_assign | bsleft_assign | bsright_assign
	expression     -> or_assign | and_assign | xor_assign

Some example of creating variables are:

	var aNumber: int = 953
	var some_float: float = 53.2
	var aHexNum: uint32 = 0xDEADBEEFu32
	var a_variable = 0b111100001111u16

If a variable in Orange is given an initial value, specifying a typename may be omitted.

Using the previous example, `var aNumber = 953` is valid but `var aNumber` is not, since the latter does not have an initial value, and Orange can't determine the type of aNumber.

Note that you can declare multiple variables with the same statement. If you wish to give these initial value to the statement, you must supply an initial value to each variable declared. This can be done by passing in a [tuple](collections.md#tuples) as the initial value.

	var a, b: int, float = (54, 72.98f)
	// or
	var a, b = (54, 72.98f)

### Shadowing Variables

A variable can be redefined with a new type at any point:

	var myVariable: int = 3
	var myVariable: float = 2.1
    // any reference to myVariable now uses the redefined float

Unlike the C-family of languages, shadowing variables is perfectly valid in the original scope that the shadowed variable is declared.

## Boolean Expressions

Another class of expressions are ones that resolve to a boolean `false` or `true` value:

	less_than      -> expression "<" expression
	greater_than   -> expression ">" expression
	less_eq_to     -> expression "<=" expression
	greater_eq_to  -> expression ">=" expression
	not_equal      -> expression "!=" expression
	equal          -> expression "==" expression
	boolean_and    -> expression "&&" expression
	boolean_or     -> expression "||" expression

	expression     -> less_than | greater_than | less_eq_to
	expression     -> greater_eq_to | not_equal | equal
	expression     -> boolean_and | boolean_or

Note that those last two operations requore both sides of the expression to be boolean values, since `true || false` is a valid statement, but `3 || 5` wouldn't make much sense. Unlike C, non-greater values are not truthy values.

## Unary Expressions

The final class of expressions are those that operate on a single lvalue.

	pre_increment  -> "++" expression
	post_increment -> expression "++"
	pre_decrement  -> "--" expression
	post_decrement -> expression "--"
	deference      -> "*" expression
	reference      -> "&" expression
	not_expr       -> "!" expression
	negate_expr    -> "-" expression

	expression     -> pre_increment | post_increment | pre_decrement
	expression     -> post_decrement | deference | reference | not_expr
	expression     -> negate_expr

The pre-increment and pre-decrement's value will be the modified lvalue, whereas the post-increment and post-decrement will be equal to the lvalue before modification.

For more information on deference and reference, see [Pointers](pointers.md).

## Interpreted Strings

Orange supports interpreting expressions inside of a string if a sequence of `${expression}` is found. The expression will be evaluated and concatenated in the proper place to the string at runtime.

    var year = 2016
    "I think ${year} will be a great year!"
    "I think ${ year + 1 } will be even better!"

If you want to put a `${` inside of a string, escape the dollar sign with `\`.
