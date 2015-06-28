# Inline Assembly
**STATUS**: Design Phase 

Inline assembly can be accomplished with `$`. It is created with GAS syntax. For example:

`$xor %rax, %rax`

You can also use variables with `@`. 

`$mov @myAge, %rax`

or 

`$mov %rax, @myAge`

The overall syntax is:

`$ _assembly_ : clobbers`
