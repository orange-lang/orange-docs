# Casts

Casts allow you to convert from one type to another. Internally, they are implemented by adding a constructor via a type extension.

All builtin numeric types can be casted interchangably, but note that some information may be lost in the casts.

Casting is done by calling the type as if it was a function, with the argument being the value.

```
double(5) // coerces 5 to be of type double
int64(5.2) // coerces 5.2 to be of type int64
```

Example implementation:

```
extend double {
	def double(v: int): /* internal implementation */
}
```
