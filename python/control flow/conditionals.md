## if

```python
if condition1:
	# Executes this block if condition1 is true
elif condition2:
	# Executes this block if condition1 is false
else:
	# Executes this block if condition2 is false
```

- Parentheses are not required (optional) around the `if` condition
- Indentation defines the scope of each statement (C uses `{` `}`)

If you have only one statement to execute,  you can put it all on the same line:

```python
if <expr>: <statement_1>; 
```

```python file="one-line if statement"
if a > b: print("a is greater than b")
```

You can also have multiple else statements on the same line, separated by semicolons:

```python
if <expr>: <statement_1>; <statement_2>; ...; <statement_n>
```

There are 2 possible paths:
1. If `<expr>` is true, execute all of `<statement_1> ... <statement_n>`.
2. Otherwise, don’t execute any of them.

The semicolon binds the statements tightly as a suite, so it is pretty much treated like:

```python
if <expr>: 
	<statement_1>; 
	<statement_2>; 
	...; 
	<statement_n>
```
## match / case
The match / case in python is similar to switch / case in C.

A `match` statement takes an expression and compares its value to each `case` block.
Only the first pattern that matches gets executed.

```python
match status:
	case 400:
		return "Bad request"
	case 404:
		return "Not found"
	case 418:
		return "I'm a teapot"
	case _:
		return "Something's wrong with the internet"
```

> [!alert|no-title]
> *Note the last block*: the [[variables assignment#throwaway variable `_`|throwaway variable _]] acts as a *wildcard_ and never fails to match. If no cases matches, it is caught by this block.

You can combine several literals in a single pattern using `|` (“or”):

```python
case 401 | 403 | 404:
    return "Not allowed"
```