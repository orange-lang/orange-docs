# Extensions

Any existing type can have more methods defined on it, or implement an existing interface. This includes implementing methods on tuples, enums, strict aliases, classes, and arrays.

Let's define a sum method on an array of `int`:

```
extend int {
	def sum() {
		return for (var i, total = (0, 0); i < this.length; i++) {
			yield total += this[i]
		}
	}
}

[0,1,2,3,4].sum() == 10 // true
```

Inside an extension, `this` refers to the value the method is being called on. In this case, the type of `this` was `int&`.

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
}
```

This shadows the automatic implemented of `Ordered` for enums to assert that Friday is, and always will be, the best day.
