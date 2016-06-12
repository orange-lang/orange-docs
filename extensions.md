# Extensions

	extension -> "extend" identifier (":" super_list)? block
	statement -> extension


Existing classes can have their functionality extended with new behavior via Extensions. Extensions can declare a list of interfaces in their super list,
but not another class.

Extensions operate on existing non-`final` classes, and allow you to define an interface for an existing class, or add new methods or properties. Extensions only have access to public or proteced members of a class, but not private.

    class Dog {
        public def sleep() { /* some code */ }
    }

    extend Dog {
        public def bark() { /* more code */ }
    }

    var dog = Dog();
    dog.sleep();
    dog.bark();
