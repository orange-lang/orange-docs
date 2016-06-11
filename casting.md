# Type Casting

	expression -> "(" type ")" expression

A type may be casted to another valid type by prefixing the expression to cast with the target type name in parenthesis. For example, `(int)5.3` casts 5.3 as an integer (`5`).

Type casts may be defined in classes by overloading the operator with the target TypeName in parenthesis (`def operator(TargetType)`).
