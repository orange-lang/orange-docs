# Properties

	getter    -> "get" block
	setter    -> "set" block

	property  -> "property" identifier ("->" type)? block

	statement -> getter | setter | property

Properties are methods that are used like regular members. They can be defined in interfaces, and can indicate whether or not they provide a getter and a setter. Going back to our `Pet` example, we can replace the `getName` with a property:


    class Pet {
        private var species: Species
        private var name: string
        private var age: int

        public property Species -> Species {
			get: species
        }

        public property Name -> string {
			get: name
        }

        public property Age -> int {
			get: age
			set: age = value
        }

        public def Pet(species: Species, name: string, age: int) {
            this.species = species
            this.name = name
            this.age = age
        }
    }

    var polly = Pet(Species.Parrot, "Polly", 1)
    println("Polly's age: {polly.Age}") // valid, as a getter is defined for Age.
    polly.Age = 2 // valid, as a setter is defined for Age

If the type of the property is ommited, it is inferred from the get.

The shorthand blocks can be used as well with properties. Using that format will cause the getter and setter to access and modify the expression. It's useful if you want to have placeholders for accessing private members where custom code may be added later. Our three properties could be replaced with the following:

	// Types omitted for inferrence, but could be defined explicitly
	public property Species: species
	public property Name: name
	public property Age: age

Note that the expression of the short-hand property block must be an lvalue to compile properly.

Getters and setters are functions, so any code can be executed in them. In a setter, `value` is defined as the new value being assigned to the property. It can be ignored if desired.

The `get` and `set` components of a property can be set to `public`, `protected` or `private` if so desired. The default privacy level for get/sets of properties is `public`.
