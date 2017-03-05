# Variables

Variables are mutable, bound values to a referenceable name. They can be declared with a type or the type can be infered by the initial assignment:

```
var myNumber = 5      // type inferred from value
var myNumber: int = 5 // type declared explicitly
var myNumber: int     // type declared explicitly
var myNumber          // ERROR: cannot infer type of myNumber
```

## Default values

When the initial value is omitted from the variable declaration, the _default constructor_ for the type is used. This means that all of these statements are equivalent:

```
var myNumber: int
var myNumber: int = int()
var myNumber = int()
```

## Constant Variables

A variable can be made immutable and constant by prefixing the declaration with `const`.

```
const var myNumber = 5

myNumber = 6 // ERROR: myNumber was declared as a constant.
```

## Unwrapping Tuples

Tuples can be unwrapped to multiple variables by having multiple variable names on the left-hand side of the declaration's assignment.

```
var a, b = (5i8, 20u)

// alternatively:
var a, b: int8, uint = (5i8, 20u)
```

## Underscore

`_` is a special variable in Orange that can be assigned a value from any type but can never be read from.

```
_ = 5  // good:  assigning to _
a = _  // error: cannot read from _
```
