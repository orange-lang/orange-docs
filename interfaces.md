# Interfaces

	interface -> "interface" identifier block
	statement -> interface 

Interfaces are memberless classes that declare (but not define) methods. Certain classes will _implement_ these interfaces, which means any method defined in an interface will be valid to use on a class.

    interface InterfaceName {
       // method declarations, without bodies
    }

For example:

    interface Talker {
       def saySomething() -> string;
    }

Methods in an interface _must_ have a return value, since it cannot be inferred from some implementation's body.

Interfaces can also be used as valid typenames. If an interface is used as a type, the only operations valid on that interface are its defined methods, unless you cast the interface to an object of a class that implements it (see Type Casting) for more information.

When defining a class, you can place a `:` after the class name, and a list of interfaces that the class implements, separated by commas. After a class is said to implement some interface, all functions declared in that interface must be implemented.
