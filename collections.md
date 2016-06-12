# Collections

A list of values in Orange can be created by appending an array-specifier to the data type when creating a variable. For example, `int[5]` is an array of 5 integers.

    type               -> array
	array_type         -> data_type "[" expression "]"

	array_expression   -> "[" arr_elements "]"
	arr_elements       -> arr_single_element | arr_mult_elements
	arr_single_element -> expression?
	arr_mult_elements  -> expression ("," expression)*

	array_access_expr  -> expression "[" expression "]"

	expression         -> array_expression | array_access_expr

Assigning an initial list of values to an array variable is also done using the square-bracket syntax:

    int[5] myList = [0, 1, 2, 3, 4];
    // or
    var myList = [0, 1, 2, 3, 4];
	var emptyList = [];
	var listOneElement = [5.3f];

When you want to access an individual element of the array, you return once again to the square-bracket syntax:

    myList[0]; // first element in myList
    myList[n]; // nth element in myList

The size of an array can be omitted if it is given an initial value, or if it is a parameter to a function. That is to say, `int[] myList;` is not valid but `int[] myList = [0,1,2];` is.

Note that all elements of an array must have valid types upon declaration and assigning new values. Some types will be automatically up-casted. See [Type Casting](casting.md).


## Array range

	inclusive_range_expr -> "[" expression "..." expression "]"
	exclusive_range_expr -> "[" expression ".." expression "]"

	expression           -> inclusive_range_expr | exclusive_range_expr

An array range can be created by using `..` for an exclusive range, or `...` for an inclusive range. For example, `0 .. 5` will be `[0, 1, 2, 3, 4]` and `0 ... 5` will be `[0, 1, 2, 3, 4, 5]`

It is important to note that using an array range will actually create the array and all of its elements in memory, so be wary about expressions like `[0 ... n]` if n is a really large number!

## Tuples


	tuple_type   -> "(" type ("," type )* ")"
	tuple_expr   -> "(" tuple_value ("," tuple_value )* ","? " ")"
	tuple_value  -> expression
	access_tuple -> tuple_expr "." (0 ... infinity)

	type         -> tuple_type
	expression   -> tuple_expr | access_tuple

A tuple is a collection of a set of values whose components may be different types. They are created by grouping values with parenthesis: `(a, b, c)`. A tuples size is not limited, but cannot be increased at runtime. Accessing members of a tuple is done using the `.` syntax:

    (string, int) tuple = ("dog", 2016);
    // tuple.0 == "dog"
    // tuple.1 == 2016

A tuple of a single element must have a trailing comma: `(a,)`. This is to avoid confusion with expressions where parenthesis are used, like `(5 + 3) * 2`.

## Named Tuples

	tuple_value -> named_expr
	named_expr  -> name ":" expression
	expression  -> named_expr

Tuples may have named elements, which can be used as substitute for using offsets to access tuple members:

    var tuple = (animal: "dog", year: 2016);
    // tuple.animal == tuple.0 == "dog"
    // tuple.year == tuple.1 == 2016

## Deconstructing Tuples

	var_decl        -> tuple_type "(" name ("," name)* ","? ")"
	temp_tuple_elem -> "_"

	expression      -> temp_tuple_elem

Tuples, like variables, are also lvalues. They can appear on the lefthand side of an assignment operation. Note that when used as an lvalue, each of the tuples components must also be lvalues. Using them as lvalues will deconstruct the tuple:

    var (a, b) = (1, 2); // a == 1, b == 2
    (a, b) += (5, 25); // a += 5, b += 25

When a tuple is deconstructed, `_` can be used as a throwaway value.

    var (_, year) = ("dog", 2016); // only assign 2016 to year, ignore "dog"

Using tuples stored into a variable can also be used as an lvalue:

 	var rover = (name: "Rover", age: 4);
	rover += (_, 1);
	// rover.name == "Rover"
	// rover.age == 5
