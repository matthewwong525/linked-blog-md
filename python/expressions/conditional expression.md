The conditional expression is Python's “ternary operator” `? :`.

```python
exprIfTrue if condition else exprIfFalse
```

1. The expression first evaluates the *condition* (not `exprIfTrue`).
2. If the condition is true, *exprIfTrue* is evaluated and its value is returned.
3. Otherwise, *exprIfFalse* is evaluated and its value is returned.

> [!note|no-title]
> This is different from the [[conditionals#if|if]] [[python/glossary/glossary#statement|statement]] because it is **not** a control structure that directs the flow of execution. <mark class="grey">It is more like an operator that defines an expression depending on the condition, hence the name "conditional expression"</mark>. It can be used within an expression (i.e. it can be evaluated) – in contrast to `if` and `if`-`else`, which are just statements and not expressions.

The conditional expression is commonly used to select variable assignment:

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===

```python
m = a if a > b else b
```
is equivalent to:
`````

`````col-md
flexGrow=1
===

```python
if a > b:
	m = a
else:
	m = b
```

`````
``````

> [!danger] The conditional expression has the <u>lowest priority</u> of all Python operations.
> This means that conditional expressions need to be surrounded by parentheses when used with other any other expressions/operators.

For example, the `+` operator binds more tightly than the conditional expression, so `1 + x` and `y + 2` are evaluated first, followed by the conditional expression:

```python hlt:'1 + x' impt:'y + 2' infot:'x > y'
z = 1 + x if x > y else y + 2
```

instead of this desired behaviour:

```python hlt:'z = 1 + x' infot:'y + 2' info1t:'x > y'
z = 1 + x if x > y else y + 2
```

To fix this, add parenthesis:

```python
z = (1 + x) if x > y else (y + 2)
```

## conditional expression in nested if else
We can nest the conditional expression to evaluate multiple conditions in a single line:

```python
res = "Positive" if n > 0 else "Negative" if n < 0 else "Zero"
```

```python
s = ('foo' if (x == 1) else
     'bar' if (x == 2) else
     'baz' if (x == 3) else
     'qux' if (x == 4) else
     'quux')
```

## conditional expression using tuple
The conditional expression can also be written by using [[data types#Tuple `(,)`|tuples]]: 

```syntax
(on_false, on_true)[condition]
```

```python
n = 7
res = ("Odd", "Even")[n % 2 == 0]
# res = "Odd"
```