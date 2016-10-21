# Generic Types

Generic types are types that will morph based on context and can be constrained.

Generic types and constraints are defined inside a `<>` section, which is placed after the following keywords:

- `def`
- `class`
- `extend`
- `interface`

The generic types defined are comma delimited, like `<T,V>`.

Constraints also occur inside the generic section, prefixed with `where` (`<T,V where constraints`). Constraints are comma delimited and the only constraint at the moment is `=`, where the RHS of the expression is a base type or interface. `<T where T = Number<T>>` defines a generic type `T` where `T` must implement `Number`.

If when defining class members or function parameters, types can be omitted to be automatically assigned a generic type. For example:

```
def add(a, b): a + b
```

Defines a generic method where `a` and `b` will automatically be given generic types. Constraints will be determined from usage, and in this case, they must implement `Number<T>` to be added together.
