---
cssclasses:
  - pinkCode
  - greenLinks
---
## Objects, Types & Classes
Python is an object-orientated language
- Everything in Python is an *object*, with an associated *type*.
- It uses *classes* to define an object's *data type*.
- The built-in [`type()`](https://docs.python.org/3/library/functions.html#type) function returns an object's type.

An object's type = class
- The type of an object is which class the object derives (instantiates) from.
- A class defines the **data** (attributes) and **behaviour** (methods) available to that object. Different types of objects have different built-in methods and attributes.
- Type casting is done using class constructor functions like `str()`, `int()`, etc.

Built-in data types
- Python provides a number of built-in types (i.e. classes) that cover a variety of different data representations.
- We can also create new classes, representing new types of data.
## Constants
### None
- The `NoneType` has 1 object value — [`None`](https://docs.python.org/3/library/constants.html#None).
- `None` is an object that signifies the absence of a value.
- `None` is returned from functions that don’t explicitly return anything.
- `None` has a truth value of `False`.
### Booleans: True, False
- The [`bool`](https://docs.python.org/3/library/functions.html#bool "bool") type has exactly 2 values: `True` and `False`. [^1]
- Internally, bool is a subtype of an integer:  `True` has a value of 1 and `False` has a value of 0.
- The built-in function [`bool()`](https://docs.python.org/3/library/functions.html#bool "bool") converts *<i>any value/object</i>* to a boolean.

> [!error|outlined] Falsy Values
> - Zero:  `0`, `0.0`, `0j`, `Decimal(0)`, `Fraction(0, 1)`
> - Constants: `None` and `False`
> - Empty Sequences and Collections: `''`, `()`, `[]`, `{}`, `set()`, `range(0)`

> [!correct|outlined] Truthy Values
> - One: `1`
> - warn Beware: All these values are true
>     - `"0"` or `"False"` (non-empty string)
>     - `[0]` or `[False]` (non-empty list)
>     - `(None,)` (but `(None)` is false)
>     - `[[]]`
## Numbers
### Integers
- The [`int`](https://docs.python.org/3/library/functions.html#int) type represents *<i>whole numbers</i>*, positive or negative, **without decimals**.
- The [`int()`](https://docs.python.org/3/library/functions.html#int) constructor converts a number or string into an integer object.
- For example, `5`, `20`, `10000` are all integers.
### Float
- The [`float`](https://docs.python.org/3/library/functions.html#float "float") type represents <i>floating-point numbers</i>, containing one or more decimals.
- The [`float()`](https://docs.python.org/3/library/functions.html#float "float") constructor converts a number or string into a floating-point number
- For example, `5.0`, `0.25`, `1.6e5` are all floating point numbers.
- *Note:* `float('inf')` and `float('-inf')` represent +/- infinity.
## Sequences
**[Sequences](https://docs.python.org/3/library/stdtypes.html#typesseq) are data structures that store an [[python/glossary/glossary#ordered collection|ordered]] and ==indexed== collection of items.** For example: `list`, `tuple`, `range` and `str`.

> [!summary]- Features of sequences
> - ==indexed==: The first item has index `[0]`, the second item has index `[1]` etc.
> 	- `s[index]` — element lookup/access
> 	- `s.index(x)` — index of x
> 	- `s[-1]` — last item
> 	- `s[-4]` — 4th from the end
> 	- `s[:-3]` — going up to but not including the last 3 items.
> 	- `s[-3:]` — starting from the 3rd item from the end
>
> - ==slicing==: The slice syntax refers to sub-parts of a sequence. It creates a new object.
> 	- `s[start:end]` gives elements from index `start` up to *but not including* `end`.
> 	- `s[i:]`, `s[:j]` omitting either index defaults to the start or end
> 	- `s[i:j:k]` gives elements from i to j with a *step* `k` i.e. at index `i + n*k`
> 	- `s[:]` gives us a *copy* of a sequence
> 	- `s[:n] + s[n:] == s` partitions s into 2 parts, conserving all items (for any n)
>
> Sequences are also an [[python/glossary/glossary#iterable|iterable]] object. We can loop through items using a `for` loop, and use functions like [`zip()`](https://docs.python.org/3/library/functions.html#zip "zip") and [`map()`](https://docs.python.org/3/library/functions.html#map "map").
### Strings
> An immutable sequence (array) of characters

- Python has a built-in string class named [`str`](https://docs.python.org/3/library/stdtypes.html#str "str").
- Strings are ==arrays== ([[#Sequences|sequences]]) of bytes:
	- **Index** characters of the string with `string[index]`
	- **Loop** through each character with a `for` loop
- Strings are [[python/glossary/glossary#immutable|immutable]].
	- Cannot change a string after its created e.g. `string[index] = '\n'`
- String literals are enclosed in either ==single, double or triple quotes==:
	1. Single quotes: `'allows embedded "double" quotes'`
	2. Double quotes: `"allows embedded 'single' quotes"`
	3. Triple quoted: `'''Three single quotes'''` or `"""Three double quotes"""`
	- *Note:* Triple quoted strings can span multiple lines — all whitespaces will be included.
- Strings can also be created from other objects with the [`str()`](https://docs.python.org/3/library/stdtypes.html#str "str") constructor

```python
s = 'hi'
print(s[1])          ## i
print(len(s))        ## 2
print(s + ' there')  ## hi there
```

 The '+' operator can concatenate two strings. However, it does not automatically convert numbers or other types to string form. The `str()` function converts values to a string form so they can be combined with other strings.

```python error:2 success:3 file="String Concatentation"
pi = 3.14
text = 'The value of pi is ' + pi        ## NO, does not work
text = 'The value of pi is '  + str(pi)  ## yes 
```

#### f-strings
- Formatted string literals let you embed Python expressions inside `{` `}`.
- Prefix the string with `f` or `F` like so: `f"..."` or `f'...'`
- Expressions contained in '`{}`' are are printed out using the format specification described in [the format spec.](https://docs.python.org/3/library/string.html#formatspec)
- Any text outside of curly braces '`{}`' is printed out directly.

```python hlt:3|f":",hlt:6|f:,7,8
a = 10 
b = 20 
print(f"No primes between {a} and {b}")

# multi-line 
program=f"""#!/usr/bin/env python3
print('{string}')
"""
```
#### self-documented expressions
An f-string such as `f'{expr=}'` will expand to the text of the expression, an equal sign, then the representation of the evaluated expression. This is called a [self-documented expression](https://docs.python.org/3/whatsnew/3.8.html#f-strings-support-for-self-documenting-expressions-and-debugging) and it is useful feature of f-strings used for debugging. 

```python
>>> variable = "Some mysterious value"

>>> print(f"{variable = }")
variable = 'Some mysterious value'
```



### List `[ ]`
> An ordered, mutable sequence of elements

- Python has a built-in list class named [`list`](https://docs.python.org/3/library/stdtypes.html#list).
- List are like <i>dynamically sized arrays</i> except they **don't need to be homogeneous**.[^2]
- Lists are [[python/glossary/glossary#ordered collection|ordered]], ==indexed== and ==allow for duplicates==.
- Lists are [[python/glossary/glossary#mutable|mutable]]: we can modify the list in place with methods like `insert`, `remove` or `sort`
- For example, `[1, 2, 3]`, `['apple', 'banana', 'cherry']` are lists.

```python
l = [1, 2, 3]
l.append(4)       # Add element: [1, 2, 3, 4]
l.remove(2)       # Remove element: [1, 3, 4]
element = l[1]    # Access element: 3

l = ['a', 'b', 'c']
l.insert(1, 'd')  # Insert element at index 1: ['a', 'd', 'b', 'c']
l.pop()           # Remove last element: ['a', 'd', 'b']
```

> [!summary|outlined] Creating Lists
> We construct lists with square brackets:
> - Empty list: `[]`
> - Square brackets: `[a]`, `[1, 2, 'apple']`
> - List comprehension: `[x for x in iterable]`
> - [`list()`](https://docs.python.org/3/library/stdtypes.html#list) constructor: `list()` or `list(iterable)`

### Tuple `(,)`
> An ordered, immutable sequence of elements

- The built-in [tuple](https://docs.python.org/3/library/stdtypes.html#tuple) class represents an **immutable list**, so it cannot be changed once created. Tuples are great for storing data that you don't want to modify.
- Tuples are [[python/glossary/glossary#ordered collection|ordered]], ==indexed== and ==allow for duplicates== => *same as lists*
- Tuples are [[python/glossary/glossary#immutable|immutable]] => whereas *lists are mutable*
- For example, `(1, 2, 3, 4, 5)` is a tuple.

```python
t = ('foo', 'bar', 'baz')
element = t[0]        # Access element: 'foo'
t[0] = 'qux'          # TypeError: Tuples are immutable
```

> [!summary|outlined] Creating Tuples
> We construct tuples with round brackets:
> - Empty tuple: `()`
> - & Singleton tuple: `(a,)` <font color="#a5a5a5">Note trailing comma! </font>
> - Round brackets: `(a, b, c)`, `(1, 'a', 3.14)`
> - [`tuple()`](https://docs.python.org/3/library/stdtypes.html#tuple "tuple") constructor: `tuple()` or `tuple(iterable)`
### Range
> An ordered, immutable sequence of numbers

- [Range](https://docs.python.org/3/library/stdtypes.html#range) is an [[python/glossary/glossary#ordered collection|ordered]] and [[python/glossary/glossary#immutable|immutable]] sequence of **numbers**.
- It is commonly used for *looping* a specific number of times in `for` loops.

```python
range(stop)
range(start, stop[, step])
```

The [`range()`](https://docs.python.org/3/library/stdtypes.html#range "range") constructor has 3 parameters:

- `start=0` *(optional)* is the first number in the sequence (**inclusive**) ⇒ default is `0`
- `stop` is the limit, i.e. the position to stop (**not included / exclusive**)
- `step=1` *(optional)* is the increment ⇒ default is `1`

> [!col]
 >>[!div]
> > For a positive step:
> > `r[i] = start + step * i` where `r[i] < stop`.
> > ```python
> > # for (int i = 0, i < 10, i++)
> > for i in range(0, 10, 1):
> > 	print(i)  
> > 	
> > # 0, 1, 2, 3, 4
> > ```
>
>> [!col-md]
>> For a negative step:
>> `r[i] = start + step * i` where `r[i] > stop`.
>> ```python
>> # for (int i = 0, i > -5, i--)
>> for i in range(0, -10, -1):
>> 	print(i)  
>> 	
>> # 0, -1, -2, -3, -4
>> ```
## Collections
### Dictionary `{ }`
> An ordered, mutable mapping of key-value pairs

- Python has a built-in mapping class named [dict](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict).
- Dictionary is an [[python/glossary/glossary#ordered collection|ordered]] and [[python/glossary/glossary#mutable|mutable]] collection of **key: value** pairs.
	- Values are ==indexed== by keys: `dict[key] = value-for-that-key`
	- Keys must be [[python/glossary/glossary#hashable|hashable]] — **immutable** and **unique** — e.g. *strings* and *numbers*
- Dictionary ==does not allow for duplicates==.[^3]
- For example, `{"name": "John", "age": 30}` is a dictionary.

```python
'''
Build a dictionary
'''
dict = {}
dict['a'] = 'alpha'
dict['o'] = 'omega'
dict['g'] = 'gamma'

# or
dict = {'a': 'alpha', 'o': 'omega', 'g': 'gamma'}

'''
Look up
'''
# Look up a value with a key
print(dict['z'])      # Throws KeyError if key doesn't exist
print(dict.get('z'))  # None (instead of KeyError)

# Get the .keys() list
print(dict.keys())    # dict_keys(['a', 'o', 'g'])

# Get the .values() list
print(dict.values())  # dict_values(['alpha', 'omega', 'gamma'])

# Get the .items() list of (key, value) tuples
print(dict.items())   # dict_items([('a', 'alpha'), ('o', 'omega'), ('g', 'gamma'])

'''
Add a new key-value pair
'''
dict['d'] = 'delta'

'''
Remove a key-value pair
'''
del dict['z']         ## Throws KeyError if key doesn't exist
dict.pop('z', None)   ## None (instead of KeyError)

'''
Iterate over a dict
'''
# By default, iterating over a dict iterates over its keys
# Note that the keys are stored in insertion order
for key in dict:
  print(key) # a o g d

# Exactly the same as above
for key in dict.keys():
  print(key)

# Common case -- loop over the keys in sorted order,
# accessing each key/value
for key in sorted(dict.keys()):
  print(key, dict[key])

# Also a common case -- loop over the .items() tuple list,
# accessing each (key, value)
for k, v in dict.items():
  print(k, '->', v)
```

> [!summary|outlined] Creating Dicts
> We can create dictionaries like so:
> - Comma-separated list inside braces: `{'jack': 12, 'sjoerd': 10}`
> - Dict comprehension:  `{x: x ** 2 for x in range(10)}`
> - [`dict()`](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict)constructor: `dict([(1, 'a'), (2, 'b')])`, `dict(foo=100, bar=200)`

> [!summary]- dict() constructor
> The argument to `dict()` should be an [iterable](https://docs.python.org/3/glossary.html#term-iterable) of <abbr data-title="i.e. each item must be an iterable with exactly 2 elements">key-value pairs</abbr>.
>
> For example, all of these create a dictionary equal to `{"one": 1, "two": 2, "three": 3}`.
> *Note:* Dictionaries preserve insertion-order.
>
> 1. List of Tuples
>
> ```python hlt:[:]
> dict([('two', 2), ('one', 1), ('three', 3)])  
> # {'two': 2, 'one': 1, 'three': 3}
> ```
>
> 2. Keyword Arguments
>
> ```python hlt:one:3
> dict(one=1, two=2, three=3)
> # {'one': 1, 'two': 2, 'three': 3}
> ```
>
> 3. Zip object (iterator of tuples)
>
> ```python hlt:zip:)
> dict(zip(['one', 'two', 'three'], [1, 2, 3]))
> # {'one': 1, 'two': 2, 'three': 3}
> ```
>
> 4. Dictionary
>
> ```python hlt:{:}
> dict({'three': 3, 'one': 1, 'two': 2})
> # {'three': 3, 'one': 1, 'two': 2}
> ```

### Set `{,}`
> An unordered, mutable collection of unique elements

- A [set](https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset) is an [[python/glossary/glossary#unordered collection|unordered]] collection with ==no duplicate== [[python/glossary/glossary#hashable|hashable]] items.
	- Set elements are always unique/distinct => *unlike lists or tuples*.
	- Sets elements *cannot be indexed* => the only way to access them is through looping.
- Sets are [[python/glossary/glossary#mutable|mutable]] but its elements must be ==immutable (hashable)==
	- Set elements, like dictionary keys, *must be hashable* and *cannot be lists, dicts or sets*.
	- Set elements can be changed used methods like `add()` and `remove()`.
- Common uses:
	- & Remove duplicates from a sequence (e.g. list or tuple).
	- Perform logical mathematical operations like intersection, union, difference, and symmetric difference:
		-  `isdisjoint()`: Check if 2 sets have no common elements
		- `issubset()`, `issuperset()`: Check if 1 set has every element of the other
		- `union()`: Combine 2 sets into 1 (effectively removes any duplicates b/w the 2)
		- `intersection()`: Get all the common elements between 2 sets
		- `difference()`: Get all the elements in the set that are not in the other
		- `symmetric_difference()`: Get all the elements NOT common to both

```python file="Sets are mutable!" error:3 success:5-7
s = {1, 2, 3}
s.add(4)     # Add element: {1, 2, 3, 4}
s.add(4)     # s is still the same (no duplicates)
s.remove(2)  # Remove element: {1, 3, 4}
for x in s:  # Access elements: 1, 3, 4
    print(x)
```

```python file="Sets remove all duplicates!"
# Remove duplicates from a list
items = [1, 2, 3, 1, 2, 3]
unique_items = list(set(items))  # unique_items = [1, 2, 3]

# Remove duplicates from a tuple
items = (1, 2, 3, 1, 2, 3)
unique_items = tuple(set(items))  # unique_items = (1, 2, 3)
```

> [!summary|outlined] Creating Sets
> Create a set using curly braces:
> - Comma-separated list inside braces: `{'jack', 'sjoerd'}`
> - Set comprehension: `{c for c in 'abracadabra' if c not in 'abc'}`
> - [`set()`](https://docs.python.org/3/library/stdtypes.html#set "set") constructor: `set(iterable)`
>

[^1]: Note that the first letter must be capitalised — `true` and `false` is not defined.
[^2]: Lists can store objects of **different types.**
[^3]: If there are duplicate keys, the last key overwrites the previous one.
