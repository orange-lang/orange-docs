# Functions

```
def addTwoNumbers(a: int, b: int) -> int {
	return a + b
}
```

Above is an example of how to declare a function. Functions always begin with `def`, and then the function signature. Parameters can optionally be given default values like the following:

```
def addTwoNumbers(a: int = 5, b: int = 10) -> int {
	return a + b
}

addTwoNumbers() == 15
```

In addition, the return type can be omitted and infered by the compiler:

```
def addTwoNumbers(a: int, b: int) {
	return a + b
}
```

The type of this function is typed as `(int, int) -> int`.

## Functions are Values

Functions are first-class citizens in Orange. They can be passed as parameters to functions and stored in variables:

```
def f() {
	return 5
}

def g() {
	return 10
}

def addResults(functionA: const () -> int, functionB: const () -> int) {
	return functionA() + functionB()
}

const var numberFunctions = [f, g]
addResults(numberFunctions[0], numberFunctions[1]) == 15
```

## Anonymous Functions

Functions can have their names omitted and be used as values in-line in an expression. We can rewrite the last example like this:

```
def addResults(functionA: const () -> int, functionB: const () -> int) {
	return functionA() + functionB()
}

const var numberFunctions = [def() { return 5 }, def() { return 10 }]

addResults(numberFunctions[0], numberFunctions[1]) == 15
```

## Named Arguments

When calling a function, you can name the arguments from the function in any order you prefer:

```
def add(a: int, b: int) {
	return a + b
}

add(a: 5, b: 6) == add(b: 6, a: 5)
```

When naming an argument, if the arguments following it are unnamed, the compiler will try to match them to the next parameter in the function (without wrapping around past the end). If the compiler can't figure out how to map the arguments to parameters, they'll have to be named to compile correctly.
