# Enum
**STATUS**: Implemented

Enums are a list of named _constant_ values. 

    enum _Enum Name_
        [_NAME_ [ = _VALUE_]]+
    end

Enums must have at least one name assigned to them. You don't have to give them values; values will start at 0. Each subsequent automatically-assigned value will be equal to the previous value (automatically assigned or otherwise) + 1. 

For example,

    enum MyEnum
        A           # MyEnum.A == 0 
        B           # MyEnum.B == 1 
        C = 5       # MyEnum.C == 5
        D           # MyEnum.D == 6 
        E           # MyEnum.E == 7
    end 

An enum's members can be accessed with `_ENUM NAME_._ENUM VALUE_`. For example, in the previous example, `MyEnum.A` would access `A` in `MyEnum`. 

Enums can only have numbers that are integers; floats and doubles are not supported. 
