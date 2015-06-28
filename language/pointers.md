# Pointers
**STATUS**: Implemented

Orange has C-style pointer support. Using `&` on a variable will return a pointer to that variable's type, equal to its location in memory. Using `*` on a variable will modify the value at that memory location. 

For example:

    var a = 5
    var b = &a  # b has the type of (int*)
    *b = 6
    # a == 6 

If you wanted to declare b explicitly, you could've declared it as `int* b` (or `int *b` or `int * b`, for that matter).

As stated in the section for arrays, arrays are essentially pointers in Orange and can be used as such:

    var a = [0...5]
    *a = 5 # a == [5, 1, 2, 3, 4, 5]
