# Inheritance

Any class can inherit the behavior and members of a class and extend its functionality. When declaring a class, you can put up to one parent class in the interface section. If this is done, this class is a _subclass_ and is said to inherit from a parent class. It inherits all members and methods.

The child class can access any of the parents methods and members that are either `protected` or `public`, but not `private`. The child class can define extra members or methods as needed.

The child class may refer to the parent class' methods by name, or if the members are shadowed, by using the name of the parent class or the keyword `super`.

Methods can be overriden by child classes by default. When storing an instance of a child class into a variable that is typed with a parent class, calling overriden methods will call the child class' implementation (this is called _polymorphism_. See [Pointers](Pointers.md) for more information). To avoid this, a method must be marked as `final` in the parent class:

    final def foo() {
        // implementation
    }

A child class can also mark a method as `final`. If you wish to shadow the implementation of a function, the function must be marked as shadows:

    shadows def foo() {
        // implementation
    }

Classes can also be marked as `final` to indicate that they cannot be inherited
from.

A shadowed definition will be called if a member is of the child class' type, but not of the parent class' type.

## Super class' constructor

In an explicit constructor for a child class, the parent class' constructor must also be called. This has to be done explicitly by calling `super` as if it were a function, and passing in the arguments to the constructor you wish to call.

## Runtime Type Information

Every class carries with it information about its type during runtime (this functionality can be disabled using compiler settings). When runtime type information is enabled, `expression instanceof ClassName` is an expression that will be `true` if the LHS expression is an object that is an instance of the specified RHS `ClassName`.
