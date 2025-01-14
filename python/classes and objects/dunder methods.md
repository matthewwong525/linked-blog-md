Dunder methods (also called magic methods) are the methods starting and ending with double underscores ‘’`__`". Dunder here means “Double Under (Underscores)”.

These methods are defined by built-in classes and commonly used for operator overloading.

#TODO see https://realpython.com/python-magic-methods/ and

> [!tip]
> The `dir()` function can show you magic methods inherited by a class:
>
> ```
> >>> dir(int)
> ```
>
> ```output
> ['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '_...
> ```

- **Initialization and Construction**
    - `__new__`: To get called in an object’s instantiation.
    - `__init__`: To get called by the `__new__` method.
    - `__del__`: It is the destructor.
- **Numeric Magic Methods**
    - `__trunc__(self)`: Implements behavior for `math.trunc()`.
    - `__ceil__(self)`: Implements behavior for `math.ceil()`.
    - `__floor__(self)`: Implements behavior for `math.floor()`.
    - `__round__(self, n)`: Implements behavior for the built-in `round()`.
    - `__invert__(self)`: Implements behavior for inversion using the `~` operator.
    - `__abs__(self)`: Implements behavior for the built-in `abs()`.
    - `__neg__(self)`: Implements behavior for negation.
    - `__pos__(self)`: Implements behavior for unary positive.
- **Arithmetic Operators**
    - `__add__(self, other)`: Implements behavior for the `+` operator (addition).
    - `__sub__(self, other)`: Implements behavior for the `-` operator (subtraction).
    - `__mul__(self, other)`: Implements behavior for the `*` operator (multiplication).
    - `__floordiv__(self, other)`: Implements behavior for the `//` operator (floor division).
    - `__truediv__(self, other)`: Implements behavior for the `/` operator (true division).
    - `__mod__(self, other)`: Implements behavior for the `%` operator (modulus).
    - `__divmod__(self, other)`: Implements behavior for the `divmod()` function.
    - `__pow__(self, other)`: Implements behavior for the `**` operator (exponentiation).
    - `__lshift__(self, other)`: Implements behavior for the `<<` operator (left bitwise shift).
    - `__rshift__(self, other)`: Implements behavior for the `>>` operator (right bitwise shift).
    - `__and__(self, other)`: Implements behavior for the `&` operator (bitwise and).
    - `__or__(self, other)`: Implements behavior for the `|` operator (bitwise or).
    - `__xor__(self, other)`: Implements behavior for the `^` operator (bitwise xor).
    - `__invert__(self)`: Implements behavior for bitwise NOT using the `~` operator.
    - `__neg__(self)`: Implements behavior for negation using the `-` operator.
    - `__pos__(self)`: Implements behavior for unary positive using the `+` operator.
- **String Magic Methods**
    - `__str__(self)`: Defines behavior for when `str()` is called on an instance of your class.
    - `__repr__(self)`: To get called by the built-in `repr()` method to return a machine-readable representation of a type.
    - `__unicode__(self)`: This method returns a Unicode string of a type.
    - `__format__(self, formatstr)`: Returns a new style of string.
    - `__hash__(self)`: Returns an integer for quick key comparison in dictionaries.
    - `__nonzero__(self)`: Defines behavior for when `bool()` is called on an instance of your class.
    - `__dir__(self)`: Returns a list of attributes of a class.
    - `__sizeof__(self)`: Returns the size of the object.
- **Comparison Magic Methods**
    - `__eq__(self, other)`: Defines behavior for the equality operator, `==`.
    - `__ne__(self, other)`: Defines behavior for the inequality operator, `!=`.
    - `__lt__(self, other)`: Defines behavior for the less-than operator, `<`.
    - `__gt__(self, other)`: Defines behavior for the greater-than operator, `>`.
    - `__le__(self, other)`: Defines behavior for the less-than-or-equal-to operator, `<=`.
    - `__ge__(self, other)`: Defines behavior for the greater-than-or-equal-to operator, `>=`.