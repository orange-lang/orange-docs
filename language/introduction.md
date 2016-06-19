# Language

## Source File Format

When reading files, Orange expects the input to be UTF-8. At the moment, standard ASCII characters can only be used for valid identifiers, but in the future, unicode support is planned.

A comment is initialized by starting a line with `//`. A multi-line comment begins with `/*` and ends with `*/`. Note that in Orange, unlike other languages, multi-line comments can be nested, so the following is valid:

    /*
       this is my multiline comment
       /* this is still inside my comment */
    */

## Grammar used in file

The syntax for the various sections in this document will be explained using BNF-like syntax mixed with a little regex:

	production -> expression
	production_options -> expression1 | expression2
	production_group -> ( grouped_expression )
	repeats_once_or_more -> expression+
	repeats_zero_or_more -> expression*
	zero_or_once -> expression?
	terminal -> "constant in string"
	terminal_range -> "const a" ... "const b"

For example, the production rule

	s -> "a" ( "b" | "c" )*

Will derive a string of terminals starting with `a` and zero or more sequences of `b` or `c`. A few of these derivations includes `a`, `abbcccc`, and `acbcbcc`.
