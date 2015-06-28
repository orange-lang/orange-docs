Orange is a language designed to give users the strength of C++ code while avoiding all of its unnecessary syntantic clunkyness. Its syntax is very similar to a scripting language, allowing for quickly writing complex code that performs well. 

Orange does not have a `main` function; the code you write inside of your source file directly is the main function itself. This means you can have a program that returns 0 all in one line:

`return 0` 

Your program can omit the return function. If this happens, your program will return 0 by default. However, the return value must be an integer. Other values will be casted to integers (if possible). 