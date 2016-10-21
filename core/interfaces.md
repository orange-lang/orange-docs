# Interfaces

An interface defines a set of operations (called _methods_). that can be used on a specific type.

```
enum Food {
	TASTY,
	NOT_SO_TASTY
}

interface Animal {
	def eat(food: Food)
	def survive()
	def die()
}
```

Interfaces that have been defined can be used as types in functions or variable declarations.

Interfaces can extend other interfaces. For example, a Dog interface could extend Animal:

```
interface Dog : Animal {
	def bark()
}
```

Then a type that implements `Dog` can do anything an animal can do, plus bark. An interface can extend as many interfaces as it wants.

## Builtin Interfaces

Orange defines builtin operations via a set of builtin interfaces. For example, these are some (but not all) of the builtin interfaces:

```
interface<T> Number {
	static def operator+(lhs: T, rhs: T)
	static def operator-(lhs: T, rhs: T)
	static def operator*(lhs: T, rhs: T)
	static def operator/(lhs: T, rhs: T)

	def operator+=(lhs: T&, rhs: T)
	def operator-=(lhs: T&, rhs: T)
	def operator*=(lhs: T&, rhs: T)
	def operator/=(lhs: T&, rhs: T)
}

interface<T> Ordered {
	static def operator<(lhs: T: rhs: T)
	static def operator>(lhs: T: rhs: T)
	static def operator<=(lhs: T: rhs: T)
	static def operator>=(lhs: T: rhs: T)
}

interface<T> Comparable {
	static def operator==(lhs: T, rhs: T)
	static def operator!=(lhs: T, rhs: T)
}
```

When we get to [Generic Types](generic_types.md) the `<T>` will become clear, and we will explain the `&` type in [Pointers and References](pointers_and_references.md).

## Automatically Generated Interfaces

Sometimes declaring a new construct creates an interface that's automatically generated. Every possible function type has a signature that looks like this:

```
interface (args) -> retType {
	def operator()(/* arguments */) -> retType

	def apply(argList)
}
```

For example, a function with the type signature `(int, int) -> int` automatically implements this interface:

```
interface (int, int) -> int {
	def operator()(argA: int, argB: int) -> int

	def apply() -> ((int, int) -> int)
	def apply(argA: int) -> ((int) -> int)
	def apply(argA: int, argB: int) -> (() -> int)
}
```

The `apply` method allows us to create a new functions with some arguments pre-applied. It allows for things like this:

```
def add(a: int, b: int): a + b

var add5 = add.apply(5)
add5(52) == 57
```
