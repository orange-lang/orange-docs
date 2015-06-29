# Operator Overloading 
**STATUS**: Design Phase 

The following operators can be overloaded: `+`, `-`, `/`, `*`, `==`, `.`. 

An operator overload is similar to a function, but instead of `def`, you use `operator`, and instead of a function name, you use the operator. From there, the parameters are LHS and RHS to denote the left-hand side of the operator and the right-hand side, respectively. 

With operator overloading, generics can't be used; each parameter requires a type. 

Note that with `.`, there is no `lhs` and `rhs` parameters. Instead, it's replaced with `name`, which is the name of the member trying to be accessed. 

Example:

    class Person
        var name, age 

        operator +(Person lhs, Person rhs) 
            return Person("Some baby", 0)
        end

        def Person(name, age)
            me.name = name
            me.age = age
        end
    end

    bob = Person("Bob Person", 32)
    alice = Person("Alice Person", 33)

    baby = bob + alice
