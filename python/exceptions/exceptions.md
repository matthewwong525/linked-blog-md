## Exceptions
Exceptions are errors that occur during the execution of a program, disrupting the normal flow of the program.
## Exceptions and Syntax Errors
Syntax errors occurs when the parser detects an incorrect statement. The arrow indicates where the parser ran into the **syntax error**.

```python
>>> print(0 / 0))
  File "<stdin>", line 1
    print(0 / 0))
                ^
SyntaxError: unmatched ')'
```

**Exception errors** occur whenever syntactically correct Python code results in an error.

```python
>>> print(0 / 0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
```

## Raising an Exception
Python comes with [various built-in exceptions](https://docs.python.org/3/library/exceptions.html) as well as the possibility to create user-defined exceptions.

You raise an exception in Python using the `raise` keyword followed by an exception object, which can include a custom message.

```python file=low.py hlt:3
number = 10
if number > 5:
    raise Exception(f"The number should not exceed 5. ({number=})")
print(number)
```

Here, we raised an `Exception` object and passed it a custom message build using an [[data types#f-strings| f-string]] and [[data types#self-documented expressions|self-documenting expression]].

When you run `low.py`, you’ll get the following output:

```
Traceback (most recent call last):
  File "./low.py", line 3, in <module>
    raise Exception(f"The number should not exceed 5. ({number=})")
Exception: The number should not exceed 5. (number=10)
```