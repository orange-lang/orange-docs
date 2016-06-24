# Grammar Summary

This is a compilation of the various bits of grammar defined throughout this documentation.

	program              -> statements?
	statements           -> statement (term statement)*

	term                 -> "\n"

	type                 -> tuple_type | array_type | pointer_type | func_type
	type                 -> "int" | "uint" | "int8" | "int16" | "int32"
	type                 -> "int64" | "uint8" | "uint16" | "uint32"
	type                 -> "uint64" | "float" | "double" | "var" | "void"
	type                 -> identifier | ref_type

	identifier           -> "_"? ( alphas | "_" ) ( alphanumerics | "_" )*
	identifier           -> "operator" operator

	alphas               -> ( "A" ... "Z" | "a" ... "z" )
	numerics             -> "0" ... "9"
	alphanumerics        -> alphas | numerics

	long_block           -> "{" statements? "}"
	short_block          -> ":" statement
	block                -> long_block | short_block

	statement            -> var_decl | class | long_block
	statement            -> break_stmt | continue_stmt
	statement            -> yield_stmt | function | aggregate | struct
	statement            -> extern_fn
	statement            -> interface | destructor | namespace
	statement            -> import | extension
	statement            -> getter | setter | property | enum | expr_statement

	expr_statement       -> expression ";"?

	expression           -> binop_expr | unary_expr | value | control
	expression           -> access_tuple | named_expr | temp_tuple_elem
	expression           -> fn_call | new | delete | member_access | "this"
	expression           -> "(" expression ")" | ternary

	value                -> array_expression | array_access_expr
	value                -> inclusive_range_expr | exlusive_range_expr
	value                -> tuple_expr

	control              -> if | for_loop | foreach | while | forever | do_while
	control              -> switch

	binop_expr           -> addition | subtraction | division | multiplication
	binop_expr           -> remainder | bit_or | bit_and | bit_xor
	binop_expr           -> bitshift_left
	binop_expr           -> bitshift_right | assign | plus_assign | minus_assign
	binop_expr           -> times_assign | div_assign | rem_assign
	binop_expr           -> bsleft_assign
	binop_expr           -> bsright_assign | or_assign | and_assign | xor_assign
	binop_expr           -> less_than | greater_than | less_eq_to
	binop_expr           -> greater_eq_to
	binop_expr           -> not_equal | equal | boolean_and | boolean_or

	unary_expr           -> pre_increment | post_increment | pre_decrement
	unary_expr           -> post_decrement | deference | reference

	var_decl             -> type variable_name (":" expression)?
	                        ( "=" expression )?

	addition             -> expression "+" expression
	subtraction          -> expression "-" expression
	division             -> expression "/" expression
	multiplication       -> expression "*" expression
	remainder            -> expression "%" expression

	bit_or               -> expression "|" expression
	bit_and              -> expression "&" expression
	bit_xor              -> expression "^" expression
	bitshift_left        -> expression "<<" expression
	bitshift_right       -> expression ">>" expression

	assign               -> expression "=" expression
	plus_assign          -> expression "+=" expression
	minus_assign         -> expression "-=" expression
	times_assign         -> expression "*=" expression
	div_assign           -> expression "/=" expression
	rem_assign           -> expression "%=" expression
	bsleft_assign        -> expression "<<=" expression
	bsright_assign       -> expression ">>=" expression
	or_assign            -> expression "|=" expression
	and_assign           -> expression "&=" expression
	xor_assign           -> expression "^=" expression

	less_than            -> expression "<" expression
	greater_than         -> expression ">" expression
	less_eq_to           -> expression "<=" expression
	greater_eq_to        -> expression ">=" expression
	not_equal            -> expression "!=" expression
	equal                -> expression "==" expression
	boolean_and          -> expression "&&" expression
	boolean_or           -> expression "||" expression

	pre_increment        -> "++" expression
	post_increment       -> expression "++"
	pre_decrement        -> "--" expression
	post_decrement       -> expression "--"
	deference            -> "*" expression
	reference            -> "&" expression

	type_cast            -> "(" type ")" expression

	enum                 -> flags? "enum" identifier "{" enum_values? "}"
	enum_values          -> enum_value ("," enum_value)*
	enum_value           -> identifier ( "(" param_list? ")" )?
	enum_access          -> identifier "." identifier
	enum_pattern         -> member_access "(" arg_list? ")"

	class                -> flags? "class" identifier (":" super_list)?
	super_list           -> identififer ("," identifier)*
	partial_class        -> "partial" class
	member_access        -> identifier "." identifier

	struct               -> flags? "struct" identifier block

	array_type           -> data_type "[" expression "]"
	array_expression     -> "[" arr_elements "]"
	arr_elements         -> arr_single_element | arr_mult_elements
	arr_single_element   -> expression?
	arr_mult_elements    -> expression ("," expression)*

	array_access_expr    -> expression "[" expression "]"

	inclusive_range_expr -> "[" expression "..." expression "]"
	exclusive_range_expr -> "[" expression ".." expression "]"

	tuple_type           -> "(" type ("," type )* ")"
	tuple_expr           -> "(" tuple_value ("," tuple_value )* ","? " ")"
	tuple_value          -> expression
	access_tuple         -> tuple_expr "." (0 ... infinity)
	tuple_value          -> named_expr

	named_expr           -> name ":" expression

	temp_tuple_elem      -> "_"

	if                   -> "if" "(" expression ")" block (elif | else)?
	elif                 -> "elif" "(" expression ")" block (elif | else)?
	else                 -> "else" block

	ternary              -> "(" expression ")" "?" expression ":" expression

	for_loop             -> "for" "(" exprression ";" expression ";"
	                        expression ")" block
	foreach              -> "foreach" "(" var_decl "in" expression ")" block
	while                -> "while" "(" expression ")" block
	forever              -> "forever" block
	do_while             -> "do" block "while" "(" expression ")"

	switch               -> "switch" "(" expression ")" switch_block
	switch_block         -> "{" switch_match ("," switch_match)* "}"
    switch_match         -> switch_pattern ("," switch_pattern)* ":"
	                        switch_value
    switch_value         -> expression | "{" ( statement | expression )* "}"
    switch_pattern       -> ("_" | expression ) | enum_pattern

	break_stmt           -> "break"
	continue_stmt        -> "continue"
	yield_stmt           -> "yield" expression

    func_type            -> "(" type_list? ")" "->" type
    type_list            -> type (COMMA type)*

    function             -> flags? "def" fn_name? generics? "(" param_list? ")"
	                        ("->" type)? block
    extern_fn            -> flags? "extern" "def" fn_name "(" param_list? ")"
	                        "->" type
    param_list           -> var_decl ("," var_decl)*

    fn_call              -> expression "(" arg_list? ")"
    arg_list             -> arg ("," arg)*
    arg                  -> expression | named_expr

	generics             -> "<" generic_values? (":" constraints)? ">"
	generic_values       -> IDENTIFIER ("," IDENTIFIER)*

	constraints          -> constraint ("," constraint)*
	constraint           -> "where" IDENTIFIER "=" type_constraint
	type_constraint      -> "class" | "new()" | identifier
	type_constraint      -> "data" type | type

    aggregate            -> "aggregate" block

	interface            -> "interface" identifier block

	constructor          -> identifier "(" param_list? ")" block
	destructor           -> "~" identifier "(" ")" block

	namespace            -> "namespace" identifier block?
	import               -> "import" identifier

	new                  -> "new" identifier
	delete               -> "delete" expression
	pointer_type         -> type "*"
	ref_type             -> type "&"

	flags                -> flag+
	flag                 -> privacy | virtual | "partial"
	virtual              -> "virtual" | "final"
	privacy              -> "private" | "protected" | "public"

	getter               -> "get" block
	setter               -> "set" block

	extension            -> "extend" identifier (":" super_list)? block

	property             -> flags? "property" identifier "->" type block
