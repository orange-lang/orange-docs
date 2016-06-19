# Pointers

	new          -> "new" identifier
	delete       -> "delete" expression

	expression   -> new | delete
	pointer_type -> type "*"

	type         -> pointer_type 

In Orange, pointers can be used to refer to a memory location where a value of a specific type is stored. For example, `int*` refers to a memory location where an int is stored.

If you wish to create a new instance of any type on the heap, resulting in a pointer to memory where it is exists, you must use the new keyword:

    new TypeName

For our `int*` example, that would be `int* ourPointer = new int;`

You can couple this with a constructor: `Polly* p = new Pet(Species.Parrot, "Polly", 1);`
or you can couple it with a size to instantiate an array: `int[5]* a = new int[5];`

Note that with arrays, `int[5]*` is a pointer to five integers, and `int*[5]` is an array of 5 pointers (and `int*[5]*` is a pointer to an array of 5 pointers).

You can use `*` and `&` to dereference a pointer or get a reference to one. For example, to store `5` in the memory location pointed by `ourPointer`:

    int* ourPointer = new int;
    *ourPointer = 5;

Or to get a memory reference to a stack variable (i.e., a variable that is not created on the heap via `new`):

    int a = 5;
    int* ptr = &a;

Memory allocated in the heap via the `new` keyword can be deleted by using the `delete` keyword.

    int* ptr = new int;
    delete ptr;

Unlike in C, we don't use `->` to access class members of a pointer to a class. `.` is always used and Orange will intelligentally dereference the pointer as needed.

## Reference Types

`&` may be suffixed to a type to indicate a reference to a particular type. For example, `int&` indicates a reference to an integer. In a function, changing the value of the parameter  will change the value of the argument passed to it. This is different than a parameter of `int*` as the caller will not need to pass `&someVariable` as an argument.

## Automatic Reference Counting

If Automatic Reference Counting is enabled (which it is by default), objects allocated via the heap will keep track of the number of references to that object (incremented when copied, decremented when going out of scope). When the number of references reaches zero, that object will be deallocated automatically.

When automatic reference counting is enabled, objects may not be deleted manually. It can be disabled in the compiler settings to enable fine-grain control of memory.
