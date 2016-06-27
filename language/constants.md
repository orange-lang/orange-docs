# Constants

Orange has four types of constants: floating-point, integral, strings, and chars.

	value      -> ( "0" ... "9" | "A" ... "F" )+
	expression -> integral_const | float_const | string_const

	integral_const -> iprefix? value isuffix?
	iprefix        -> "0b" | "0o" | "0x"
	isuffix        -> "i" | "u" | "i8" | "i16" | "i32" | "i64"
	isuffix        -> "u8" | "u16" | "u32" | "u64"

	float_const -> value ( "." value )? fsuffix?
	fsuffix     -> "f" | "d"

	string_const -> "\"" string_content "\""
	char_const -> "'" character "'"

When writing an integral const, the prefixes `0b`, `0o`, and `0x` refer to a binary, octal, and hexadecimal constant respectively. If the prefix is omitted, the constant defaults to a decimal. Note that when specifying binary, octal, or hexadecimal, you can only use numbers valid for that base for the value.

The integral suffix determine the size and sign of the constant:

- `i`: signed integer
- `u`: unsigned integer
- `i8`: 8-bit signed integer
- `u8`: 8-bit unsigned integer
- `i16`: 16-bit signed integer
- `u16`: 16-bit unsigned integer
- `i32`: 32-bit signed integer
- `u32`: 32-bit unsigned integer
- `i64`: 64-bit signed integer
- `u64`: 64-bit unsigned integer

The size of `i` and `u` is either 32- or 64-bits depending on the system you're compiling on. If the suffix is ommited, `i` is inferred.

Floating-point constants are simpler; they don't support prefixes and only have two suffixes:

- `f`: floating-point number
- `d`: double-precision floating-point number

Each of the suffixes from both integral and floating-point constants correspond to a data type in Orange:

- `i`: `int`
- `u`: `uint`
- `i8`: `int8`
- `u8`: `uint8`
- `i16`: `int16`
- `u16`: `uint16`
- `i32`: `int32`
- `u32`: `uint32`
- `i64`: `int64`
- `u64`: `uint64`
- `f`: `float`
- `d`: `double`

Strings and chars can neither be prefixed nor suffixed. They must begin and end with double quotes, but double qoutes can be contained inside the string if they are escaped using a `\`.
