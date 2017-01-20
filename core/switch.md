# Switch

In Orange, a switch statement is like an if statement that allows for executing code based on certain patterns.

```
switch (expression) {
	pattern: {
		// code
	},
	pattern: {
		// code
	},
	// ...
}
```

Note that Orange also supports short blocks here, as well:

```
switch (expression) {
	pattern: expression,
	pattern: expression,
	// ...
}
```

## Patterns

Patterns can do a lot of things:

- Check for a constant
- Bind to a variable
- Decouple tuples and enums
- Do a logical or
- Have guards

### Constant

If a pattern is a constant, the pattern will only match if the value of the expression being switched on matches the value of the constant:

```
switch ("dog") {
	"cat": Console.Print("Meow!"),
	"dog": Console.Print("Woof!"),
	"cow": Console.Print("Moo!")
}
```

### Binding

If a pattern is a binding, the pattern defines a variable name that will be equal to the value of the expression.

```
switch ("dog") {
	x: {
		// x == "dog"
	}
}
```

### Decoupling

By combining binding and decoupling, users can access the components of an enum. Starting with tuples:

```
var myTuple = ("dog", 52u)

switch (myTuple) {
	(animal, 16u): Console.Print("A 16 pound animal!"),
	(animal, weight): {
		// do something with this heavy-ish animal
	}
}
```

And enums:

```
enum Status {
	STOPPED,
	RUNNING(since: Date)
}

switch (Status.Running(Date.now)) {
	Status.STOPPED: Console.Print("Not running."),
	Status.Running(since: x): Console.Print("Running since ${x}")
}
```

### Combining

Patterns can be combined by using `||` like a logical OR.

```
def isBinaryDigit(digit: int64) {
	return switch (digit) {
		0 || 1: true,
		_: false
	}
}
```

### Guards

Guards are an if statement that executes before the rest of pattern is checked, and affects whether or not the pattern matches.

```
def isAlive(age: int64) {
	return switch (age) {
		_ if age > 200: {
			// find out their secret to eternal life
			yield true
		},
		_ if age < 0: false,
		_: true
	}
}
```
