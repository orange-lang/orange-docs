# Packages and Namespaces

Orange files can define types in the context of a package and namespaces inside that package. Defining a package simply means defining a root namespace for the rest of the file.

```
package My.Package

public def foo() {
	return "Foo!"
}
```

This program defines a method called `My.Package.foo`.

Namespaces define namespaces in a smaller scope. If no package statement is included, they are global, otherwise they're nested inside the package.

```
package My.Package

namespace Namespace {
	// use as My.Package.Namespace
}
```

```
namespace Namespace {
	// use as Namespace
}
```

Other files can import code from packages and namespaces with the `import` directive. `import My.Package` imports the functions and types defined inside `My.Package` into the current file for use.

Importing can import into a custom global namespace. Using our `My.Package.foo` example:

```
import My.Package = FooPackage

FooPackage.foo() == "Foo!" // true
```
