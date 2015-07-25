# Modules
**STATUS**: Design Phase

Once your code starts getting a bit long, you'll need modules to separate code into its own pieces. You can insert `package __packageName__` in your file to indicate that it's part of a package. Then, you can use `import __packageName__` in other files to include it. See section 4.4 to know how this comes together on the compiler side. 

Example:

`mymath.or`:

    package my.math 

    def add(var a, var b)
        return a + b
    end 

`main.or`:

    import my.math
    return add(5, 3) # program returns 8

When `importing` a package, all of the code inside of that package will be executed. 

In the example above, we were creating a main program and the types of `add` were resolved. 

When modules are compiled, they compile to two things:
    1. Object files 
    2. Orange Bitcode 

Object files are what you would normally expect functions and classes to compile to; they're code that you can link against to use. However, when using generic functions and classes, Orange can't compile those to native code since there are no defined types for them yet. 

Orange's solution is to take all generic classes and functions and store them in Orange Bitcode (a serialized form of the AST). It is stored with your object file as metadata. When these classes and functions are used, they are  parsed, compiled to native code, and stored in a global cache.

The global cache is used such that each combination of arguments to a generic function or class only have to be compiled once per system. Once you use a function a certain way, you only have to deal with the slow compile times once. Afterwards, Orange will just link the used object files from the cache as normal.  

When you `export` types of a function, you're essentially forcing the generic clone to be created in the cache. For example, if we added the following code to `mymath.or`:

    export add(uint64, uint64)
    export add(double, double)

This will export two versions of `add`, one which takes two `uint64` as parameters and another which takes two `double`s as parameters. 