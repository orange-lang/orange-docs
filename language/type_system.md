## Type System
**STATUS**: Implemented

Every variable and expression has a type in Orange. Orange defines the following basic types for use in source programs:

1. bool
2. int8 (or char)
3. int16
4. int32
5. int64 (or int)
6. uint8
7. uint16
8. uint32 
9. uint64 (or uint)
10. float
11. double

As you would expect, the difference between `int` and `uint` is that `uint` is unsigned, and the difference between `int8` and `int16` is that `int8` takes up 8 bits, while `int16` takes up 16 bits.

The size in bytes of an expression or variable can be accessed via `sizeof`:

    sizeof(_expression or type_)

The `sizeof` operator acts a function, returning a `uint64`. It can be used in expressions like `8 + sizeof(int64)` and will give you the size of arrays with a variable length of elements:

```
    var n = 50 
    sizeof(int8[n]) # => 50
```

The listed types were ordered by _type precedence_, from lowest to highest. This means that doing an operation between two types of unmatching types will have the type of the lower precedence casted to the other type. 

By default, integers in orange default to signed 64-bit integers (i.e., `int64`). You can append type suffixes to a constant to give it a different type: 

- `u` for unsigned (defaults to 64-bit)
- `u8` for unsigned 8-bit
- `u16` for unsigned 16-bit 
- `u32` for unsigned 32-bit
- `u64` for unsigned 64-bit 
- `i` for signed (defaults to 64-bit)
- `i8` for signed 8-bit
- `i16` for signed 16-bit
- `i32` for signed 32-bit
- `i64` for signed 64-bit
- `f` for float (only works with floating point numbers)

Any floating point number requires a decimal plus one digit, like `5.0`. By default, a floating point number is a `double`, unless specified with the suffix `f`. That is to say, `5.0f` is a `float`. 
