# Rules

This is a strict collection of all rules for a well-typed program. Rules are structed with a letter sequence indicating the type of error and a number representing the error code. Error codes are globally unique across all error categories as to make searching for issues easier. This means that there would be no `R1000` and `E1000`, since the error codes are the same, despite the categories being different.

Categories:

- `ID`: Identifiers
- `C`: Constants
- `V`: Variables
- `A`: Arrays
- `T`: Tuples
- `CF`: Control Flow
- `FC`: Function Calls
- `FD`: Function Declarations
- `E`: Enumerators
- `S`: Switch
- `I`: Interfaces
- `TA`: Type Aliases
- `CL`: Classes
- `NS`: Namespaces and Packages
- `P`: Privacy
- `EX`: Exceptions
- `G`: Generics

LATEST ID: 0032

## ID: Identifiers

- Code: ID0001
- Message: Cannot find identifier (name)

## C: Constants

- Code: C0002
- Message: Invalid signed suffix (suffix) for implicitly unsigned constant (value)
- Explanation:
	Signed suffixes, like i, i32, etc., can't be used for implicitly unsigned constants, like binary, octal, hex.

## V: Variables

- Code: V0003
- Message: Variable may not be of type void

- Code: V0004
- Message: Variable's value may not be of type void.

- Code: V0005
- Message: Variable's initial value does not match variable's declared type.

## A: Arrays

- Code: A0006
- Message: Array cannot store void values.

- Code: A0007
- Message: Array must contain values of all the same types.

## T: Tuples

- Code: T0008
- Message: Tuple cannot store void values.

## CF: Control Flow

- Code: CF0009
- Message: Block used as value must yield value in all exit points.

- Code: CF0010
- Message: Block used as value must yield the same type in all exit points.

- Code: CF0011
- Message: Block can not yield void value.

## FC: Function Call

- Code: FC0012
- Message: Cannot find a function (name) that matches the arguments (type list).

- Code: FC0013
- Message: Cannot pass void value as argument to function.

## FD: Function Declaration

- Code: FD0014
- Message: Function with matching type signature already exists.

## E: Enumerators

- Code: E0015
- Message: Enumerator value (value) already exists.

## S: Switch

TBD

## I: Interfaces

- Code: I0016
- Message: Interface method may not have body.

## TA: Type Aliases

- Code: TA0017
- Message: Type does not exist.

- Code: TA0018
- Message: Alias already exists.

## CL: Classes

- Code: CL0019
- Message: Class named (name) already exists.

- Code: CL0020
- Message: Class inheriting from (parent) with non-default constructor must explicitly declare a constructor.

- Code: CL0021
- Message: Class constructor must call a parent constructor from non-default constructed parent class.

- Code: CL0022
- Message: Class may not have more than one destructor.

- Code: CL0023
- Message: Variable named (name) already exists in class.

- Code: CL0024
- Message: Method with matching type signature already exists.

## NS

TBD

## P: Privacy

- Code: P0025
- Message: Cannot access (privacy level) class member (name)

- Code: P0026
- Message: Cannot access (privacy level) class method (name)

- Code: P0027
- Message: Cannot access (privacy level) class constructor (name)

- Code: P0028
- Message: Cannot access (privacy level) class destructor (name)

- Code: P0029
- Message: Cannot access (privacy level) function (name)

- Code: P0030
- Message: Cannot make (name) (privacy level)

## EX: Exceptions

- Code: EX0031
- Message: Try block with no catch

- Code: EX0032
- Message: Cannot throw void value

## G: Generics

TBD
