---
cssclasses:
  - codewrapOff
---
> [!summary]
> - [`help()`](https://docs.python.org/3/library/functions.html#help) looks up the documentation for modules, functions, objects and methods.
> - [`dir()`](https://docs.python.org/3/library/functions.html#dir) returns the list of attributes (including methods) for the object argument.
## help()
The built-in `help()` function lets you gives you access to Python’s **built-in help system**:

```
help([object])
```

Where `[object]` is a specific function or keyword you want help on.

You can call this function in 2 ways:

1. `help()` with **no arguments** enters Python's help system (*interactive help mode*)
2. `help(object)` with **an object or string** gives you access to the object's help page

The help page of an object typically contains information from the object’s [[documentation string ("docstring")|docstrings]].
It may also include a list of methods and attributes.
## dir()
The built-in `dir()` function returns a list of valid attributes for that object.
This includes the method names available for the object (with no description unlike help).

```
>>> dir(str)
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'removeprefix', 'removesuffix', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```

