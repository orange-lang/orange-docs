# Orange Mini

The C++ version of Orange is a slimmed down version of the full language so developement on a bootstrapped version of Orange can begin more quickly. We'll refer to this here as "Orange Mini"

Orange Mini lacks the following features:

- Tuples
- Switch statements
- Block-as-value
- Generics
- Interpolated strings
- Operator overloading
- Array range
- Yield
- Anonymous functions
- Aggregate functions
- Properties
- Foreach
- Reference types
- Named arguments
- Parametric enums (e.g., just simple names for enum values)

The Orange Mini standard library has only the following classes:

- Orange.IO.File
- Orange.IO.FileStream

The Orange.Kernel namespace (i.e., the namespace imported by default) has the following static objects and functions:

- Console (PrintLine, PrintError, Printf) (e.g., `Console.PrintLine("Hello")`)
