# Preprocessor Macros
**STATUS**: Not Implemented

There is two planned preprocessor macros for Orange: `@ifdef __CONSTANT__` and `@endif`. 

`@ifdef __CONSTANT__` is used to conditionally compile code. For example:

    @ifdef Windows
        # you're on windows
    @endif 

    @ifdef Mac
        # you're on mac
    @endif 

However, it should be noted that since the standard library is intended to be cross-platform, there is no real use for preprocessor macros outside from low-level development.
