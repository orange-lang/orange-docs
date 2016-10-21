# Privacy

Defined types have a privacy modifier that define how they can be used externally. There are four different privacy values:

- `public`: usable from anywhere
- `package`: usable from package
- `protected`: usable from sub-types
- `private`: only usable locally (in current file/class, context-sensitive)

The default type for functions, enums, and classes is `package`. The default type for class members, methods, and properties is `protected`.

Packages and namespaces do not accept privacy modifiers.
