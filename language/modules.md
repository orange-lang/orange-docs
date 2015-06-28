# Modules
**STATUS**: Design Phase

Once your code starts getting a bit long, you'll need modules to separate code into its own pieces. You can insert `package __packageName__` in your file to indicate that it's part of a package. Then, you can use `import __packageName__` in other files to include it. See section 4.4 to know how this comes together on the compiler side. 

Example:

`mymath.or`:

    package my.math 

    def add(a, b)
        return a + b
    end 

`main.or`:

    import my.math
    return add(5, 3) # program returns 8

When `importing` a package, all of the code inside of that package will be executed. 

In the example above, we were creating a main program and the types of `add` were resolved. However, generics are handled differently while creating a library, since their types can't be resolved after compilation. By default, they will be resolved to take `Object` from the standard library as parameters, and use operator overloading to resolve all of the code. This has a computational overhead, so you may instead want to `export` some types to be available.  

When you `export` types of a function, you're essentially forcing the generic clone to be created. For example, if we added the following code to `mymath.or`:

    export add(uint64, uint64)
    export add(double, double)

This will export two versions of `add`, one which takes two `uint64` as parameters and another which takes two `double`s as parameters. 