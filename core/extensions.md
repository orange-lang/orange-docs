# Extensions

Any existing type can have more methods defined on it, or implement an existing interface. This includes implementing methods on tuples, enums, strict aliases, classes, and arrays.

Let's define a sum method on an array of `int`:

```
extend int[] {
	def sum() {
		return for (var i, total = (0, 0); i < this.length; i++) {
			yield total += this[i]
		}
	}
}

[0,1,2,3,4].sum() == 10 // true
```

Inside an extension, `this` refers to the value the method is being called on. In this case, the type of `this` was `int[]&`.

We can also extend a type to implement an interface (or shadow it if it's automatically generated):

```
enum Day {
	Monday,
	Tuesday,
	Wednesday,
	Thursday,
	Friday,
	Saturday,
	Sunday
}

extend Day : Ordered<Day> {
	def operator<(lhs: Day, rhs: Day) {
		return switch ((lhs, rhs)) {
			(Friday, _): false,
			(_, Friday): true,
			(l, r): return (l as int) < (r as int)
		}
	}

	def operator>(lhs: Day, rhs: Day): !(lhs < rhs)
}
```

This shadows the default implementation of `Ordered` for enums to assert that Friday is, and always will be, the best day.

You can only shadow interfaces and methods that are implemented by default; if any method or interface is defined explicitly, it cannot be shadowed for that type, even if the method is virtual. (Virtual methods may only be overriden in subtypes).

## Extending Constructors

It's also possible to add constructors to existing methods. This is synonymous with a "cast" if there's only one parameter. Like other methods, you can only define a constructor that has not been defined before, or shadow a default one (e.g., the copy constructor for a type).

Builtin types implement copy constructors and constructors for type conversions; these are considered concrete and may not be overriden.

## Generic Extensions

Combining generics and extensions allow for adding behavior to _all_ types. This is used internally to implement some default behaviors, like the default constructor for compound types:

```
extend<T> T* {
	// Default constructor for a pointer is a null value
	def T(): null

	// Access operator, allows for a.b instead of (*a).b
	def operator.() -> T {
		return *this
	}
}
```

```
extend<T> T[] {
	// Default constructor for an array is an empty array
	def T(): []

	def length() -> int {
		// internal implementation
	}
}
```

Note that the restrictions on redefining functions for existing types still apply to generic extensions, so it would be wise to use generic extensions sparingly.
