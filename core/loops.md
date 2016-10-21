# Loops

Orange has three types of looping constructs: `for` loops, `while` loops, and `do while` loops.

## For Loops

For loops have three components: the initializer, condition, and afterthought. These components are tied to the scope of the loop's body.

The initializer is a statement that is always ran before the loop begins. It can be used for declaring variables for the loop to use.

The condition is a boolean-typed expression that is checked for being `true` each time before the loop executes.

The afterthought executes each time the loop body's finishes.

```
for (initializer; condition; afterthought) {
	// statements
}

// or
for (initializer; condition; afterthought): expression
```

## While Loops

While loops only have a condition it checks each iteration before the body is executed:

```
while (condition) {
	// statements
}

// or
while (condition): expression
```

## Do While Loops

Do while loops execute their condition after the code block has been executed.

```
do {
	// statements
} while (condition)

// or
do: expression while (condition)
```

## Break and Continue

`break` and `continue` are statements that can be used inside loops to continue to the next iteration or stop all iterations. Unlike in other languages, `break` and `continue` can be given values to be used with giving the block a value. If no value is supplied, they give void.

## Yield in Loops

If a loop block is used as a value, each iteration must provide a value. That means the loop must always end with a `yield` statement that has a value, and if a break or continue is used anywhere else in the loop, it must supply a value of the same type.

In the context of a loop, `yield` acts as `continue` instead of `break`.
