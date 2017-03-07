# Conditionals

Orange allows using `if` statements to conditionally execute code. Additionally, a list of `elif` statements (`else if`) can be chained immediately following the `if` statement for extra conditionals if the first check fails. Afterwards, an `else` statement can be used at the end to execute if everything else fails.

```
if (yourAge == 20) {
	Console.Print("Almost there!")
} elif (yourAge < 21) {
	Console.Print("You can't drink yet!")
} else {
	Console.Print("Drink up!")
}
```

Like functions, conditionals support short blocks:

```
if (yourAge == 20): Console.Print("Almost there!")
elif (yourAge < 21): Console.Print("You can't drink yet!")
else: Console.Print("Drink up!")
```

And since conditionals support short blocks, they can also be used as values. Note that if a conditional is being used as a value, there must be an else statement to catch all the remaining cases for the values, and all of the conditional blocks (if/elifs/else) must yield the same value.

```
var beerRequestResponse = if   (yourAge == 20): "Almost there!"
                          elif (yourAge < 21): "You can't drink yet!"
                          else: "Drink up!"

Console.Log(beerRequestResponse)
```

Note that the formatting applied in that example was just to make the code more readable. It could also have been written with yield statements in long blocks:

```
var beerRequestResponse = if (yourAge == 20) {
	yield "Almost there!"
} elif (yourAge < 21) {
	yield "You can't drink yet!"
} else {
	yield "Drink up!"
}

Console.Log(beerRequestResponse)
```

## Conditions with Initializers

Like C++17 and Go, Orange supports having a statement as the "first part" to an if block. The general form to a condition can be either `booleanCondition` or `statement; booleanCondition`.

For example:

```
if (var yourAge = getAge(); yourAge == 20) {
	yield "Almost there!"
} elif (yourAge < 21) {
	yield "You can't drink yet!"
} else {
	yield "Drink up!"
}
```

The statements used in the condition part of the if blocks share scope with _all_ of the if blocks, including `elif` and `else`, so you can't redeclare the variable in an `elif` block (but you _can_ reassign to it).  
