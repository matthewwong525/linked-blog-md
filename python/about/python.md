## Language Introduction
Python is an [[python/glossary/glossary#interpreted|interpreted]], object-oriented, high-level language which is both strongly typed and [[python/glossary/glossary#dynamically typed|dynamically typed]].

> Python has a strong, dynamic, duck-type system.

**Dynamically typed**: Variables are assigned a type at runtime during execution. There are no type declarations of variables, parameters, functions, or methods in source code.

```python
a = 6      #  `a` holds an integer
a = 'hi'   #  `a` can also hold a string
```

**Strongly-typed**: The interpreter enforces strict rules about how types are used. For example, adding a string to an integer without explicit conversion will raise a runtime error. 

```python
x = "Hello"
y = 5
print(x + y)  # Raises TypeError at runtime
```

**Duck typing**: Recall that we don't have to declare the types of arguments in function declarations. This is because Python has a duck-typing system. Whether or not an object is suitable as an input to a function only depends on what is requested of that object in that function, regardless of what type the object is. An object is compatible with a specified type if it has all the methods and properties the type requires. This allows us to create functions where the parameter doesn't have a specific type. As long as the object passed has the methods called in the function body, it works. 

```python
def quack(duck):
	# As long as the object has a 'quack' method, it works
	duck.quack()
```

Duck-typing avoids the need for type checks using [`type()`](https://docs.python.org/3/library/functions.html#type) or [`isinstance()`](https://docs.python.org/3/library/functions.html#isinstance). 
## Python Documentation
The official Python documentation can be found here: [docs.python.org](http://docs.python.org/).

However,  the REPL has a built-in `help()`  function you can use to look up keywords and functions:

```
help([object])
```

Where `[object]` is a specific function or keyword you want help on.

You can access the inbuilt documentation by calling the built-in `dir()` functions.

- [`help()`](https://docs.python.org/3/library/functions.html#help) looks up the documentation for modules, functions, objects and methods. 
- [`dir()`](https://docs.python.org/3/library/functions.html#dir) returns the list of attributes (including methods) for the object argument. 

> [!note|no-title]
> **Note:** You can also start interactive help by calling `help()` with no arguments.
