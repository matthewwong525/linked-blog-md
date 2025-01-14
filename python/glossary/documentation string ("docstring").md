- [PEP 257 docstring conventions](https://peps.python.org/pep-0257/#one-line-docstrings)
## What is a Docstring?
Docstrings are the string literals that appear right after the function definition.
We can access these docstrings using the `__doc__` attribute.

```python
def square(n):
    '''Take a number n and return the square of n.'''
    return n ** 2

print(square.__doc__)
```

```output
Take a number n and return the square of n.
```
## Single-line Docstrings
- Single-lined docstrings should still be enclosed in triple quotes.
- The first line should begin with a capital letter and end with a period.
- The first line should summarise the function's behaviour/purpose.
- ! For one liner docstrings,  keep the closing `"""` on the same line:

```python
def avg(*args):
    """Returns the average of a list of numeric values."""
    return sum(args) / len(args)
```
## Multi-line Docstrings
Docstrings can be more than one line, to summarise a function's behaviour AND document its arguments and return values. It should also list all the exceptions that can be raised and other optional arguments.

> [!alert|no-title]
> The `"""` that ends a multiline docstring should be on a line by itself

```python
def add_binary(a, b):
    '''
    Return the sum of two decimal numbers in binary digits.

		Parameters:
				a (int): A decimal integer
				b (int): Another decimal integer

		Returns:
				binary_sum (str): Binary string of the sum of a and b
    '''
    binary_sum = bin(a+b)[2:]
    return binary_sum
```

```python
"""
This is an example of Google style.

Args:
    param1: This is the first param.
    param2: This is a second param.

Returns:
    This is a description of what is returned.

Raises:
    KeyError: Raises an exception.
"""
```
## Access Docstrings
We can access the docstrings for built-in functions such as `print()` like so:

```python
>>> print(print.__doc__)
```

We can also use the `help()` function to read the docstrings associated with various objects:

```python
>>> help(print)
```

Both methods return the same docstring (except help also gives other info like methods):

```output
print(*args, sep=' ', end='\n', file=None, flush=False)
    Prints the values to a stream, or to sys.stdout by default.

    sep
      string inserted between values, default a space.
    end
      string appended after the last value, default a newline.
    file
      a file-like object (stream); defaults to the current sys.stdout.
    flush
      whether to forcibly flush the stream.
```
