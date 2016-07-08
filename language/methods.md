# Methods

A method is a function defined inside a class, and defines a function that can be used on an instance of that class.

    class Pet {
        public species: Species
        public name: name
        public age: int

        public def sayHello() {
            println("Hi, I'm {name}!")
        }
    }

    var polly = Pet()
    polly.name = "Polly"
    polly.sayHello() // prints "Hi, I'm Polly!"

Inside a class method, a special variable called `this` is defined. `this` refers to the specific instance of the class upon which the method is being called. For example, `this.name` inside of `Pet.sayHello` would refer to that pet's name. However, `this` can be omitted unless the name of the member you're trying to access has been shadowed.

## Constructors and Destructors

    identifier -> "~" identifier

Constructors can be used to couple custom initialization code for a class. Destructors are like constructors, but execute when the class instance is deleted.

The name of a constructor is the name of the class, and the name of a destructor is the name of the class, prefixed with a ~.

Class instances will be deleted when the object goes out of scope _or_, if the object is a pointer, when its memory is deleted.

Constructors can also take parameters. If you wish to make `Pet` more complex, where its species, name, and age could only be set once, you can use constructors to achieve that behavior:

    class Pet {
        private var species: Species
        private var name: string
        private var age: int

        public def getSpecies(): species
        public def getName(): name
        public def getAge(): age

        public def sayHello() {
            println("Hi, I'm {name}!")
        }

        public def Pet(species: Species, name: string, age: int) {
            this.species = species
            this.name = name
            this.age = age
        }

        public def ~Pet() {
            println("{name} says goodbye!")
        }
    }

    var polly = Pet(Species.Parrot, "Polly", 1)
    polly.sayHello() // prints "Hi, I'm Polly!"

## Operator Overloading

	identifier -> "operator" operator

Certain operators can be overloaded by a class to call custom behavior: `+`, `- (binary)`, `* (binary)`, `%` `- (unary)`, `* (unary)`, `[]`, `++`, `--`, `<<`, `>>`, `|`, `& (binary)`, `^`, `<`, `>`, `<=`, `>=`, `!=`, `==`, `+=`, `-=`, `/=`, `*=`, `%=`, `<<=`, `>>=`, `()`.

An operator is overloaded just like declaring a function, but the name of the function is `operator` followed by the name of the operator.

    class Number {
        private mInternal: int

        public def value(): mInternal

        public def Number(val: int): mInternal = val;

        public def operator+(other: Number) -> Number:
            Number(mInternal + other.mInternal)
    }

    var a = Number(5)
    var b = Number(52)
    var c = a + b
    // c.value() == 57
