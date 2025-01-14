## Print to the console
In Python, the `print` function outputs text on the screen, or another standard output device (`sys.stdout` or `sys.stderr`):

```python
print('Hello World!')
```

 By default, `print` outputs/appends **a newline character at the end of the line**, so that a subsequent call to `print` starts on the next line:
 
 ![|400](https://cs.stanford.edu/people/nick/py/img/python-print.png)

> [!code] Syntax
> ```
> print(*objects, sep=' ', end='\n', file=None, flush=False)
> ```
> 
> Prints *objects* to the text stream *file*, separated by *sep* and followed by *end*. 

Non-Keyword Arguments (`*objects`): 
- Accepts **any number of parameters** and prints them all out on **one line** of text. 
	- Pass multiple objects separated by commas `,` 
	- Each object is concatenated into a single string, separated by spaces, for output.
- By default, if any object is not a string, it will be converted to a string before printing.
- If no parameters are given, print() will just output _end_ = a *newline* `'\n'`.

```python
>>> print('hi', 'there', -2)  # print multiple objects
hi there -2

>>> print()  # print a newlinw

>>> 
```

Optional Keyword Arguments:
- `sep=`: <i>string</i> separator to use between object. Defaults to a single space `' '`.
- `end=`: <i>string</i> to print at the end of output. Defaults to a newline `'\n'`. 
	- By default, print will move to the next line after each call.
	- If you set `end=''`, print() will <i>not</i> move to the next line after printing.
- `file=`: <i>file</i> object to send the output to. Defaults to `sys.stdout`.
- `flush=`: <i>boolean</i> that specifies whether the output buffer should be flushed after printing. Defaults to `False`, meaning the output buffer will only be flushed when necessary (e.g. when the program terminates).
# Standard Input
There are 2 main ways to read data from `stdin`:
1. `input()`
2. `sys.stdin`
## Read user input 

The built-in [input()](https://docs.python.org/3/library/functions.html#input) reads a line from input and returns it as a string w/o the trailing newline. 

To read one line from the keyboard:
```
line = input()
```

You can also call the `input` function with a `prompt` string:
```
line = input('Enter a line: ')
```

These 2 programs are *almost* the same. The difference is that `print(prompt)` (by default) adds a newline to the output, whereas `input(prompt)` will write the prompt without a trailing newline:
> [!col]
> 
> > [!div]
> > 
> > ```python hl:2
> > print('Enter your name: ')
> > name = input()
> > print(name)
> > ```
> > 
> > ```
> > Enter your name: 
> > // enter input here
> > ```
> 
> > [!div]
> > ```python hl:1
> > name = input('Enter your name: ')
> > print(name)
> > ```
> > 
> > ```
> > Enter your name: // enter input here
> > ```
> 

## Write to a file
#TODO

