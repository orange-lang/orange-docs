# Builtin Operations

There are a few categories of builtin operations you can do: mathematical operations, bitwise operations, logical operations, conditional operations, and assignment operations.

Note that all binary operations here require both operands to be of the same type, but we'll see in [Type of Numeric Constants](numeric_consts.md) that the two constants `5` and `82.9` don't necessarily have different types.

## Mathemtical Operations

The mathematical operations should be fairly obvious: `+`, `-`, `/` and `*` are all valid binary operators to be used on two numeric types.

The modulo operator, `%`, is only valid on integers.

## Bitwise Operations

Bitwise operations are only valid on integers, and include:

- `<<`: Shift left
- `>>`: Shift right
- `|`: Bitwise OR
- `&`: Bitwise AND
- `^`: Bitwise XOR
- `~`: Bitwise NOT

## Logical Operations

Logical operations can only be used on boolean expressions, and there is only `!`, `||`, and `&&` for logical NOT, logical OR, and logical AND respectively. The binary logical operations are short-circuiting.

## Conditional Operations

The following conditional operations are:

- `<`: Less than
- `>`: Greater than
- `<=`: Less than or equal to
- `>=`: Greater than or equal to
- `==`: Equal to
- `!=`: Not equal to

The less than/greater than family of conditional operations are only valid on numeric values, while the equal to and not equal to can be used on values of any of the builtin types.

All of the conditional operations can be used on new types, since the conditional operations are defined for the builtin `Equality` and/or `Ordered` interface types. See [Interfaces](interfaces.md), [Extensions](extensions.md) and [Classes](classes.md) for more information on how to do this.

## Assignment Operations

All of the non-conditional operations here can be combined with a single equal sign to become an assignment operation. For example, `a += b` is equivalent to `a = a + b`.
