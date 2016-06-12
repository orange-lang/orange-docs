# Control Flow

Orange provides control blocks that can optionally execute code if a condition is met and be values. These control blocks are `if`, `for`, `foreach`, `while`, `forever`, `switch`, and `do ... while`.

## if

	statement -> block
	block     -> "{" (statement | expression)* "}"
	block     -> ":" (statement | expression)

	if         -> "if" "(" expression ")" (elif | else)? block
	elif       -> "elif" "(" expression ")" (elif | else)? block
	else       -> "else" block

	expression -> if

`if` is the most basic control block. It has a condition, and if it is met, the code for that block is executed once.

    if (condition) {
        // code
    }

Orange also supports `elif` blocks, which can be used following an if block to try more conditions if the first condition didn't meet.

    if (condition) {
        // code
    } elif (anotherCondition) {
        // different code
    }

Any number of `elif` blocks can be used following an if block. Finally, an `else` block can be placed after the if and list of elifs to execute code without a condition check:

    if (condition) {
        // code
    } elif (anotherCondition) {
        // different code
    } elif (finalCondition) {
        // more code
    } else {
        // fallback code
    }

It is important to note that if any of the conditions meet, after the code in the block executes, no other condition will be checked. The `else` block is only executed if absolutely none of the conditions were met. If you wish to check for two conditions and execute the same block, that can be done using the boolean operation `||`.

Note that blocks normally begin with `{` and end with `}`, but Orange allows replacing the `{` with a semicolon for a one-line block:

	var a = 5;
	if (condition): a += 8;

This single-expression block can be used anywhere a block is allowed, including functions.

## for

	for_loop  -> "for" "(" exprression ";" expression ";" expression
	             ")" block

	expression -> for_loop

For loops can be used to run code continously until a condition is met.

    for (initializer; condition; afterthought) {
        // loop body
    }

The `initializer` of the loop is always ran only once before the loop begins. Afterwards, the condition is checked. If the condition resolves to `true`, the loop body is executed. Then, the `afterthought` is ran. After the afterthought is executed, we loop back to the condition check and start all over.

An example of looping through all numbers 1 to 10 to sum them is as follows:

    int sum = 0;
    for (int i = 1; i <= 10; i++): sum += i;

## foreach

	foreach    -> "foreach" "(" var_decl "in" expression ")" block
	expression -> foreach

`foreach` can be used to iterate over an object that implements `Iterable` or for an object that an iterator can be created for. See [Interfaces](interfaces.md) for more details.

    int sum = 0;
    foreach (var i in [1 ... 10]) {
        sum += i;
    }

In this example, `[1 ... 10]` is a plain array, so an iterator is created for it. The behavior where certain objects can have iterators built from them is built-in to the compiler and can't be replicated in code.

Unlike arrays, tuples cannot be iterated over, as each element can have a different type.

## while

	while      -> "while" "(" expression ")" block
	expression -> while

A while loop is a simplified for loop that doesn't have the `initializer` or `afterthought`:

    while (condition) {
        // block
    }

## forever

	forever    -> "forever" block
	expression -> forever

A forever loop is the simplest loop that has no condition and after executing the block, will loop back to the beginning infinitely until broken.

    forever {
        // block
    }

## do while

	do_while   -> "do" block "while" "(" expression ")"
	expression -> do_while

Do while is like a while loop where the code block is executed before the condition is checked. After the block is executed, if the condition fails, the loop will no longer continue.

    do {
        // code block
    } while (condition);

## Loop control

	break_stmt    -> "break"
	continue_stmt -> "continue"
	statement     -> break_stmt term | continue_stmt term

Loops can have their blocks controlled by using `continue` or `break` statements (which can have values, see Blocks as values for more details). A continue statement will continue to the next iteration. `continue` will skip to the afterthought, if one exists. If an afterthought doesn't exist, it'll skip to the condition, if one exists for that loop. If a condition doesn't exist, it will skip to the top of the body of the loop. `break` will always exit the loop, and executes neither `afterthought` nor `condition`.

## switch

	switch         -> "switch" "(" expression ")" switch_block
	switch_block   -> "{" switch_match ("," switch_match)* "}"
    switch_match   -> switch_pattern "," switch_pattern "=>" switch_value
    switch_value   -> expression | "{" ( statement | expression )* "}"
    switch_pattern -> ("_" | expression )

	expression     -> switch

`switch` is similar to using `if` and `elif`, but allows for more power, since it does pattern matching.

The syntax is as follows:

    switch expression {
        pattern => statement,
        pattern => statement,
        ...
        _: statement
    }

In a switch statement, you can have as many patterns as you wish, and `_` can be omitted. If `_` is present, it'll match for any pattern that wasn't already matched. A pattern can be matched against constants:

    var x = 0;
    switch x {
       0 => "zero",
       1 => "one",
       _ => "neither zero nor one"
    }

In this case, the result is `"zero"`.

A pattern can also be matched against a decoupled tuple:

    switch ("dog", 2016) {
       ("dog", 2015) => "2015 dogs is a lot of dogs",
       ("cat", 1994) => "1994 cats is less than 2015 dogs",
       ("bird", number) => "we have a bird and some number",
       (animal, _) => animal
    }

In this example, we excluded `_` from the switch list, since that last pattern, `(animal, _)` will bind to any value. Any variable declared in the pattern of a switch statement will shadow existing variables with that same name.

Multiple patterns can be used with commas:

    var x = 0;
    switch x {
        0, 1 =. "zero or one",
        _ => "neither zero nor one"
    }

The statement for a pattern in a switch statement can be a block of code, if so desired.

    pattern => {
        // lots of code
    }

Enums can also be used for pattern matching. See Enumerations for more details.

## Blocks as values

	yield_stmt -> "yield" expression
	statement  -> yield_stmt term

Any control block can be used as a value, if it would produce a value in all scenarios. For example, an if block can be used as a value if it has an else, and all if blocks `yield` some value.

    var a = if (5 > 10) {
        yield 0;
    } else {
        yield 1;
    };

Yield has a shorthand for easier use: if the last statement in a block does not have a semicolon, that will be used as the yield value. Using this, the previous example can be rewritten as follows: `var a = if (5 > 10) { 0 } else { 1 };`

Loops that use `continue` and `break` can be used as values only if each continue and break statement has a yield-value (e.g., `break 5` or `continue myVar`). If the main block of the loop does not have a terminating statement (i.e., `continue`, `break`), it will need a `yield` statement to be properly used as a value.

If a block is used as a value, all of yield statements (including continue and break) must have the same data type.
