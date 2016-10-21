# C Interoperability

Orange links against `libc` by default, and allows for calling functions defined inside `libc`.

If a function is marked as `external`, its body can be omitted. Orange will assume it's defined in a linked library and allow usage.

External functions must not be generic.

```
extern def printf(str: const char*, ...)

printf("Hello, %s!\n", "world")
```
