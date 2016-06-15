# Namespaces &amp; Packages

	namespace -> "namespace" identifier block?
	import    -> "import" identifier

	statement -> namespace term | import term

In Orange, code may be oragnized into a hierarchy of different packages and namespaces. By convention, the namespace of a file will be its path inside a project directory. For example, if a file is in `Main/util`, its namespace would be `Main.util`.

A namespace can be defined with a namespace statement: `namespace namespaceName`. The namespace can contain periods, which indicate sub-namespaces. Subsequently, a namespace can be defined as a block: `namespace namespace { /* code */ }`. Any code inside that block would belong to that namespace. Note that using the namespace with a semicolon means that the whole file, including other namespace blocks, are children of that namespace defined.

A package is a compiled unit of Orange code. It may contain multiple namespaces. When a Package is being included by the compiler, all of its namespaces are accessible to any file in the project. If a package defined a namespace `TestLibrary.TestFunctions.Test`, your code unit may import `TestLibrary.TestFunctions` to just refer to `Test` without the namespace. This is done via an _import statement_: `import namespaceName`, or with our example, `import TestLibrary.TestFunctions`.

When importing a namespace, you can give a namespace a different name to refer to it as in your code. For example, if you did `import TestLibrary.TestFunctions = T`, you'd refer to `TestLibrary.TestFunctions.Test` in your code as `T.Test`. You can still use the full namepath if desired; importing simply creates a shortcut to the full name, but does not remove the original.
