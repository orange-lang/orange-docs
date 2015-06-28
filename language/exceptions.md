# Exceptions 
**STATUS**: Design Phase 

Orange has exception support, but has a dependency on the standard library.

However, on the core level, exceptions can be used like this:

    try 
        [[ _code_ ]]
    catch [[ _exceptionVar_ ]]
        [[ _code_ ]]
    end

You can also have a `finally` block:

    try 
        [[ _code_ ]]
    catch [[ _exceptionVar_ ]]
        [[ _code_ ]]
    finally 
        [[ _code_ ]]
    end

`finally` blocks will execute after the `try` and `catch` block, regardless of whether or not an exception is thrown. 

You can throw an exception simply as well:

`throw _your exception_`