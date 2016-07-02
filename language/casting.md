# Type Casting

	type_cast  -> expression "as" type
	expression -> type_cast

A type may be casted to another valid type by prefixing the expression to cast with the target type name in parenthesis. For example, `5.3 as int` casts 5.3 as an integer (`5`).

Type casts may be defined in classes by overloading the operator with the target TypeName in parenthesis (`def operator(TargetType)`).
