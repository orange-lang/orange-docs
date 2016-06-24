# Lexer

This file outlines the tokens and the regular expressions that generate them.

The lexer rules are written in a pseudo-BNF: right-hand sides of productions
are regex. The RHS of a production can derive another nonterminal when that nonterminal is referenced inside `<>`. Comments are provided in C-style, and nonterminals are written in all-caps.

	COMMENT            -> "//"[^\r\n]*

	// Allows for nesting block comments
	BLOCK_COMMENT      -> "/*" <BLOCK_COMMENT_BODY> "*/"
	BLOCK_COMMENT_BODY -> <BLOCK_COMMENT> | [^*/]

	INTEGER            -> <INTEGER_PREFIX> <INTEGER_SUFFIX>?
	INTEGER_PREFIX     -> 0b <BINARY> | 0o <OCTAL> | 0x <HEX> | <DECIMAL>
	INTEGER_SUFFIX     -> "i" | "u" | "i8" | "i16" | "i32" | "i64" |
	                      "u8" | "u16" | "u32" | "u64"

	BINARY             -> [0|1]+
	OCTAL              -> [0-7]+
	HEX                -> [0-9A-Fa-f]+
	DECIMAL            -> "0" | [1-9][0-9]*

	FLOATING_POINT     -> <FLOAT> <FLOAT_SUFFIX>?
	FLOAT              -> DECIMAL ("." [0-9]+)?
	FLOAT_SUFFIX       -> "f" | "d"

	STRING             -> \"(\\.|[^\\"])*\"

	NEWLINE            -> "\n"
	SEMICOLON          -> ";"
	INT                -> "int"
	UINT               -> "uint"
	INT8               -> "int8"
	INT16              -> "int16"
	INT32              -> "int32"
	INT64              -> "int64"
	UINT8              -> "uint8"
	UINT16             -> "uint16"
	UINT32             -> "uint32"
	UINT64             -> "uint64"
	FLOAT              -> "float"
	DOUBLE             -> "double"
	VAR                -> "var"
	VOID               -> "void"
	IDENTIFIER         -> "_"? [A-Za-z_][A-Za-z0-9_]*
	TEMP               -> "_"
	OPERATOR           -> "operator"
	OPEN_PAREN         -> "("
	CLOSE_PAREN        -> ")"
	PLUS               -> "+"
	MINUS              -> "-"
	DIVIDE             -> "/"
	TIMES              -> "*"
	REMAINDER          -> "%"
	BIT_OR             -> "|"
	BIT_AND            -> "&"
	BIT_XOR            -> "^"
	QUESTION           -> "?"
	SHIFT_LEFT         -> "<<"
	SHIFT_RIGHT        -> ">>"
	ASSIGN             -> "="
	EQUALS             -> "=="
	PLUS_ASSIGN        -> "+="
	MINUS_ASSIGN       -> "-="
	TIMES_ASSIGN       -> "*="
	DIVIDE_ASSIGN      -> "/="
	REMAINDER_ASSIGN   -> "%="
	SHIFT_LEFT_ASSIGN  -> "<<="
	SHIFT_RIGHT_ASSIGN -> ">>="
	BIT_OR_ASSIGN      -> "|="
	BIT_AND_ASSIGN     -> "&="
	BIT_XOR_ASSIGN     -> "^="
	LESS_THAN          -> "<"
	GREATER_THAN       -> ">"
	LEQ                -> "<="
	GEQ                -> ">="
	NEQ                -> "!="
	NOT                -> "!"
	AND                -> "&&"
	OR                 -> "||"
	INCREMENT          -> "++"
	DECREMENT          -> "--"
	ENUM               -> "enum"
	OPEN_CURLY         -> "{"
	CLOSE_CURLY        -> "}"
	COMMA              -> ","
	DOT                -> "."
	CLASS              -> "class"
	PARTIAL            -> "partial"
	OPEN_BRACKET       -> "["
	CLOSE_BRACKET      -> "]"
	EXLUSIVE_RANGE     -> "..."
	INCLUSIVE_RANGE    -> ".."
	COLON              -> ":"
	IN                 -> "in"
	IF                 -> "if"
	ELIF               -> "elif"
	ELSE               -> "else"
	FOR                -> "for"
	FOREACH            -> "foreach"
	WHILE              -> "while"
	FOREVER            -> "forever"
	DO                 -> "do"
	SWITCH             -> "switch"
	BREAK              -> "break"
	CONTINUE           -> "continue"
	YIELD              -> "yield"
	DEF                -> "def"
	ARROW              -> "->"
	EXTERN             -> "extern"
	AGGREGATE          -> "aggregate"
	INTERFACE          -> "interface"
	TILDE              -> "~"
	NAMESPACE          -> "namespace"
	IMPORT             -> "import"
	NEW                -> "new"
	DELETE             -> "delete"
	PRIVATE            -> "private"
	PROTECTED          -> "protected"
	PUBLIC             -> "public"
	GET                -> "get"
	SET                -> "set"
	VIRTUAL            -> "virtual"
	FINAL              -> "final"
	PARTIAL            -> "partial"
	WHERE              -> "where"
	DATA               -> "data"
	EXTEND             -> "extend"
