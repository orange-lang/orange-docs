# Rules for Well Formed Programs

This page is going to outline each and every rule that is applied to various expressions and statements for well-formed programs. It is a completely exhaustive list.

## Parser

### Ignored Newlines

Newlines are used as the termination indicator of a statement, but they are also allowed in a few places:
	- After a comma
	- After a binary operator, before the second operand
	- After a colon for short-term blocks
	- Inside long-form blocks (`{}`)
	- Inside and after a string of flags
	- After a `?` for ternary operators.
	- Between the components of a for loop.
	- Before a long-form block begins.
	- Before and after specifying generics for a function
	- After a terminal that starts a declaration (`def`, `interface`, etc)

## Types

Let a _real number type_ be the class of all integers and floating point types.

### Implicit Casting

- Compatible types are compared using the following precedence table (highest to lowest):
	- double
	- float
	- int64/int
	- int32
	- int16
	- int8
	- uint64/uint
	- uint32
	- uint16
	- uint8
- Given this, if adding an int32 and a uint8, the uint8 will be casted to int32, which takes precedence over the int8.
- Two types are said to be _compatible_ if they are the same type, or one can be implicitly casted to the other.
- Var is always a valid operand for _any_ expression.
- When computing a valid operation with var, var always takes precedence as the type.
- If bit loss may occur via an implict cast, a warning is generated.

## Variables

### Names

- Names can only be a single identifier (e.g., not `A.B.C`).

### Types

- If types are declared, there must be one type for each variable binding.
- If no type is declared, a value must be supplied.

### Value

- If there is more than one binding declared, if a value is supplied, that value must be a tuple with one element per binding.
- If a type is supplied for a binding, the value must be implicitly castable to its type.
- If a type is not supplied for a binding, the binding's type will be identical to the type of the value for it.
- If the value is an array and a type is supplied, the number of elements in the array must match the number of elements specified by the type.
- If the variable is flagged `const`, there must be a value.

## Lvalues

The following expressions are l-values:
	- References to a variable
	- An expression with a reference type
	- Deferencing a pointer
	- The temp identifier `_`

## Binary Operations

### Arithmetic binary operations

Arithmetic binary operations include the following:
	`+ - / * % | & ^ % << >>`

- The type of the result is the highest-precdence type between the two operands.
- Both operands of the binary operations must be real number types.
- The following bitwise operators can only be used with integers: `% | ^ & << >>`

### Assignment binary operations

Assignment binary operations include the following:
	`= += -= *= /= %= <<= >>= |= &= ^=`

- The type of this expression is equal to the LHS's type.
- The left-hand side of the operation must be an lvalue.
- The right-hand side must be the same type as the left-hand side OR be compatible with it.
- For the subset of assignment binary operations that do mathemetical operations, the rules for arithmetic binary operations apply:
	- LHS and RHS must be real number types
	- Bitwise operations can only be used with integer types.
- Unlike C, these are *not* lvalues (e.g., `a = b = c` is invalid).
- If the LHS is flagged const, it cannot be modfied and an error will be generated.

### Comparison binary operations

Comparison binary operations include the following:
	`< > <= >= != ==`

- The type of this expression is `bool`.
- Both operators to the expression must be compatible.

### Logical binary operations

Logical binary operations include the following:
	`|| &&`

- The type of this exression is `bool`.
- Both operators to the expression must also be boolean. No implicit casting will be done here, unlike C.

## Unary Operations

### Lvalue modifiers

- `++` and `--` can only be used on l-values.
- They are also only valid on real number types.

### Reference and Deferencing

- `*` is only valid on a pointer type.
- `&` is only valid on a variable reference.

### Other unary operations

- `!` is only valid with boolean types.
- `~` is only valid on integer types.
- `-` is only valid with real types.

## Using Variables

- Any variable must be assigned a value at least once before using it in a given scope.
	- This is checked by seeing if the current scope or any of the parent scopes, up until the scope where the variable is declared, assigns a value to the variable.
	- This is a warning in all cases.

### Shadowed Variables

- Referencing a shadowed variable only ever refers to the most recent declaration of the binding, never the first. The original binding is inaccessible after it is re-bound.

## Explicit Casting

- Any real number can be casted to another real number type.
- Any real number can be casted to a pointer type.
- A pointer type can be casted to an integer.
- Arrays _can not_ be casted.
- Tuples _can not_ be casted.

## Classes

- The type of a class is derived from the combination of the types of its members.
- Redeclaring members is not valid.
- Any var typed or member without a type makes the class generic.
- The default constuctor exists until a custom constructor is supplied.
- A constructor must always be the same name as the class.
- Each "super" in the class' super list must exist.

## Arrays

- Each member of an array must be compatible with the array's component type.

## Array Ranges

- Each operand to the range must be an integer type.

## Tuples

- A tuple cannot be implicitly casted to another tuple type.
- When a tuple has named elements, all components must have a name.

## Temp ID

- The temp identifier has a special type `auto`. It is the lowest-precedence type and is compatible with any other type.
- The temp identifier is throwaway and does not store its value anywhere. It can only be used as an lvalue, never an rvalue.

## Enums

- The type of an enum is a value indicating which enumeration it represents, and a union for any potential parameters it may have.

## Exceptions

- An exception can be thrown for any valid rvalue.
- If a try block is specified, there must be at least one catch block.

## Extensions

- The class defined by the extension must exist.
- Only methods and properties may be defined in an extension.

## If blocks

- The expression of an if block must exist and must be a boolean type.
- If an if block has its value taken, there must be an else block.
- If an if block has its value taken, every possible value yielded by the block must be compatible.

## Ternary Operators

- The true and false value of the ternary operator must be compatible.
- The expression of the ternary operator must be a boolean type.

## For Loop

- The condition of the for loop is optional, but must be a boolean type if specified.

## Functions

- If a return type is specified, the function must return something.
	- If that return type is void, the function *must not* return something.
- Each return statement in the function must be compatible with the return type.
- If the return type is not specified, the return type will be inferred via the highest precedence type amonst all the return statements.
- If the return type is not void, each return must have a value.

## Short blocks

- A short block's expression will be used for either return or yield (depending on the block) if the expression has a value. It must be compatible with the type of the block, if that block has an explicitly defined type (like a function's return type).

## Aggregate blocks

- Aggregate blocks can only define any non-function statement for its header.
- When a function is declared, that specifies the body of the aggregate. Only functions may be declared in the body.
- When a non-function is declared, that specifies the footer of the aggregate. No more functions may be declared.
- Aggregate blocks must have a body, but headers and footers are optional.

## External functions

- External functions must have a return type.

## Inheritance

- Sub-classes whose parent class does not have a default constructor must themselves have an explicitly defined constructor where they call the constructor for a parent.
- Sub-classes with explicitly defined constructors must explicitly call the constructor for their parent class.

## Interfaces

- Interfaces may only define functions, and must not have bodies.

## Privacy

Privacy flags may only be declared on functions, declared objects, and class members. 
