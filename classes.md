# Classes

	class         -> "class" identifier (":" super_list)?
	super_list    -> identifier? | identififer ("," identifier)*
	partial_class -> "partial" class

	statement     -> class 

A class is essentially a named tuple that supports methods. An example class called `Animal` is defined below.

    enum Species {
        Dog,
        Cat,
        Parrot
    }

    class Pet {
        public Species species;
        public string name;
        public int age;
    }

An instance of `Pet` has to be created by calling `Pet` like a method, which calls `Pet`'s _constructor_ (see Methods for creating new constructors).

From there, any public member of `Pet` can be accessed using the dot syntax.

    var polly = Pet(); // or: Pet polly = Pet();
    polly.species = Species.Parrot;
    polly.name = "Polly";
    polly.age = 1;

Inside of a class, privacy indicators have a different meaning. A `public` member or method can be used anywhere, where as a `protected` member or method can only be used by the class that defines it or children classes. `private` can only be used inside the class that defines it.

## Partial Classes

Classes in the same compilation unit can be marked as partial to spread out the implementation and definition of a class across multiple files. It's as easy as prefixing the class definition with `partial`.

    partial class Pet {
        public string sayHello() { println("Hello! I am {age} years old."); }
    }

    partial class Pet {
        private int age;
        Pet(int age) { this.age = age; }
    }

If using partial classes, all class fragments must be marked as partial. Each partial fragment is allowed to define more members for that class.
