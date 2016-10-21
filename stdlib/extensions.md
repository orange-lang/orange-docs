# Extensions

The standard library provides a set of extensions that can be used.

## For Each

`foreach` is a loop construct that operates on a `Enumerable<T>` type.

```
foreach (var object in enumerableObject) {
	// do something with object
}
```

## Array Ranges

An array range is a custom type that implements `Enumerble<T>`.

```
[a .. b] // exclusive range from a to b
[a ... b] // inclusive range from a to b
```

## Type attributes

Type attributes allow for giving types static information that can be queried at runtime.

The full information for this is not yet determined.

## String Interpretation

The standard library replaces lexing strings to allow for interpreting expressions inside a string if the expression takes the form of `${expression}`.

For example, `"3 + 5 is ${3 + 5}"` would be equal to the string `"3 + 5 is 8"`.

## Suffixes

Suffixes allow a friendlier way to create instances of strict aliases.

```
strict alias MilesPerHour = uint

suffix mph(num: uint): MilesPerHour(num)

50mph == MilesPerHour(50)
```

## Nullable Types

The standard library defines an extension where adding a `?` to any type transforms it into `Nullable<Type>`. For example, `int?` is `Nullable<int>`.
