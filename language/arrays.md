# Arrays
**STATUS**: Implemented

Arrays in Orange use the following syntax:

    [ _expression_ [[ , _expression 2_ ]] * ]

For example, `[4]` and `[1, 2, 3, 4]` are both valid arrays. In both of these examples, the arrays are of type `int[]`. Like variables, the type of arrays use data morphing. The type of the array is determined by the largest precedence element of the array. That is to say, if one of the elements is a double, the array is a `double[]`. 

Internally, like in C, arrays are pointers, and can be used as such. This means you can assign one array to another by reference: 

    var a = [0, 1, 2]
    var b = a # b and a are pointing to the same memory location 

For more information on Pointers, see [Pointers](pointers.md).

Similar to regular variables, arrays can morph, too: 

    var a = [0, 1, 2]
    a[0] += 0.5 # a should be an array of doubles now 

    if a[0] >= 0.5 
        # this code will execute!
    end