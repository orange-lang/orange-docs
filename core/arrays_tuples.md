# Arrays and Tuples

The two builtin container types in Orange are arrays and tuples.

## Arrays

Arrays are a collection of zero or more values of a single type. They can be formed by having a comma-delimited list of values enclosed in brackets. For example, `[0,1,2,3,4]` is an array of numbers and `["hello", "goodbye"]` is an array of `string` (or more appropriately, an array of `char[]`).

The type of an array is the container type plus a `[]`.

The values in an array can be accessed by adding `[index]` to an expression whose type is an array. For example, the value of `[0,2,4,6,8][3]` is `6`.

Arrays store their length internally, which can be access with `.length`.

```
[0,1,2,3,4].length == 5
```

### Constrained Array Type

If you wanted to enforce an array type to have a certain number of values, you could enclose a constant integer inside the brackets when writing the type. For example, `int[5]` is an array of 5 `int`s.

## Tuples

A tuple is a collection of two or more values of any combination of types. They are formed similarly to arrays, except instead of enclosing the collection in square brackets, they're enclosed in parenthesis.

Since tuples don't have the constraint of all the values of being the same type, you can store anything you want in them: `("dog", 52u)` would be a tuple of a `string` and `uint`, written as `(string, uint)`.

You can access the members of a tuple with the dot syntax (`.index`). From our example earlier, these following expressions hold:

```
("dog", 52u).0 == "dog" // true
("dog", 52u).1 == 52u   // true
```

### Named Tuples

Optionally, you can name each component in the tuple and have the option of using the traditional `.index` syntax for accessing the components or `.name`.

```
(animal: "dog", someNumber: 52u).animal == "dog" // true
(animal: "dog", someNumber: 52u).0 == "dog"      // true
```

You don't have to name every component; you can only name one, if that is preferred.

Note that using named tuples is a constraint just like providing the size of an array in the array's type. For all Orange is concerned, `(string, uint) and (animal: string, someNumber: uint)` are different types, even though they store the same values.

This may seem pointless and restrictive, but it stops from accidentally interchanging `(country: string, countryAge: uint)` and `(animal: string, someNumber: uint)` in your code.
