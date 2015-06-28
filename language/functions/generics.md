# Generics
**STATUS**: Implemented

I'm going to provide an example for this entire section:

    def add(a, b)
        return a + b
    end

When you call this function with two ints, `add(3, 5)`, a copy of `add` called `addll` is created internally. It has the same code with the proper types being set. The copy will only be created once for the number of arguments passed. That is to say, there will never be more than one `addll` created, but there can be an `addll` and an `addFl`. See [Name Mangling](mangling.md) for how these names are determined 

Not all of the parameters have to be generic for it to be a generic function. For example, 

    def add(a, int b) 
        return a + b
    end 

Is still a generic function. Calling `add(3, 5)` and `add(3.0, 5)` will create the functions `addll` and `addFl` respectively.

This contrasts from a non-generic function: 

    def add(int a, int b) 
        return a + b
    end

No copies of this function will be made since none of the parameters are generic. 
