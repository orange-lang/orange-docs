# Error Handling

	try_block     -> "try" block catch_block+ finally_block?
	catch_block   -> "catch" "(" var_decl ")" block
	finally_block -> "finally" block
	throw_stmt    -> "throw" expression ";"

	statement     -> try_block | catch_block | finally_block | throw_stmt

Orange offers exception support to implement error handling. An object of any type (including plain data types such as `int` or `float`) may be thrown as an exception.

To throw an exception, use the throw syntax: `throw expression;`

To catch an exception, the exception to catch must be in a `try` block:

    try {
       // code which may throw an exception
    } catch (exceptionType ex) {
       // use exception to print an error
    } finally {
	   // code that runs after the try or catch
	}

A try block may be paired with as many `catch` blocks as desired, with each catch block catching an exception of a different type. If a catch block catches an exception of a parent class before an exception of a child class, the parent class block will be executed. If a child class block is placed before the parent, the child class catch block will be executed if the exception is an instance of a child.

Finally blocks are optional blocks that are executed regardless of whether or not an exception is thrown. It executes after the try or catch block exits.
