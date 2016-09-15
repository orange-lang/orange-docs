# Assignment

Assignment is supported through the following function:

```
def operator=<T>(LHS: T&, RHS: const T)
```

These two functions are implemented internally and allow for assigning to any value to an lvalue of the same type. Their values are copied to the lvalue.

You can override the assignment operator with more specific types, or even create an assignment operator with two different types. For example, you could define this:

```
def operator=(LHS: MyType&, RHS: const Int) {
	LHS.value = RHS
}
```

Note that Orange disallows defining binary operators where the first argument, the left-hand side of the expression, is a builtin type.

Note that unlike types and other functions, overriden operators are always populated in the global namespace when importing.
