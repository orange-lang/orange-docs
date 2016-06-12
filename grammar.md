# Grammar Summary

This is a compilation of the various bits of grammar defined throughout this documentation.

	statement  -> var_decl term | expression term | class | block
	statement  -> break_stmt term | continue_stmt term
	statement  -> yield_stmt term | function | aggregate | extern_fn term
	statement  -> interface | destructor | namespace term | import term
	statement  -> getter | setter | property

	expression -> addition | subtraction | division | multiplication
	expression -> remainder | bit_or | bit_and | bit_xor | bitshift_left
	expression -> bitshift_right | assign | plus_assign | minus_assign
	expression -> times_assign | div_assign | rem_assign | bsleft_assign
	expression -> bsright_assign | or_assign | and_assign | xor_assign
	expression -> less_than | greater_than | less_eq_to | greater_eq_to
	expression -> not_equal | equal | boolean_and | boolean_or
	expression -> pre_increment | post_increment | pre_decrement
	expression -> post_decrement | deference | reference | type_cast
	expression -> array_expression | array_access_expr
	expression -> inclusive_range_expr | exclusive_range_expr
	expression -> tuple_expr | access_tuple | named_expr | temp_tuple_elem
	expression -> if | for_loop | foreach | while | forever | do_while
	expression -> switch | fn_call | new | delete
	expression -> "(" expression ")"

	term       -> ";"

	var_decl       -> type variable_name ( "=" expression )?

	addition       -> expression "+" expression
	subtraction    -> expression "-" expression
	division       -> expression "/" expression
	multiplication -> expression "*" expression
	remainder      -> expression "%" expression

	bit_or         -> expression "|" expression
	bit_and        -> expression "&" expression
	bit_xor        -> expression "^" expression
	bitshift_left  -> expression "<<" expression
	bitshift_right -> expression ">>" expression

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

	less_than      -> expression "<" expression
	greater_than   -> expression ">" expression
	less_eq_to     -> expression "<=" expression
	greater_eq_to  -> expression ">=" expression
	not_equal      -> expression "!=" expression
	equal          -> expression "=" expression
	boolean_and    -> expression "&&" expression
	boolean_or     -> expression "||" expression

	pre_increment  -> "++" lvalue
	post_increment -> lvalue "++"
	pre_decrement  -> "--" lvalue
	post_decrement -> lvalue "--"
	deference      -> "*" lvalue
	reference      -> "&" lvalue

	type_cast      -> "(" type ")" expression

	class          -> "class" identifier (":" super_list)?
	super_list     -> identifier? | identififer ("," identifier)*
	partial_class  -> "partial" class

    type                 -> array
	array_type           -> data_type "[" expression "]"

	array_expression     -> "[" arr_elements "]"
	arr_elements         -> arr_single_element | arr_mult_elements
	arr_single_element   -> expression?
	arr_mult_elements    -> expression ("," expression)*

	array_access_expr    -> expression "[" expression "]"

	inclusive_range_expr -> "[" expression "..." expression "]"
	exclusive_range_expr -> "[" expression ".." expression "]"

	tuple_type   -> "(" type ("," type )* ")"
	tuple_expr   -> "(" tuple_value ("," tuple_value )* ","? " ")"
	tuple_value  -> expression
	access_tuple -> tuple_expr "." (0 ... infinity)

	type        -> tuple_type

	tuple_value -> named_expr
	named_expr  -> name ":" expression

	var_decl        -> tuple_type "(" name ("," name)* ","? ")"
	temp_tuple_elem -> "_"

	block     -> "{" (statement | expression)* "}"
	block     -> ":" (statement | expression)

	if         -> "if" "(" expression ")" (elif | else)? block
	elif       -> "elif" "(" expression ")" (elif | else)? block
	else       -> "else" block

	for_loop  -> "for" "(" exprression ";" expression ";" expression
	             ")" block

	foreach    -> "foreach" "(" var_decl "in" expression ")" block

	while      -> "while" "(" expression ")" block

	forever    -> "forever" block

	do_while   -> "do" block "while" "(" expression ")"

	break_stmt    -> "break"
	continue_stmt -> "continue"

	switch         -> "switch" "(" expression ")" switch_block
	switch_block   -> "{" switch_match ("," switch_match)* "}"
    switch_match   -> switch_pattern "," switch_pattern "=>" switch_value
    switch_value   -> expression | "{" ( statement | expression )* "}"
    switch_pattern -> ("_" | expression )

	yield_stmt -> "yield" expression

    function   -> "def" fn_name? "(" param_list ")" ("->" type)? block
    param_list -> var_decl? | var_decl ("," var_decl)*

    fn_call    -> expression "(" arg_list ")"
    arg_list   -> arg? | arg ("," arg)*
    arg        -> expression | named_expr

    aggregate -> "aggregate" block

    extern_fn -> "extern" "def" fn_name "(" param_list ")" "->" type
	interface -> "interface" identifier block

	destructor -> "~" identifier "(" ")" block
	identifier -> "operator" operator

	namespace -> "namespace" identifier block?
	import    -> "import" identifier

	new        -> "new" identifier
	delete     -> "delete" expression

	privacy_level -> "private" | "protected" | "public"

	getter    -> "get" block
	setter    -> "set" block

	property  -> type identifier block
