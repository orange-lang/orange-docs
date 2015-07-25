# Classes 
**STATUS**: Not Implemented 

    class _className_ [from _parentClass_] [implements _interfaces_]
        [[ [[ static ]] [[ private | public | protected ]] __variable__ ]] *
        [[ [[ static ]] [[ private | public | protected ]] __function__ ]] *
    end

Classes are represented here with confusing syntax, but the idea behind them is simple:
1. A class can have a list of variables, which can be static (e.g., they are class variables, not instance variables)
2. These variables can be private (e.g., can only be accessed by this class), protected (e.g., can only be accessed by this class or child classes), or public (e.g., can be accessed by anybody/anything).
3. A class can have a list of functions, which have the same accessor levels as variables do. 
4. A class can inherit from a parent class using `from`. By default, with the standard library, evey class inherits from `Object`. 
5. A classs can implement any interface using `implements`. 

The constructor function for the class is the class' name.

By default, the accessor level is `public`.

When declaring a variable, a type must be given. If you do not wish to give a type and have the morphing engine figure it out, let the type be `var`.

Here is an example of a class:

    class Person
        protected var name, age 

        def canDrink()
            return this.age >= 21
        end

        def Person(var name, var age)
            this.name = name
            this.age = age
        end
    end

    class Cat from Person
        def canDrink()
            return false
        end

        def Cat(var name, var age)
            super(name, age)
        end
    end

    var charlie = Person("Charlie Realperson", 22)
    # charlie.canDrink() == true 

    var real_cat = Cat("A Real Cat", 8)
    # rationally, real_cat.canDrink() == false

Note that `Cat` called `super` in its constructor; it was accessing the `super` class, `Person`. 

The `Cat` constructor here is optional: it was only included to demonstrate using the `super` class.

Members can be accessed by using `this._member_` or `@_member_`. For example, in the example above, `this.name` and `@name` are equivalent. 