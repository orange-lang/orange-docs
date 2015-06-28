# External Functions
**STATUS**: Implemented

Orange links against libc by default, so you can add an external reference to any C function contained in that library.

`extern _function name_(_param list_) -> _return type_` 

When trying to access an external function, you must declare the type for each parameter. For `printf`, this means:

``` 
# OK
extern printf(char* str, ...) -> int32 

# BAD - Won't compile!
extern printf(s, ...) -> int32
```
