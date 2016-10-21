# Blocks and Yield

In the last section, we've defined how to create functions. Some blocks in Orange support a simpler form for providing a value. These are called _short blocks_, and instead of wrapping statements in curly braces, they're just formed by a semi-colon and then any statement or expression.

Our `addTwoNumbers` function from earlier could be re-written in this short block form:

```
def addTwoNumbers(a: int, b: int) -> int: a + b

// alternatively:
def addTwoNumbers(a: int, b: int): a + b

// alternatively:
def addTwoNumbers(a: int, b: int): return a + b

// alternatively:
def addTwoNumbers(a: int, b: int): yield a + b
```

This short-form syntax can be used in any place where statements can occur (functions, for loops, conditionals, etc). More information on rules will be given when we describe those components.

## Yield

Note that the last example of our short-block `addTwoNumbers` function referenced the keyword _yield_. When using short blocks, the statement or expression provided will be passed through a yield by default.

A `yield` is a context-sensative keyword that exits out of the current block with the value provided. Like return, a `yield` can supply nothing and its type would be `void`.

When `yield` is used at the highest scope of a function, it acts the same as a `return` would.

## Scoped Blocks

A block is also a valid expression in Orange, which defines a new scope. These scoped blocks can also yield values that can be used as part of an expression. For example:

```
var myAge = {
	var currentYear = 2016
	var birthYear = 1925
	yield currentYear - birthYear
}

// currentYear and birthYear are out of scope now
```
