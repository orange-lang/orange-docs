# Constants

A constant can be one of the following general types:

- Number (e.g., `5`, `-910`, etc.)
- Fractional (e.g., `12.91`, `-3.4`, etc.)
- Bool (`true`, `false`)
- Char (`a`, `F`, unicode chars, etc.)

`Number` and `Fractional` have a lot of subtypes that a constant may resolve to, based on usage.

Number can resolve to any of the following: `Int`, `UInt`, `Int8`, `UInt8`, `Int16`, `UInt16`, `Int32`, `UInt32`, `Int64`, `UInt64`. It defaults to `Int` if a more specific type can't be determined.

Fractional can resolve to `Float`, `Double`, or `Float128`. It defaults to `Double` if a more specific type can't be determined.

Note that `Fractional` is technically a subtype of `Number`; any operation defined for `Number` also works for `Fractional`.
