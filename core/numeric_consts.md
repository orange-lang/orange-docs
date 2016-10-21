# Type of Numeric Constants

When refering to numbers, there are three important builtin interfaces to consider: `Number`, `Real`, and `Integer`. Number is the base interface, and `Real` and `Integer` are two distinct extensions from that.

Basic integers without prefixes or suffixes, like `5`, are simply the interface type `Number`. We consider this a _non-conrete_ type in that it does not yet have an actual non-interface type. The actual type will be infered based on its usage inside the scope.

Integers with a prefix or suffix will be `Integer` until it's resolved to a more specific type (`uint`, `int64`, etc).

Real numbers default to `Real` until it's resolved to either `float` or `double` (or a custom type that implements the `Real` interface).

If the type of a numeric constant can't be inferred through usage and there are no errors, it'll default to `int` for integers and `double` for real numbers.

Note that aliases and static aliases inherit the interfaces implemented on the base type, but static alises can have extra interfaces implemented on them that won't affect the base type. See [Extensions](extensions.md) for more information.
