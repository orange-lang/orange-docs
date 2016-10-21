# Casts

Casts allow you to convert from one type to another. It is a static operator defined from one type to another via the `Castable<From, To>` interface.

All builtin numeric types can be casted interchangably, but note that some information may be lost in the casts.

Casting is done via the `as` keyword.

```
5 as double // coerces 5 to be of type double
```
