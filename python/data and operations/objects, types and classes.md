[Data model python.org](https://docs.python.org/3/reference/datamodel.html)
[variables vs objects](https://www.practicaldatascience.org/notebooks/PDS_not_yet_in_coursera/20_programming_concepts/vars_v_objects.html)
## Mutable vs. Immutable Types
Certain data types in Python are called “immutable.” That means an object, once created, can’t actually be modified. As a result, if you want to do something that looks like modifying the object, Python has to create _an entirely new object_ that lives in a new location.

Strings, for example, are “immutable.” So if we create a string, then try and modify it, what we’re actually doing is creating a new string that has the features we want:

> [!col]
> ```python info:2
> x = "my string"
> y = x
> 
> id(x) == id(y) # True: x and y point to the same object
> ```
![var_v_object_string_1](https://www.practicaldatascience.org/_images/var_v_object_string_1.png)

> [!col]
> 
> ```python info:1
> x = x.upper()  # x is now'MY STRING'
> 	
> id(x) == id(y) # False: x and y now point to different object
> ```
> ![var_v_object_string_2](https://www.practicaldatascience.org/_images/var_v_object_string_2.png)


> [!important]
> **if you mutate a mutable object, that change will propagate to all variables that point at said object. But if you modify an immutable object, a new object will actually be created, so that change will not be accessible to variables pointing at the old object**


**Some immutable objects**
- numbers (`int`, `float`, `complex`)
- ==strings (`str`)==
- ==tuples (`tuple`)==
- booleans (`bool`)
- frozen sets

**Some mutable objects**
- lists (`list`)
- dictionaries (`dict`)
- sets (`set`)

> [!NOTE]
> **Nearly anything that is a collection of other objects is mutable — except `tuples`.** 
> Therefore, tuples are useful for storing data that you want to keep immutable.

## Special / "Private" / "Magic" Attributes
All objects contain "private" attributes that may be methods that are indirectly called, or internal "meta" information for the object.
### `__dict__`
The `__dict__` attribute shows any attributes stored in the object.

```
>>> list.__dict__.keys()
['__getslice__', '__getattribute__', 'pop', 'remove', '__rmul__', '__lt__', '__sizeof__',
 '__init__', 'count', 'index', '__delslice__', '__new__', '__contains__', 'append',
 '__doc__', '__len__', '__mul__', 'sort', '__ne__', '__getitem__', 'insert',
 '__setitem__', '__add__', '__gt__', '__eq__', 'reverse', 'extend', '__delitem__',
 '__reversed__', '__imul__', '__setslice__', '__iter__', '__iadd__', '__le__', '__repr__',
 '__hash__', '__ge__']
```

The `dir()` function will show the object's available attributes, including those available through inheritance:

```
>>> dir(list)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__delslice__',
 '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__',
 '__getslice__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__iter__',
 '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__',
 '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__',
 '__setslice__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'count',
 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

In this case, `dir(list)` includes attributes not found in `list.__dict__`.
### `__bases__`
The `__bases__` attribute tells us which class(es) the object inherits from.
