# Arrays in Functions
**STATUS**: Implemented 

Arrays in functions, whether explicitly declared as a pointer `*` or array `[]`, will be treated as pointers. This is so they can be passed by reference. The downfall to this is `sizeof` will not return the size of the array including elements inside of a function; instead of will just return the size of the pointer.