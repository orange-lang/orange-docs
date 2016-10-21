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
