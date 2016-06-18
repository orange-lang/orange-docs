# Grammar

This file outlines the BNF grammar that Orange will use for its parser. It is a simplified version of [Grammar Summary](grammar_summary.md).

	program              -> opt_statements

	opt_statements       -> statements | %epsilon
	statements           -> statement statements'
	statements'          -> TERM statement | %epsilon

	term                 -> SEMICOLON | NEWLINE

	type                 -> tuple_type | array_type | pointer_type | func_type
	type                 -> INT | UINT | INT8 | INT16 | INT32 | INT64
	type                 -> UINT8 | UINT16 | UINT32 | UINT64
	type                 -> FLOAT | DOUBLE | VAR | VOID | full_id

	identifier           -> namespace_id | operator_id
	full_id              -> IDENTIFIER full_id'
	full_id'             -> DOT identifier | %epsilon
	operator_id          -> OPERATOR operator

	long_block           -> OPEN_CURLY opt_statements CLOSE_CURLY
	short_block          -> COLON statement
	block                -> long_block | short_block

	statement            -> var_decl | class | long_block
	statement            -> break_stmt | continue_stmt
	statement            -> yield_stmt | function | aggregate | struct
	statement            -> extern_fn
	statement            -> interface | destructor | namespace
	statement            -> import
	statement            -> getter | setter | property | enum | expr_statement

	expr_statement       -> expresssion expr_statement'
	expr_statement'      -> SEMICOLON | %epsilon

	expression           -> binop_expr | unary_expr | value | control
	expression           -> access_tuple | named_expr | temp_tuple_elem
	expression           -> fn_call | new | delete | member_access | THIS
	expression           -> OPEN_PAREN expression CLOSE_PAREN | ternary
	expression           -> type_cast | identifier

	value                -> array_expression | array_access_expr
	value                -> inclusive_range_expr | exlusive_range_expr
	value                -> tuple_expr

	control              -> if | for_loop | foreach | while | forever | do_while
	control              -> switch

	binop_expr           -> expression binop expression
	binop                -> PLUS | MINUS | DIVIDE | TIMES | REMAINDER
	binop                -> BIT_OR | BIT_AND | BIT_XOR | SHIFT_LEFT
	binop                -> SHIFT_RIGHT | ASSIGN | PLUS_ASSIGN
	binop                -> MINUS_ASSIGN | TIMES_ASSIGN | DIVIDE_ASSIGN
	binop                -> REMAINDER_ASSIGN | SHIFT_LEFT_ASSIGN
	binop                -> SHIFT_RIGHT_ASSIGN | BIT_OR_ASSIGN
	binop                -> BIT_AND_ASSIGN | BIT_XOR_ASSIGN | LESS_THAN
	binop                -> GREATER_THAN | LEQ | GEQ | NEQ | EQUALS
	binop                -> AND | OR | DOT

	unary_expr           -> pre_increment | post_increment | pre_decrement
	unary_expr           -> post_decrement | deference | reference

	var_decl             -> type variable_name opt_size opt_value
	opt_size             -> COLON expression | %epsilon
	opt_value            -> ASSIGN expression | %epsilon

	pre_increment        -> INCREMENT expression
	post_increment       -> expression INCREMENT
	pre_decrement        -> DECREMENT expression
	post_decrement       -> expression DECREMENT
	deference            -> TIMES expression
	reference            -> BIT_AND expression

	type_cast            -> OPEN_PAREN type CLOSE_PAREN expression

	enum                 -> flags enum_base | enum_base
	enum_base            -> ENUM full_id OPEN_CURLY opt_enum_values
	                        CLOSE_CURLY
	opt_enum_values      -> enum_values | %epsilon
	enum_values          -> enum_value enum_values'
	enum_values'         -> COMMA enum_values
	enum_value           -> IDENTIFIER opt_enum_params
	opt_enum_params      -> OPEN_PAREN param_list CLOSE_PAREN | %epsilon
	enum_patterm         -> full_id OPEN_PAREN arg_list CLOSE_PAREN

	class                -> flags base_class | base_class
	base_class           -> CLASS IDENTIFIER opt_supers
	opt_supers           -> COLON super_list | %epsilon
	super_list           -> full_id super_list'
	super_list'          -> COMMA super_list
	partial_class        -> flags PARTIAL base_class

	struct               -> flags base_struct | base_struct
	base_struct          -> STRUCT IDENTIFIER block

	array_type           -> type OPEN_BRACKET expression CLOSE_BRACKET
	array_expression     -> OPEN_BRACKET opt_arr_elements CLOSE_BRACKET
	opt_arr_elements     -> arr_elements | %epsilon
	arr_elements         -> expression arr_elements'
	arr_elements'        -> COMMA arr_elements

	array_access_expr    -> expression OPEN_BRACKET expression CLOSE_BRACKET

	inclusive_range_expr -> OPEN_BRACKET expression INCLUSIVE expression
                            CLOSE_BRACKET
	exclusive_range_expr -> OPEN_BRACKET expression EXCLUSIVE expression
	                        CLOSE_BRACKET

	tuple_type           -> OPEN_PAREN types CLOSE_PAREN
	types                -> type types'
	types'               -> COMMA types

	tuple_expr           -> OPEN_PAREN tuple_values opt_comma CLOSE_PAREN
	tuple_values         -> tuple_value tuple_values'
	tuple_values'        -> COMMA tuple_value
	tuple_value          -> expression | named_expr
	opt_comma            -> COMMA | %epsilon

	named_expr           -> IDENTIFIER COLON expression

	temp_tuple_elem      -> TEMP

	if                   -> IF OPEN_PAREN expression CLOSE_PAREN block
	                        elif_or_else
	elif_or_else         -> ELIF OPEN_PAREN expression CLOSE_PAREN block
	                        elif_or_else | else
	else                 -> ELSE block

	ternary              -> expression QUESTION expression COLON expression

	for_component        -> expression | var_decl | %epsilon
	for_loop             -> FOR OPEN_PAREN for_component SEMICOLON
	                        for_component SEMICOLON for_component CLOSE_PAREN
							block
	foreach              -> FOREACH OPEN_PAREN var_decl IN expression
	                        CLOSE_PAREN block
	while                -> WHILE OPEN_PAREN expression CLOSE_PAREN block
	forever              -> FOREVER block
	do_while             -> DO block WHILE OPEN_PAREN expression CLOSE_PAREN

	/*
	** NOTE: when parsing switch_pattern, function call turns into enum pattern
	*/
	switch               -> SWITCH OPEN_PAREN expression CLOSE_PAREN
	                        switch_block
	switch_block         -> OPEN_CURLY opt_switch_matches CLOSE_CURLY
	opt_switch_matches   -> switch_matches | %epsilon
	switch_matches       -> switch_match switch_matches'
	switch_matches'      -> COMMA switch_matches | %epsilon
	switch_match         -> switch_patterns COLON switch_value
	switch_patterns      -> switch_pattern switch_patterns'
	switch_patterns'     -> COMMA switch_patterns
	switch_value         -> expression | long_block
	switch_pattern       -> expression

	break_stmt           -> BREAK
	continue_stmt        -> CONTINUE
	yield_stmt           -> YIELD expression

	func_type            -> OPEN_PAREN opt_type_list CLOSE_PAREN ARROW type
	opt_type_list        -> type_list | %epsilon
	type_list            -> type type_list'
	type_list'           -> COMMA type_list | %epsilon

	function             -> flags base_function | base_function
	base_function        -> DEF opt_identifier OPEN_PAREN opt_param_list
	                        CLOSE_PAREN opt_func_type block
	opt_identifier       -> identifier | %epsilon
	opt_param_list       -> param_list | %epsilon
	param_list           -> var_decl param_list'
	param_list'          -> COMMA param_list | %epsilon
	opt_func_type        -> ARROW type | %epsilon
	extern_fn            -> flags base_extern | base_extern
	base_extern          -> EXTERN DEF IDENTIFIER OPEN_PAREN opt_param_list
	                        CLOSE_PAREN ARROW type

    fn_call              -> expression OPEN_PAREN opt_arg_list CLOSE_PAREN
	opt_arg_list         -> arg_list | %epsilon
	arg_list             -> arg arg_list'
	arg_list'            -> COMMA arg_list | %epsilon
    arg                  -> expression | named_expr

    aggregate            -> AGGREGATE block

	interface            -> INTERFACE IDENTIFIER block

	constructor          -> IDENTIFIER OPEN_PAREN opt_param_list CLOSE_PAREN
	                        block
	destructor           -> TILDE IDENTIFIER OPEN_PAREN CLOSE_PAREN block

	namespace            -> NAMESPACE identifier opt_block
	opt_block            -> block | %epsilon
	import               -> IMPORT identifier

	new                  -> NEW identifier
	delete               -> DELETE expression
	pointer_type         -> type TIMES

	flags                -> flag flags'
	flags'               -> flag flags | %epsilon
	flag                 -> privacy | virtual | PARTIAL
	virtual              -> VIRTUAL | FINAL
	privacy              -> PRIVATE | PROTECTED | PUBLIC

	getter               -> GET block
	setter               -> SET block

	property             -> flags property_base | property_base
	property_base        -> identifier opt_func_type block

