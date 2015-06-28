# Name Mangling
**STATUS**: Implemented

The types of arguments are internally appended to the end of the function on creation. This is never exposed to the programmer. Name mangling starts with the base function name, and then appending a letter for each of the parameter types.

- If the parameter type is a 1-bit integer, `T` is appended.
- If the parameter type is an int8, `b` is appended. `B` is appended for uint8.
- `s` is appended for int16, `S` for uint16.
- `i` is appended for int32, `I` for uint32.
- `l` is appended for int64, `L` for uint64.
- `f` is appended for floats, `F` for doubles.
- `?` will be appended for any unknown type; this will only appear in compiler bugs.

Additionally, a `p` is appended for each pointer and array dimension. 

For example, `int*` would be `lp`. `int[5]` would be `lp`, as well. Likewise, `int[5][3]` would be `lpp` and `int*[5][3]` would be `lppp`. 
