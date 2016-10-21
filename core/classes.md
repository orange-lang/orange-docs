# Class

In Orange, a class is essentially a named tuple that is defined with optional methods, properties, and inheritance from a single base type.

Here's an example of a `Dog` class:

```
enum DogType {
	GoodDog,
	WeirdDog
}

extend DogType : Printable<DogType> {
	def toString() {
		return switch (this) {
			DogType.GoodDog: "good dog",
			DogType.WeirdDog: "weird dog"
		}
	}
}

class Dog {
	var name: string
	var age: uint
	var type: DogType

	def bark(): Console.Log("Woof. I am a ${age} year old dog named ${name} and I am a ${type}.")

	def Dog(name: string, age: uint, type: DogType) {
		this.name = name
		this.age = age
		this.type = type
	}

	def ~Dog() {
		Console.Log("Goodbye, human. Woof.")
	}
}

var weirdDog = Dog("Fido", 4, DogType.WeirdDog)
weirdDog.bark() // => Woof. I am a 4 year old dog named Fido and I am a weird dog.


// => Goodbye, human. Woof.
```

The method on `Dog` called `Dog` is a constructor; it is a method that is called upon creation of the class type with all the provided parameters. The `~Dog` method is a descructor and is called when the object is out of scope (if it was created on the stack, or if deleted manually otherwise).

## Properties

Properties are methods that are used like normal object members. A property is defined with one or both of a getter and setter. If only a getter is defined, the property can not appear on the left-hand side of an assignment. If only a setter is defined, the property can not appear on the right-hand side of an assignment.

The various ways to deeclare a property are as follows:

```
property PropertyName -> optionalType {
	get { yield someExpression }
	set(value: someType) {
		// something
	}
}

property PropertyName {
	get: someExpression
	set: someExpression // type of value is inferred from type of someExpression
}

// in here, get/set is automatically generated. get will return someExpression
// and set will change someExpression.
property PropertyName: someExpression

// when readonly, no set is generated. If this was in the long-block format,
// defining a set would be a compilation error.
readonly property PropertyName: someExpression
```

Note that `extend` supports defining properties on the extended type.

## Inheritance

A class can implement a any number of interfaces or extend a single type.

When defining a class, after the class name, include a semicolon and include the list of interfaces and optional parent class. The parent class must be a class and not a builtin type like int or a tuple.

When inheritance of a parent type is in affect, one of the parent constructors must be explicitly called if it is not an implicit constructor. This must be done via calling the `super` keyword as a function in all constructors of the child class.

If both the parent and the child class have default constructors, this happens automatically.

## Partial Class

A class marked as partial (`partial class MyClassName`) means that multiple definitions of the class (also marked with partial) can occur anywhere in the project and define new methods and members on the class.
