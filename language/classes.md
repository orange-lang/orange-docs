# Classes

	class         -> "class" identifier (":" super_list)? class_body
	super_list    -> identifier? | identififer ("," identifier)*
	partial_class -> "partial" class
	member_access -> identifier "." identifier

	class_body    -> "{" class_stmts? "}"
	class_stmts   -> class_stmt (term class_stmt)*

	class_stmt    -> implicit_var | class | function | aggregate
	class_stmt    -> extern_fn | import | extension | property
	class_stmt    -> enum

	statement     -> class
	expression    -> member_access

A class is essentially a named tuple that supports methods. An example class called `Animal` is defined below.

    enum Species {
        Dog,
        Cat,
        Parrot
    }

    class Pet {
        public species: Species
        public name: string
        public age: int
    }

An instance of `Pet` has to be created by calling `Pet` like a method, which calls `Pet`'s _constructor_ (see Methods for creating new constructors).

From there, any public member of `Pet` can be accessed using the dot syntax.

    var polly = Pet() // or: Pet polly = Pet()
    polly.species = Species.Parrot
    polly.name = "Polly"
    polly.age = 1

Inside of a class, privacy indicators have a different meaning. A `public` member or method can be used anywhere, where as a `protected` member or method can only be used by the class that defines it or children classes. `private` can only be used inside the class that defines it.

Also, the statements that are syntatically valid inside of a class are different than other blocks. Only declarative statements can be made; no expressions. This is done so support for declaring class members without `var` can be supported.

## Partial Classes

Classes in the same compilation unit can be marked as partial to spread out the implementation and definition of a class across multiple files. It's as easy as prefixing the class definition with `partial`.

    partial class Pet {
        public def sayHello(): println("Hello! I am {age} years old.")
    }

    partial class Pet {
        private age: int
        def Pet(age: int) { this.age = age }
    }

If using partial classes, all class fragments must be marked as partial. Each partial fragment is allowed to define more members for that class.
