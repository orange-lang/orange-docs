# Preprocessor Conditionals

Orange allow sfor a very limited set of preprocessor conditions that compile the code block if a certain preprocessor variable exists. 

Note that unlike the C-family preprocessors, all branches will be checked for synantical errors, but type checking won't happen. 

A preprocessor conditional works like a standard if statement, but is prefixed with `const`. 

```
const if (MacOS) {
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
