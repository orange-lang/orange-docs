# Grammar

This file outlines the EBNF grammar that Orange will use for its parser. It is a simplified version of [Grammar Summary](../language/grammar_summary.md).

```
program              -> statements?

statements           -> statement (TERM statement?)*

term                 -> SEMICOLON | NEWLINE

long_block           -> OPEN_CURLY statements? CLOSE_CURLY
short_block          -> COLON statement
block                -> long_block | short_block

/*
** Types
*/

type                 -> basic_type | complex_type

basic_type           -> INT | INT8 | INT16 | INT32 | INT64
basic_type           -> UINT | UINT8 | UINT16 | UINT32 | UINT64
basic_type           -> CHAR | FLOAT | DOUBLE | VAR | VOID

complex_type         -> tuple_type | array_type | pointer_type | func_type
complex_type         -> ref_type | id_type

tuple_type           -> OPEN_PAREN tuple_types CLOSE_PAREN
array_type           -> type OPEN_BRACKET expression CLOSE_BRACKET
pointer_type         -> type TIMES
func_type            -> OPEN_PAREN type_list? CLOSE_PAREN ARROW type
ref_type             -> type BIT_AND
id_type              -> id_path_type id_ty_access?
id_ty_access         -> DOT base_id_type

id_path_type         -> basic_type | id_type generic_spec?
generic_spec         -> LESS_THAN OF type_list GREATER_THAN

base_id_type         -> IDENTIFIER | operator_id | dtor_id
operator_id          -> OPERATOR operator
dtor_id              -> TILDE IDENTIFIER

/* Allows for a list of types with a trailing comma */
tuple_types          -> type COMMA (type (COMMA type)*)?

/* Allows for a list of types with no trailing comma */
type_list            -> type (COMMA type)*

/*
** Identifiers
*/

identifier           -> identifier_base generic_spec?
identifier_base      -> IDENTIFIER | TILDE IDENTIFIER

full_identifier      -> full_id_base full_id_access?
full_id_accesss      -> DOT identifier_base
full_id_base         -> IDENTIFIER | full_identifier generic_spec?

/*
** Statements
*/

statement            -> var_decl | class | long_block
statement            -> break_stmt | continue_stmt
statement            -> yield_stmt | function | aggregate
statement            -> extern_fn | interface | destructor
statement            -> namespace | import | extension | getter
statement            -> setter | property | enum | expr_statement
statement            -> delete | COMMENT

var_decl             -> CONST? VAR identifiers (COLON type_list)?
                        (ASSIGN expression)?
identifiers          -> identifier | OPEN_PAREN identifer_list CLOSE_PAREN
identifier_list      -> identifier (COMMA identifier)*

enum                 -> flags? ENUM identifier OPEN_CURLY enum_values?
                        CLOSE_CURLY
enum_values          -> enum_value (COMMA enum_value)*
enum_value           -> IDENTIFIER enum_params?
enum_params          -> OPEN_PAREN param_list? CLOSE_PAREN

class                -> flags? CLASS IDENTIFIER (COLON super_list)? class_body
super_list           -> full_identifier (COMMA full_identifier)*

class_body           -> OPEN_CURLY class_stmts? CLOSE_CURLY
class_stmts          -> class_stmt (term class_stmt)*

class_stmt           -> var_decl | class | function | aggregate
class_stmt           -> extern_fn | import | extension | property
class_stmt           -> enum

function             -> flags? DEF identifier? generics? OPEN_PAREN
                        param_list? CLOSE_PAREN (ARROW type)? block
param_list           -> implicit_var (COMMA implicit_var)*
extern               -> flags? EXTERN DEF IDENTIFIER OPEN_PAREN param_list?
                        CLOSE_PAREN ARROW type

implicit_var         -> flags? identifiers (COLON type)? (ASSIGN expression)?

aggregate            -> AGGREGATE IDENTIFIER? block

interface            -> INTERFACE IDENTIFIER interface_block

interface_block      -> OPEN_CURLY interface_statements CLOSE_CURLY
interface_statements -> interface_function (term interface_function)*
interface_function   -> flags? DEF identifier? generics? OPEN_PAREN
                        param_list? CLOSE_PAREN ARROW type

namespace            -> NAMESPACE full_identifier full_block?
import               -> IMPORT full_identifier

extension            -> EXTEND full_identifier supers? block

property             -> flags? PROPERTY IDENTIFIER (ARROW type)? block

expr_statement       -> expresssion SEMICOLON?

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
                        values DECREMENT | dot | primary

dot                  -> values DOT identifier

primary              -> value | OPEN_PAREN expression CLOSE_PAREN

value                -> array_expression
value                -> inclusive_range_expr | exlusive_range_expr
value                -> tuple_expr | constant_val | THIS | control | new | TEMP

constant_val         -> VAL_INT | VAL_INT8 | VAL_INT16 | VAL_INT32
constant_val         -> VAL_INT64 | VAL_UINT | VAL_UINT8 | VAL_UINT16
constant_val         -> VAL_UINT32 | VAL_UINT64 | VAL_FLOAT | VAL_DOUBLE
constant_val         -> VAL_STRING | VAL_CHARACTER

control              -> if | for_loop | foreach | while | forever | do_while
control              -> switch | try_block

type_cast            -> expression AS type

array_expression     -> OPEN_BRACKET arr_elements? CLOSE_BRACKET
arr_elements         -> expression (COMMA expression)*

array_access_expr    -> values OPEN_BRACKET expression CLOSE_BRACKET

inclusive_range_expr -> OPEN_BRACKET expression INCLUSIVE expression
                        CLOSE_BRACKET
exclusive_range_expr -> OPEN_BRACKET expression EXCLUSIVE expression
                        CLOSE_BRACKET

tuple_expr           -> OPEN_PAREN tuple_values COMMA? CLOSE_PAREN
tuple_values         -> tuple_value (COMMA tuple_value)*
tuple_value          -> expression | named_expr

named_expr           -> IDENTIFIER COLON expression

if                   -> IF OPEN_PAREN expression CLOSE_PAREN block
                        elif_or_else
elif_or_else         -> ELIF OPEN_PAREN expression CLOSE_PAREN block
                        elif_or_else | else
else                 -> ELSE block

for_component        -> expression | var_decl
for_loop             -> FOR OPEN_PAREN for_component? SEMICOLON
                        for_component? SEMICOLON for_component? CLOSE_PAREN
						block
foreach              -> FOREACH OPEN_PAREN var_decl IN expression
                        CLOSE_PAREN block
while                -> WHILE OPEN_PAREN expression CLOSE_PAREN block
forever              -> FOREVER block
do_while             -> DO block WHILE OPEN_PAREN expression CLOSE_PAREN

// NOTE: when parsing switch_pattern, function call turns into enum pattern
switch               -> SWITCH OPEN_PAREN expression CLOSE_PAREN
                        switch_block
switch_block         -> OPEN_CURLY switch_matches? CLOSE_CURLY
switch_matches       -> switch_match (COMMA switch_matches)*
switch_match         -> switch_patterns COLON switch_value
switch_patterns      -> switch_pattern (COMMA switch_patterns)
switch_value         -> expression | long_block
switch_pattern       -> IDENTIFIER enum_pattern? | TEMP
enum_pattern         -> OPEN_PAREN enum_pattern_list? CLOSE_PAREN
enum_pattern_list    -> IDENTIFIER (COMMA IDENTIFIER)*

break_stmt           -> BREAK
continue_stmt        -> CONTINUE
yield_stmt           -> YIELD expression

fn_call              -> values OPEN_PAREN arg_list? CLOSE_PAREN
arg_list             -> arg (COMMA arg)*
arg                  -> expression | named_expr

generics             -> LESS_THAN generic_values? constraints?
                        GREATER_THAN
generic_values       -> IDENTIFIER (COMMA IDENTIFIER)*
constraints          -> constraint (COMMA constraint)*
constraint           -> WHERE IDENTIFIER ASSIGN type_constraint
type_constraint      -> CLASS | NEW OPEN_PAREN CLOSE_PAREN
type_constraint      -> full_identifier | DATA type | type

new                  -> NEW full_identifier
delete               -> DELETE expression

flags                -> flag+
flag                 -> privacy | virtual | PARTIAL | CONST
virtual              -> VIRTUAL | FINAL
privacy              -> PRIVATE | PROTECTED | PUBLIC

try_block            -> TRY block catch_blocks? finally_block?
catch_blocks         -> catch_block+
catch_block          -> CATCH OPEN_PAREN implicit_var CLOSE_PAREN block
finally_block        -> FINALLY block
throw_stmt           -> THROW expression
```
