# Properties

	getter    -> "get" block
	setter    -> "set" block

	property  -> type identifier block

	statement -> getter | setter | property

Properties are methods that are used like regular members. They can be defined in interfaces, and can indicate whether or not they provide a getter and a setter. Going back to our `Pet` example, we can replace the `getName` with a property:


    class Pet {
        private Species species;
        private string name;
        private int age;

        public Species Species {
            get { species }
        }
        public string Name {
            get { name }
        }
        public int Age {
            get { age }
            set { age = value; }
        }

        public Pet(Species species, string name, int age) {
            this.species = species;
            this.name = name;
            this.age = age;
        }
    }

    var polly = Pet(Species.Parrot, "Polly", 1);
    println("Polly's age: {polly.Age}"); // valid, as a getter is defined for Age.
    polly.Age = 2; // valid, as a setter is defined for Age

Getters and setters are functions, so any code can be executed in them. In a setter, `value` is defined as the new value being assigned to the property. It can be ignored if desired.

The `get` and `set` components of a property can be set to `public`, `protected` or `private` if so desired. The default privacy level for get/sets of properties is `public`.
