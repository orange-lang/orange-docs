# Pointers and References

There are two extra builtin types, pointers and references. Pointers are a container type that point to another type in memory, designated by the base type and an asterisk (like `int*`).

Pointers implement `Deref<T>` and the unary `*` operator which allow dereferencing the pointer and getting the value at the location the pointer is refering.

All variables implement `Ref<T>` and the unary `&` operator which gets a pointer to that variable.  

References also point to another type in memory like pointers, but are used like normal values. Re-assigning the value of a reference changes the value the reference is pointing at, rather than where the reference is pointing.
