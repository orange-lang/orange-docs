# Generic Types

Generic types are types that will morph based on context and can be constrained.

Generic types and constraints are defined inside a `<>` section, which is placed after the following keywords:

- `def`
- `class`
- `extend`
- `interface`

The generic types defined are comma delimited, like `<T,V>`.

For example, here is an add function where you add two values of type `T`: 

```
def<T> add(a: T, b: T) -> T { 
	return a + b 
}
```

Constraints also occur inside the generic section, prefixed with `where` (`<T,V where constraints>`). Constraints are comma delimited and the only constraint at the moment is `=`, where the RHS of the expression is a base type or interface. `<T where T = Number<T>>` defines a generic type `T` where `T` must implement `Number`.

If when defining class members or function parameters, types can be omitted to be automatically assigned a generic type. For example:

```
def add(a, b): a + b
```

Defines a generic method where `a` and `b` will automatically be given generic types. Constraints will be determined from usage, and in this case, they must implement `Number<T>` to be added together.

## Type Annotation and Instantiation

Declared types, like classes, can have their generic types explicitly annotated simiarily to how they were declared: `ClassName<TypeList>`. This syntax is valid in the context of declaring a type. However, if you wish to explicitly instantiate a generic function, you must prepend the `<TypeList>` with `.`. We call this type instantiation. For example, here is a type annotation:

```
var classInst : ClassName<int> 
```

And here is type instantiation using our `add` function from earlier:

```
var result = add.<int>(3, 5)
```

You may ask why we require the dot to instantiate a type in Orange. Languages like C++ do not require it, but it makes the grammar ambiguous. For example, would the following (invalid Orange) statement: `a<b>(5)` be equivalent to calling a function called a with a type of b, and an argument of 5? Or is it equivalent to comparing `a < b` and seeing if that result is greater than the expression `(5)`? This ambiguity is avoided by simply adding the `.`. 
