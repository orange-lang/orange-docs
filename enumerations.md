# Enumerations

	enum         -> "enum" identifier "{" enum_values "}"
	enum_values  -> enum_value? | enum_value ("," enum_value)*
	enum_value   -> identifier ( "(" param_list ")" )?
	enum_access  -> identifier "." identifier

	pattern      -> enum_pattern
	enum_pattern -> identifier "." identifier "(" arg_list ")"

In Orange, an enumeration is a list of named values which may contain values themselves.

    enum Status {
        Stopped,
        Running,
        Finished,
        Error
    }

This defines an enum named `Status` with four states: `Stopped`, `Running`, `Finished`, and `Error`. States of an enum are accessed using the `.` syntax: `Status.Stopped`, `Status.Running`, etc.

If we wanted to tie information to an enum value, we can do so:

    enum Status {
        Stopped,
        Running,
        Finished,
        Error(string err)
    }

A value can be conditionally checked to see if it is equal to any enum value (e.g., `a == Status.Error`). However, if that enum value contains data, it can only be decoupled and retrieved via a switch statement:

    switch myStatus {
        Status.Error(e) => println("we've got an error: {e}"),
        _ => println("we're good!")
    }

Note that the decoupled enum pattern's argument list creates variables with that name. If `e` already exists, it'll be shadowed in the scope of the match pattern's statement.
