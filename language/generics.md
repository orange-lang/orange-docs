# Generics

In a function and class, the keyword `var` can be applied to class members and function/method parameters to indicate a generic parameter.

If we defined the function `def add(var a, var b): a + b`, we will have created a generic fucntion. A generic function with a type being `var` means that a copy of the function will be created for each unique combination of types in which it is called. That means `add(3, 5)` and `add(3, 5.2)` create two different functions, where one takes two integers, and the other takes an integer and a double.

When var is used, each parameter gets its own, unique type. A generic type can be created by prefixing the parameter list with a list of generic types inside of `<>`. For example, `def add<T>(T a, T b)` will create a generic `add` where both parameters have to be the same type.

Orange can infer the type of `a` and `b` based on the types of the arguments to the function. If the types are different, you must explicitly define the type of `T` in the caller: like `add<int>(5, 2.3)` or `add<float>(1, 9.2f)`.

Multiple generic types can be defined as needed. `<T, V>` is a way to define two generic types named `T` and `V`, respectively.

## Generics with const values

Constant values can also be used as generic parameters: `def constAdd<N>(var a) { a + N }`
would add a constant value `N` to the parameter `a`. Note that since N is used as a value, it must be explicitly defined when calling the function, such as `constAdd<5>(myVar)`.

## Generic constraints

Constraints can be applied to generic types. Inside the generic definition of `<>`, adding a `:` after the list of generic names allows you to apply constaints, delimited by commas. The syntax to define a constraint starts with a `where`, followed by the generic type, and then the constraint.

Here are the list of valid constraints that can be used:

- `where T = class` - T must be an instance of a class
- `where T = new()` - T must have a default constructor that takes no arguments
- `where T = <base class>` - T must inherit from base class
- `where T = <interface>` - T must implement interface
- `where T = U` - T must be or derive from the type supplied for U.
- `where T = data <constraint>` - T must be data of another constraint.
- `where T = typename` - T must be any type, including plain data like int
- `where T = <typename>` - T must be of typename

For the `data <constraint>` constraint, our constAdd<N> could be constrained to: `def constAdd<N : where N = data int>(var a) { a + N }`.
