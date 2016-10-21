# Preprocessor Conditionals

Orange allows for a very limited set of preprocessor conditionals that check if a certain preprocessor variable exists. If it does, the code inside the conditional will be compiled.

A preprocessor conditional works like a standard if statement, but the `if` chain begins with #.

```
#if (MacOS) {
	// running MacOS
} elif (Windows) {
	// running Windows
} else {
	// running something else
}
```

The following preprocessor conditionals may be set:

- `MacOS`
- `Linux`
- `BSD`
- `Windows`
- `Debug`
- `Release`
