# Exceptions

Exceptions are an extension that allow for delivering an error message that is delivered up the call stack until it is accepted by a block or caught by the standard library.

The delivering of an error is calling _throwing_, and Orange allows to throw anything up the stack, including integers. (For example, `throw 5`).

Any block in Orange may wrap code in a `try`, `catch`, and `finally`. Anything wrapping in a try will receive a thrown error and try to match it against one of the `catch` blocks. If none of them match, it continues up the call stack.

A catch block catches an exception of a specific type. A try/catch with multiple catch blocks might look like this:

```
try {
	// do something
} catch (e: int) {
	// caught int exception
} catch (e: float) {
	// caught float exception
}
```

A finally block can be appended to the try/catch sequence to execute after the try/catch completes. It'll always exceute whether an exception was caught or not.

```
try {
	// stuff
} catch (e: int) {
	// caught
} finally {
	// cleanup stuff 
}
```
