# Aliases

Orange allows you to define aliases for your types to give them friendlier names. For example, the alias `string` is builtin to be identical to `char[]`.

They can be defined in your code with the following:

```
alias aliasName = originalTypeName
```

These types are interchangable. Using `string` as an example again, any function that takes `char[]` as a parameter can be given a `char[]` or a `string` as an argument.

## Strict Aliases

Strict aliases allow you to force Orange to treat the aliases as separate types from the original, despite internally being stored the same. They can be created by prefixing `strict` to your alias declaration.

```
strict alias MilesPerHour = int
```

When a strict alias is declared, to create a value of that type, you must have to call it as if it was a function:

```
MilesPerHour(55)
```

In fact, the name of the strict alias is a function, so it could be passed as a function reference. In this case, the type of the function is `(int) -> MilesPerHour`.

Strict aliases are safer than regular aliases in that they are not interchangeable with the original type or other aliases that refer to the same type. With `MilesPerHour`, a function that takes `int` as a parameter could not be given a `MilesPerHour` argument.

In [the Suffix Extension](../stdlib/extensions.md#suffixes) we'll see that we can create a friendlier way to refer to strict aliases.