## Ambiguity

Note that there are an amount of FIRST(2) conflicts for statement (`tuple_type`, `tuple_expr`, `expression`, `type_cast` all contain `OPEN_PAREN, IDENTIFIER` in their FIRST(2) sets). Contextually, we treat IDENTIFIER as a type lexeme if it is determined to be a type.

To get type information, we have two phases of parsing. The first phase begins parsing, looking for any statement that would indicate a logical block. This includes things like if statements, while loops, functions, etc. As long as the statement derives a block in its list of symbols for a production rule, it counts as a logical block.

When parsing a logical block, any grammar derivation in the middle of a production rule that derives an expression will be ignored. For example, the condition of for loops are ignored. These are considered non-essential for gathering type names, and are stored in a buffer assigned to the AST node ID for the created element. Function return types and the like _are_ parsed, since we
are positive that identifiers are types.

After the AST node is craeted for the logical block, its body recursively parses with the same rules applied: parse essential elements only, creating AST elements and storing non-essential elements into a buffer.

The buffer is actually a stream of local buffers, where they are divided when a logical block is found. The local buffer has a reference to an AST id. If the AST ID is -1, it'll be appended to the beginning of block, otherwise it'll be placed after the block. This is used so logical blocks aren't moved out of context.

After the AST is minimally created, we can call upon `libanalysis` with our AST to ask it whether or not there is a typename accessible from a specific block. Given that, we have enough information to parse the rest of the file. We walk the AST and re-parse those tokens stored in buffers. After that is completed, the file will be fully parsed.

The situation for multiple files isn't much different: since one file could be depending on a type declared in a separate file, all files being compiled go through phase 1 of the parse before phase 2. That way `libanalysis` can be given all the ASTs to determine type accessibility.
