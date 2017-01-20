# Core Language

This section describes the core language of Orange.

## Source File Format

Orange source files are read in as UTF-8.

Comments be achieved in one of two ways: entering `//` will treat everything following the two slashes as a comment until the end of the line.

Alternatively, a comment can be started with `/*` and it doesn't end until it finds a _matching_ `*/` on the same or a different line, meaning that nesting multi-line comments are valid.

## Statements and Expressions

Orange omits the requirement of semicolons at the end of statements in most cases. Semicolons can be used to put multiple statements on a single line, or to coerce an expression to a statement and not have a value. That is to say, `5` is an expression with a value, but `5;` is a statement and does not have a referencable value.

Semicolons are the lowest-precedence operator, so an expression `a = b;` is parsed as `(a = b);`.

Orange has no `main` function; a file has code declared on a file scope (think Python, Ruby, Javascript). However, in a compiled project, one file is designated as the "main" file. Only the main file will have its statements executed when the program is ran; other files only export types.

`argv` is a global variable that is usable from the main file, of type `string[]`.
