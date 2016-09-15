# Mathematical Operations

You can do basic mathematical operations like `+`, `-`, `*`, and `/` on two values of the same type, provided those two values implement `Number`.

`Number` is an interface that provides the addition, subtraction, and multiplication operations. Division is reserved for the `Fractional` interface.

The `Number` and `Fractional` interfaces look something like this:

	interface Number {
		def operator+(LHS: Number, RHS: Number)
		def operator-(LHS: Number, RHS: Number)
		def operator*(LHS: Number, RHS: Number)
	}

	interface Fractional : Number {
		def operator/(LHS: Fractional, RHS: Fractional)
	}
