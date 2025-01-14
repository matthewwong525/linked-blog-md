
- A single asterisk `*` *unpacks* items from **iterables** (lists, tuples, sets, and strings);
- A double asterisk `**` *unpacks* **dictionaries**;
- Using a single asterisk on a dictionary will unpack only dictionary keys;
- You can pass all iterable items to a function with the help of unpacking operators;
- The [[packing & unpacking#Starred Assignment Target|starred expression]] in `first, *rest = seq` *unpacks* <abbr data-title="all remaining items not assigned to a variable">left-over</abbr> iterable items into a **list**;
- The [[functions#arbitrary arguments|arbitrary argument]] in `def func(*args)` <i>packs</i> positional arguments into a **tuple**;
- The [[functions#arbitrary arguments|arbitrary argument]] in `def func(**kwargs)` <i>packs</i> keyword arguments into a **dictionary**
## Packing
> Packing refers to the process of putting multiple values into a single iterable.

Packing values into an iterable can be done in 2 ways:

1. Assign multiple <u>values</u> to a single **variable**
2. Assign multiple <u>arguments</u> to a single **variable** with `*args` or `**kwargs` [^1]

> [!col]
> > [!div]
> > Packing into a Variable:
> > ```python hlt:1
> > my_tuple = 1, 2, "hello"
> > print(my_tuple)  # (1, 2, 'hello')
> > ```
>
> > [!div]
> > Packing into a Parameter:
> > ```python hlt:2|args,4|1:o'
> > def func(*args):
> >     print(args)   # (1, 2, 'hello')
> > 
> > func(1, 2, 'hello')
> > ```

> [!1|teal] Packing Tuples
> In an assignment where you assign *multiple* values to a *single* variable:
> 
> ```python
> my_tuple = "hello", "world", 123, [1, 2, 3]
> ```
> 
> The values above are "**packed**" together in a single tuple:
> 
> ```
> ('hello', 'world', 123, [1, 2, 3])
> ```
> 
> This is because in an assignment, the RHS expressions are evaluated first.
> 
> And by default, an [[expression list]] that contains **at least one comma** such as `1,` creates a tuple:
> 
> ```python
> my_tuple = 1,    # Creates a tuple (1,)
> my_tuple = (1,)  # Same as above
> ```
> 
> So in an assignment like this, it evaluates in this order:
> 1. RHS creates a tuple `(1,)`
> 2. LHS assigns the name to the RHS: `my_tuple = (1,)`

> [!2|pink] Packing Arguments 
> The `*args` and `**kwargs` [[functions#arbitrary arguments|arbitrary arguments]] packs all remaining, unassigned arguments into a tuple or dictionary:
> 
> 1. `*args` collects **non-keyword (positional) arguments** into a [[data types#Tuple `(,)`|tuple]]
> 2. `**kwargs` collects **keyword arguments** (key-value pairs) into a [[data types#Dictionary `{ }`|dictionary]]
> 
> 
> ```python
> def func(*args, **kwargs): 
> 	print('positional arguments:', args) 
> 	print('keywords arguments:', kwargs)
> 
> # Call the function
> func('COMP', 2041, 9044, answer=42, option=False)
> ```
> 
> ```
> positional arguments: ('COMP', 2041, 9044)
> keywords arguments: {'answer': 42, 'option': False}
> ```

## Unpacking
> Unpacking is the process of extracting values from an iterable and assigning them to multiple variables.

The reverse operation is called unpacking, where each value from an iterable is assigned to corresponding variables or passed as function arguments.

Unpacking values from an iterable can be done in 3 ways:

1. Assign multiple variables to a single iterable
2. Using the [[operators#Unpacking Operator — `*`, `**`|unpacking operators]] (`*` and `**` ) in front the iterable
3. Using the [[starred expression]] as an assignment target to an iterable
 
> [!1|teal] Unpacking Tuples
> **Note:** The variables for unpacking are on the LHS of the assignment operator `=`
>
>  ```python file="Unpacking a Tuple" hlt:2
> my_tuple = (1, 2, 3)
> a, b, c = my_tuple
> print(a)  # 1
> print(b)  # 2
> print(c)  # 3
> ```
>
> ```python file="Unpacking a Dictionary" hlt:2
> my_dict = {'fname': 'Jack', 'lname': 'Wallen', 'country': 'USA'}
> fname, name, country = my_dict.values()
> print(fname)    # Jack
> print(name)     # Wallen
> print(country)  # USA
> ```
> The **number of assignment targets** must match the **number of elements in the iterable**!
>
> ```python error:1
> a, b = [1, 2, 3]    # ValueError: trying to assign 3 values to 2 variables
> ```
> To avoid this issue, we can use a [[starred expression]] instead, which unpacks the tuple and collects all remaining and unassigned to the starred expression.

> [!2|pink] Unpacking Arguments
> `**` unpacks a dictionary into keyword arguments
>
> ```python  file="Unpacking a Dictionary" hlt:4|**:}
> def greet(name, age):
>     print(f"Hello {name}, you are {age} years old")
> 
> greet(**{"name": "Alice", "age": 25})  # same as: greet(name="Alice", age=25)
> ```
>
> `*` unpacks a sequence (list, tuple, set etc.) into positional arguments
>
> ```python file="Unpacking a List" hlt:4|*[:]
> def multiply(x, y, z):
>     return x * y * z
>     
> multiply(*[2, 3, 4])   # same as: multiply(2, 3, 4)
> ```

> [!3|purple] Starred Expression
> Recall that when unpacking a tuple in an assignment,  the number of variables on the left should be equal to the number of the elements on the right. Otherwise, it raises a `ValueError`:
> 
> ```python error:2,5
> a, b, c = 'hello', 'world', 123, [1, 2, 3]
> # ValueError: too many values to unpack (expected 3)
> 
> a, b, c, d, e = 'hello', 'world', 123, [1, 2, 3]
> # ValueError: not enough values to unpack (expected 5, got 4)
> ```
> 
> To solve this issue, we can use the [[starred expression]].
> 
> The `*` operator in front of name *unpacks* all the <abbr data-title="items that haven't been assigned to a variable">remaining</abbr> iterable items into a `list`:
> 
> ```python hlt:*b
> a, *b = [1, 2, 3] 
> print(a)  # 1
> print(b)  # [1, 2]
> ```
> 
>  `*var` is creates a =="catch-all" variable== named `var` which collects all *remaining and unassigned* items from the iterable in a ***list* (not tuple)**. 
> 
> For example, we can split a **sequence** into 3 different variables:
> 
> ```python hlt:1|*middle,1|2:4
> first, *middle, last = (1, 2, 3, 4, 5)  
> 
> print(first)   # 1
> print(middle)  # [2, 3, 4] - list
> print(last)    # 5
> ```
> 
> 

### Unpacking into Positional Arguments
You can unpack an iterable when passing them to a function:
> [!col]
>
> ```python
> def multiple(a, b, c):
>   return a * b * c
> 
> nums = [1, 2, 3]
> ```
>
> ```python
> # use indexing: multiply(1, 2, 3)
> multiply(nums[0], nums[1], nums[2]) 
> 
> # use unpacking: multiply(1, 2, 3)
> multiply(*nums)   
> ```

This passes each item of an iterable as a [[functions#positional arguments|position argument]].
### Extended Iterable Unpacking
We can also print the elements from several iterable objects:

```python 
nums = [1, 2, 3]
more_nums = [4, 5, 6, 7]
print(*nums, *more_nums) 
# 1 2 3 4 5 6 7
```

Moreover, we can join multiple lists together:

```python file="Merging Lists"
nums = [1, 2, 3]
more_nums = [4, 5, 6, 7]
all_nums = [*nums, *more_nums]
print(all_nums)
# [1, 2, 3, 4, 5, 6, 7]
```

### Unpacking Dictionaries with `*`
While the single-asterisk operator unpacks lists, tuples, strings, and sets, it can also be used on dictionaries:

```python
my_dict = {'apple': 1, 'banana': 2, 'pear': 3}
print(*my_dict)
# apple banana pear
```

> [!alert|no-title]
> **Note:** Unpacking dictionaries with a `*` only unpacks its **keys** (not values).

To unpack dictionary keys, values, or key-value pairs, you can use the `*` operator together with dictionary operations `dict.keys()`, `dict.values()` and `dict.items()`:

```python file="Unpacking a dictionary with a single asterisk operator"
my_dict = {"a": 1, "b": 2, "c": 3}

# Unpacks the keys
a, b, c = my_dict
print(*my_dict)         # a b c
print(*my_dict.keys())  # a b c

# Unpacks the values
print(*my_dict.values()) # 1 2 3

# Unpacks the key-value pairs as tuples
print(*my_dict.items())  # ('a', 1) ('b', 2) ('c', 3)
```

## The double-asterisk operator `**`
While the single-asterisk operator unpacks **iterables** (lists, tuples, strings, and sets), the double-asterisk operator can unpack **dictionaries**.

Unfortunately, dictionaries cannot be unpacked in the same way as lists and tuples:

```python hlt:**middle
my_dict = {'apple': 1, 'banana': 2, 'pear': 3}
start, **middle, end = my_dict
# SyntaxError: invalid syntax
```

### Unpacking into Keyword Arguments
You can unpack the key-value pairs of a dictionary into [[functions#keyword arguments|keyword arguments]] to a function:

```python hlt:**my_dict
my_dict = {'apple': 1, 'banana': 2, 'pear': 3}

def fruit_sum(apple, banana, pear):
  return apple + banana + pear

print(fruit_sum(**my_dict)) # 6
```

> [!alert|no-title]
> Note that the function arguments must have the same name as the keys in a dictionary.

### Extended Dictionary Unpacking
The double asterisk can also merge several dictionaries into a new dictionary:

```python file="Merging Dictionaries" hlt:4|{:}
dict_1 = {'a': 1, 'b': 2, 'c': 3}
dict_2 = {'one': 'two', 'three': 'four'}

dict_3 = {**dict_1, **dict_2}
# {'a': 1, 'b': 2, 'c': 3, 'one': 'two', 'three': 'four'}
```

Note that duplicate keys from `dict_2` will overwrite those from the first:

```python
dict_1 = {'a': 1, 'b': 2, 'c': 3}
dict_2 = {'c': 4 }

# dict_2['c'] will overwrite dict_1['c']
merged = {**dict_1, **dict_2}
# { 'a': 1, 'b': 2, 'c': 4}
```

You can merge multiple dictionaries AND add extra key-value pairs to the existing ones:

```python hlt:2|{:}
my_dict = {'apple': 1, 'banana': 2, 'pear': 3}
my_dict_updated = {**my_dict, 'strawberry': 4}
print(my_dict_updated)
# {'apple': 1, 'banana': 2, 'pear': 3, 'strawberry': 4}
```

[^1]: See [[functions#arbitrary arguments|arbitrary arguments]] for more info