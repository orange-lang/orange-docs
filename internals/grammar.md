# Grammar

This file outlines the BNF grammar that Orange will use for its parser. It is a simplified version of [Grammar Summary](../language/grammar_summary.md).

```
program              -> opt_statements

opt_statements       -> statements | %epsilon
statements           -> statement statements'
statements'          -> TERM statement | %epsilon

term                 -> SEMICOLON | NEWLINE

long_block           -> OPEN_CURLY opt_statements CLOSE_CURLY
short_block          -> COLON statement
block                -> long_block | short_block

/*
** Types
*/

type                 -> tuple_type | array_type | pointer_type | func_type
type                 -> INT | UINT | INT8 | INT16 | INT32 | INT64
type                 -> UINT8 | UINT16 | UINT32 | UINT64
type                 -> FLOAT | DOUBLE | VAR | VOID | named_id | ref_type

array_type           -> type OPEN_BRACKET expression CLOSE_BRACKET
tuple_type           -> OPEN_PAREN tuple_types CLOSE_PAREN
func_type            -> OPEN_PAREN opt_type_list CLOSE_PAREN ARROW type
pointer_type         -> type TIMES
ref_type             -> type BIT_AND

/* Allows for a list of types with a trailing comma */
types                -> type types'
types'               -> COMMA types''
types''              -> types | %epsilon

/* Allows for a list of types with no trailing comma */
opt_type_list        -> type_list | %epsilon
type_list            -> type type_list'
type_list'           -> COMMA type_list | %epsilon

identifier           -> operator_id | named_id
named_id             -> id_types opt_generic_spec
opt_generic_spec     -> generic_spec | %epsilon
generic_spec         -> LESS_THAN OF type_list GREATER_THAN
id_types             -> full_id | dtor_id
full_id              -> IDENTIFIER full_id'
full_id'             -> DOT identifier | %epsilon
operator_id          -> OPERATOR operator
dtor_id              -> TILDE IDENTIFIER

/*
** Statements
*/

statement            -> var_decl | class | long_block
statement            -> break_stmt | continue_stmt
statement            -> yield_stmt | function | aggregate
statement            -> extern_fn
statement            -> interface | destructor | namespace
statement            -> import | extension
statement            -> getter | setter | property | enum | expr_statement
statement            -> delete

var_decl             -> opt_const VAR identifiers opt_type_spec_list
                        opt_value
opt_const            -> CONST | %epsilon
identifiers          -> named_id | OPEN_PAREN identifer_list CLOSE_PAREN
identifier_list      -> named_id identifier_list'
identifier_list'     -> COMMA identifier_list | %epsilon
opt_type_spec_list   -> COLON type_list | %epsilon
opt_value            -> ASSIGN expression | %epsilon

enum                 -> flags enum_base | enum_base
enum_base            -> ENUM named_id OPEN_CURLY opt_enum_values
                        CLOSE_CURLY
opt_enum_values      -> enum_values | %epsilon
enum_values          -> enum_value enum_values'
enum_values'         -> COMMA enum_values
enum_value           -> IDENTIFIER opt_enum_params
opt_enum_params      -> OPEN_PAREN param_list CLOSE_PAREN | %epsilon
enum_patterm         -> named_id OPEN_PAREN arg_list CLOSE_PAREN

class                -> flags base_class | base_class
base_class           -> CLASS IDENTIFIER opt_supers class_body
opt_supers           -> COLON super_list | %epsilon
super_list           -> named_id super_list'
super_list'          -> COMMA super_list
partial_class        -> flags PARTIAL base_class

class_body           -> OPEN_CURLY opt_class_stmts CLOSE_CURLY
opt_class_stmts      -> class_stmts | %epsilon
class_stmts          -> class_stmt class_stmts'
class_stmts'         -> term class_stmts | %epsilon

class_stmt           -> implicit_var | class | function | aggregate
class_stmt           -> extern_fn | import | extension | property
class_stmt           -> enum

function             -> flags base_function | base_function
base_function        -> DEF opt_identifier opt_generics OPEN_PAREN
                        opt_param_list CLOSE_PAREN opt_func_type block
opt_identifier       -> identifier | %epsilon
opt_name             -> IDENTIFIER | %epsilon
opt_param_list       -> param_list | %epsilon
param_list           -> implicit_var param_list'
param_list'          -> COMMA param_list | %epsilon
opt_func_type        -> ARROW type | %epsilon
extern_fn            -> flags base_extern | base_extern
base_extern          -> EXTERN DEF IDENTIFIER OPEN_PAREN opt_param_list
                        CLOSE_PAREN ARROW type

implicit_var         -> opt_const identifiers opt_type_spec opt_value
opt_type_spec        -> COLON type | %epsilon

aggregate            -> AGGREGATE opt_name block

interface            -> INTERFACE IDENTIFIER block

namespace            -> NAMESPACE named_id opt_block
opt_block            -> block | %epsilon
import               -> IMPORT named_id

extension            -> EXTEND named_id opt_supers block

property             -> flags property_base | property_base
property_base        -> IDENTIFIER opt_func_type block

expr_statement       -> expresssion expr_statement'
expr_statement'      -> SEMICOLON | %epsilon

getter               -> GET block
setter               -> SET block

/*
** Expressions
*/

expression           -> ternary_expr | assign_expr | or_expr

ternary_expr         -> or_expr QUESTION expression COLON expression

assign_expr          -> or_expr assign_op expression
assign_op            -> ASSIGN | PLUS_ASSIGN | MINUS_ASSIGN |
                        TIMES_ASSIGN | DIVIDE_ASSIGN | REMAINDER_ASSIGN |
						SHIFT_LEFT_ASSIGN | SHIFT_RIGHT_ASSIGN |
						BIT_OR_ASSIGN | BIT_AND_ASSIGN | BIT_XOR_ASSIGN

or_expr              -> or_expr OR and_expr | and_expr
and_expr             -> and_expr AND bit_or_expr | bit_or_expr
bit_or_expr          -> bit_or_expr BIT_OR bit_xor_expr | bit_xor_expr
bit_xor_expr         -> bit_xor_expr BIT_XOR bit_and_expr | bit_and_expr
bit_and_expr         -> bit_and_expr BIT_AND equality | equality

equality             -> equality eq_op comparison | comparison
eq_op                -> EQUALS | NEQ

comparison           -> comparison comp_op shifts | shifts
comp_op              -> LESS_THAN | GREATER_THAN | LEQ | GEQ

shifts               -> shifts shift_op sums | sums
shift_op             -> SHIFT_LEFT | SHIFT_RIGHT

sums                 -> sums sum_op mult | mult
sum_op               -> PLUS | MINUS

mult                 -> mult mult_op unary | unary
mult_op              -> TIMES | DIVIDE | REMAINDER

unary                -> INCREMENT unary | DECREMENT unary | MINUS unary |
                        NOT unary | TILDE unary | type_cast |
						TIMES unary | BIT_AND unary | values

values               -> fn_call | array_access_expr | values INCREMENT |
                        values DECREMENT | dot

dot                  -> primary DOT dot | primary

primary              -> value | OPEN_PAREN expression CLOSE_PAREN

value                -> array_expression
value                -> inclusive_range_expr | exlusive_range_expr
value                -> tuple_expr | constant_val | THIS | control | new

constant_val         -> VAL_INT | VAL_INT8 | VAL_INT16 | VAL_INT32
constant_val         -> VAL_INT64 | VAL_UINT | VAL_UINT8 | VAL_UINT16
constant_val         -> VAL_UINT32 | VAL_UINT64 | VAL_FLOAT | VAL_DOUBLE
constant_val         -> VAL_STRING

control              -> if | for_loop | foreach | while | forever | do_while
control              -> switch | try_block

type_cast            -> OPEN_PAREN type CLOSE_PAREN expression

array_expression     -> OPEN_BRACKET opt_arr_elements CLOSE_BRACKET
opt_arr_elements     -> arr_elements | %epsilon
arr_elements         -> expression arr_elements'
arr_elements'        -> COMMA arr_elements

array_access_expr    -> values OPEN_BRACKET expression CLOSE_BRACKET

inclusive_range_expr -> OPEN_BRACKET expression INCLUSIVE expression
                        CLOSE_BRACKET
exclusive_range_expr -> OPEN_BRACKET expression EXCLUSIVE expression
                        CLOSE_BRACKET

tuple_expr           -> OPEN_PAREN tuple_values opt_comma CLOSE_PAREN
tuple_values         -> tuple_value tuple_values'
tuple_values'        -> COMMA tuple_value
tuple_value          -> expression | named_expr
opt_comma            -> COMMA | %epsilon

named_expr           -> IDENTIFIER COLON expression

if                   -> IF OPEN_PAREN expression CLOSE_PAREN block
                        elif_or_else
elif_or_else         -> ELIF OPEN_PAREN expression CLOSE_PAREN block
                        elif_or_else | else
else                 -> ELSE block

for_component        -> expression | var_decl | %epsilon
for_loop             -> FOR OPEN_PAREN for_component SEMICOLON
                        for_component SEMICOLON for_component CLOSE_PAREN
						block
foreach              -> FOREACH OPEN_PAREN var_decl IN expression
                        CLOSE_PAREN block
while                -> WHILE OPEN_PAREN expression CLOSE_PAREN block
forever              -> FOREVER block
do_while             -> DO block WHILE OPEN_PAREN expression CLOSE_PAREN

// NOTE: when parsing switch_pattern, function call turns into enum pattern
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

fn_call              -> values OPEN_PAREN opt_arg_list CLOSE_PAREN
opt_arg_list         -> arg_list | %epsilon
arg_list             -> arg arg_list'
arg_list'            -> COMMA arg_list | %epsilon
arg                  -> expression | named_expr

opt_generics         -> generics | %epsilon
generics             -> LESS_THAN opt_generic_values opt_constraints
                        GREATER_THAN
opt_generic_values   -> generic_values | %epsilon
generic_values       -> IDENTIFIER generic_values'
generic_values'      -> COMMA generic_values | %epsilon
opt_constraints      -> constraints | %epsilon
constraints          -> constraint constraints'
constraints'         -> COMMA constraints | %epsilon
constraint           -> WHERE IDENTIFIER ASSIGN type_constraint
type_constraint      -> CLASS | NEW OPEN_PAREN CLOSE_PAREN
type_constraint      -> named_id | DATA type | type

new                  -> NEW named_id
delete               -> DELETE expression

flags                -> flag flags'
flags'               -> flag flags | %epsilon
flag                 -> privacy | virtual | PARTIAL
virtual              -> VIRTUAL | FINAL
privacy              -> PRIVATE | PROTECTED | PUBLIC

try_block            -> TRY block opt_catch_blocks opt_finally_block
opt_catch_blocks     -> catch_blocks | %epsilon
catch_blocks         -> catch_block catch_blocks'
catch_blocks'        -> catch_blocks | %epsilon
catch_block          -> CATCH OPEN_PAREN implicit_var CLOSE_PAREN block
opt_finally_block    -> finally_block | %epsilon
finally_block        -> FINALLY block
throw_stmt           -> THROW expression
```
