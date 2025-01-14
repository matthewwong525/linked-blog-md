In order to run Python apps, you need a runtime environment/interpreter to execute the code. 

The Python interpreter installed on your machine can execute Python code in 2 modes:

1. **Script mode**: In script mode, you put a set of Python statements into a text file with a `.py` extension. You then run the python interpreter and point it at the file. The program is executed line by line, and the output is displayed.
2. **Interactive mode**: In this mode, each command you type is interpreted and executed immediately on Enter. 
## script mode
In the script mode, the python program is written in a file  (`.py`). The python interpreter reads the file and then executes it. 

To run a python file (`.py`) as a program/script:

1. Pass the module **file name** to `python3` interpreter as a command-line argument:

```shell
python3 file.py
```

2. Pass the **code** to `python3` interpreter with the [`-c`](https://docs.python.org/3/using/cmdline.html#cmdoption-c) option: 

```shell
python3 -c 'print("Hello, world")'
```

3. Begin the `.py` file with a hashbang line (`#!`) and make the file executable by setting the execute bit with `chmod`.  This lets you run python scripts directly from the command-line without explicitly calling `python` first:

> [!col]
> 
> ```python file=example.py
> #! /usr/bin/env python3 
> ```
> 
> ```shell
> chmod 755 example.py
> ./example.py
> ```
## interactive mode (REPL)
- To invoke the REPL, type `python3` in the terminal
- To quit the REPL, type `exit()` or press `Ctrl+D` 

To run the Python interpreter interactively, type `python3` (the python version) in the terminal:

```shell
python3
```

This will enter interactive mode and open a [[python/glossary/glossary#REPL|REPL]] session where you can **run python code line by line** (after the primary prompt `>>>`):

```hlt:3
Python 3.9.6 (default, Oct 18 2022, 12:41:40) 
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

- `>>>` (primary prompt) indicates that the interpreter is waiting for you to type a command.
- `...` (secondary prompt) is where you type for continuation lines.

For example:

```python
>>> number = -42

>>> if number < 0:
...     print("negative")
... elif number > 0:
...     print("positive")
... else:
...     print("equal to 0")
...
negative
```

To exit interactive mode, you can either type `exit()` or press `Ctrl+D` (on UNIX, macOS systems) or `Ctrl+Z` (in Windows). 
## command line option: `-i`
Instead of Python exiting when the program is finished, you can use the `-i` flag to start an interactive session. This can be **very** useful for debugging and prototyping.

Execute a Python script and then enter interactive mode by passing the `-i` option:

```shell
python3 -i file.py
```

This preserves the script's context — all variables, functions and import can be accessed in the REPL.

We can inspect, function calls, and debug the code in `file.py` as needed:

```python
>>> globals()
{
    '__name__': '__main__',
    ...
    'read_data': <function read_data at 0x104dd4860>,
    'sample': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    'mean': <function mean at 0x104fe3ec0>,
    'average': 5.5
}

>>> mean([2, 3, 3, 2])   
2.5

>>> mean([])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File ".../sample.py", line 10, in mean
    return sum(data) / len(data)
           ~~~~~~~~~~^~~~~~~~~~~
ZeroDivisionError: division by zero
```

The build-in [globals()](https://docs.python.org/3/library/functions.html#globals) function returns a dictionary of all the global names defined in your script.