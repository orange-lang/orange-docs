# Variables
**STATUS**: Implemented

A variable in orange does not need to be declared with a type, although it can. The specific type of a variable can be omitted by replacing it with a generic `var` keyword. For example, the statements `var a = 5` and `int a = 5` are equivalent. When the `var` keyword is used, the type of the variable will be determined from its value. 

If you omit the initial value when creating a variable with `var`, the type of the variable will be determined from the first thing it is assigned. If it is never assigned a value, an error will be thrown.  

    # VALID 
    int a 

    # VALID; a is an int 
    var a = 0

    # ERROR; no value to determine type from  
    var a

    # VALID; a is an int 
    var a 
    a = 0 
