# Operator Precedence

This file outlines the precedence of the various operators in descending order.

	Precedence 1 (Left-to-right precedence):
		- Access operator  (.)
	Precedence 2 (Left-to-right precedence):
		- Post-increment   (a++)
		- Post-decrement   (a--)
		- Function call    (a())
		- Subscript        (a[])
	Precedence 3 (Right-to-left precedence):
		- Pre-increment    (++a)
		- Pre-decrement    (--a)
		- Negation         (-a)
		- Logical NOT      (!a)
		- Bitwise NOT      (~a)
		- Casts            ((type)a)
		- Dereference      (*a)
		- Reference        (&a)
		- new              (new)
		- delete           (delete)
	Precedence 4 (Left-to-right precedence):
		- Multiplication   (a*b)
		- Division         (a/b)
		- Remainder        (a%b)
	Precedence 5 (Left-to-right precedence):
		- Addition         (a+b)
		- Subtraction      (a-b)
	Precedence 6 (Left-to-right precedence):
		- Bitshift left    (<<)
		- Bitshift right   (>>)
	Precedence 7 (Left-to-right precedence):
		- Less than        (<)
		- Greater than     (>)
		- Less or equal    (<=)
		- Greater or equal (>=)
	Precedence 8 (Left-to-right precedence):
		- Equals           (==)
		- Not equals       (!=)
	Precedence 9 (Left-to-right predence):
		- Bitwise AND      (a&b)
	Precedence 10 (Left-to-right precedence):
		- Bitwise XOR      (a^b)
	Precedence 11 (Left-to-right precedence):
		- Bitwise OR       (a|b)
	Precedence 12 (Left-to-right precedence):
		- Logical AND      (a&&b)
	Precedence 13 (Left-to-right precedence):
		- Logical OR       (a||b)
	Precedence 14 (Right-to-left precedence):
		- Ternary operator (a?b:c)
		- Assignment       (=)
		- Plus assign      (+=)
		- Minus assign     (-=)
		- Times assign     (*=)
		- Divide assign    (/=)
		- Remainder assign (%=)
		- BshiftL assign   (<<=)
		- BshiftR assign   (>>=)
		- Bit AND assign   (&=)
		- Bit OR assign    (|=)
		- Bit XOR assign   (^=)
	Precedence 15 (Left-to-right precedence):
		- Comma            (,)
