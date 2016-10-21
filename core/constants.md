# Constants

There are four basic type of constants in Orange: numbers, characters, booleans, and strings.

## Numeric Constants

A number can be written in decimal form with or without a decimal point, like `120` or `91.42`. The format is an integer constant, and the latter is a real number constant.

Integer constants can also be written in binary, octal, or hexadecimal format by prefixing the constant with `0b`, `0o` and `0x` respectively.

Numeric constants can have their type enforced by suffixes. For whole number constants, there are a set of suffixes for signed and unsigned integers.

- Signed suffixes: `i`, `i8`, `i16`, `i32`, `i64`
- Unsigned suffixes: `u`, `u8`, `u16`, `u32`, `u64`

For real numbers, a suffix of `f` or `d` can be used for floating point and double-floating point respectively.

Underscores after the optional prefix and first digit of any numeric constant are ignored and can be used at will for grouping numbers, like `0b1001_1000`, `1_500_423` or even `1_500_423.95`.

## Character Constants

A character constant is any ASCII single-byte character enclosed in single quotes.

### Escape Sequences

Special characters can be achieved by escaping a certain character with a backslash. These are valid for character constants and string constants. The valid special character sequences are:

- `\n`: Newline
- `\r`: Carriage return
- `\t`: Tab
- `\v`: Vertical tab
- `\'`: Single quote
- `\"`: Double quote
- `\\`: Backslash

## Boolean Constants

Boolean constants are the simplest, where only `false` and `true` are valid values.

## Strings

A string is like a character constant except that it allows for multiple characters and also allows for any UTF-8 sequence, including unicode characters. A string can be formed by enclosing a sequence of characters in double quotes.
