Operators perform operations on values.

- Arithmetic operators
- Assignment operators
- Comparison operators
- Logical operators
- Identity operators
- Membership operators
- Bitwise operators
## Arithmetic Operators
> Perform *arithmetic operations* on numeric values.
> Note: `+` and `*` can be used with any sequence types (`str`, `list`, `tuple`)

| Operator | Expression              | Operation                                                       |
| -------- | ----------------------- | --------------------------------------------------------------- |
| `+`      | `x + y`                 | Addition, [[#^sequence-concatentation\|Sequence Concatenation]] |
| `-`      | `x - y`                 | Subtraction                                                     |
| `*`      | `x * y`                 | Multiplication, [[#^sequence-repetition\|Sequence Repetition]]  |
| `/`      | `x / y`                 | Division (returns `float`)                                      |
| `//`     | `x // y` = floor(x / y) | Floored Division (returns `int`) [^1]                           |
| `**`     | `x ** y` = x ^ y        | Exponentiation — x to the power of y                            |
| `%`      | `x % y`                 | Modulus — Remainder of `x / y`                                  |
## Concatenation and Repetition Operators
> The `+` and `*` operators can be used with sequences for *concatenation* and *repetition*.

For all sequences (`str`, `list`, `tuple`):
- `+`: Concatenation
- `*`: Repetition

| <div style="width:150px">Operator</div> | Returns                                                         |
| --------------------------------------- | --------------------------------------------------------------- |
| `seq_1 + seq_2`                         | New sequence containing all items from both `seq_1` and `seq_2` |
| `seq * n`                               | New sequence containing the items of `seq` repeated `n` times   |

> [!danger|no-title]
>  You can't **concatenate `+`** *different* types of objects.

```python file="Concatenation with +" success:1,7,10 error:4
"hello" + "world"   # string concatenation
# helloworld

"hello" + 5         # NO: can only add objects of same type
# TypeError: can only concatenate str (not "int") to str

[1, 2] + [3, 4]     # list concatenation
# [1, 2, 3, 4]

(1, 2) + (3, 4)     # tuple concatenation
# (1, 2, 3, 4)
```

^sequence-concatentation

```python file="Repetition with *" success:1,4,7
"Hi! " * 3      # repeat 'Hi! ' 3 times
# 'Hi! Hi! Hi! '

[1, 2] * 2      # repeat the list [1, 2] 2 times
# [1, 2, 1, 2]

("a", "b") * 3  # repeat the tuple ('a', 'b') 3 times
# ('a', 'b', 'a', 'b', 'a', 'b')
```

^sequence-repetition
## Assignment Operators
* `=` assigns a value to a variable
* `:=` assigns a value to a variable ==within an expression==. See [[assignment expression]].

```python hlt:6|y:0
# Regular assignment with =
x = 10
print(x)     # Output: 10

# Assignment expression with :=
if (y := 20) > x:
    print(y)  # Output: 20
```

| Operator | Operation                 | Example   | Equivalent   |
| -------- | ------------------------- | --------- | ------------ |
| `+=`     | Addition assignment       | `x += 3`  | `x = x + 3`  |
| `-=`     | Subtraction assignment    | `x -= 3`  | `x = x - 3`  |
| `*=`     | Multiplication assignment | `x *= 3`  | `x = x * 3`  |
| `/=`     | Division assignment       | `x /= 3`  | `x = x / 3`  |
| `//=`    | Floor division assignment | `x //= 3` | `x = x // 3` |
| `%=`     | Modulus assignment        | `x %= 3`  | `x = x % 3`  |
| `**=`    | Exponentiation assignment | `x **= 3` | `x = x ** 3` |
| `&=`     | Bitwise AND assignment    | `x &= 3`  | `x = x & 3`  |
| `│=`     | Bitwise OR assignment     | `x │= 3`  | `x = x │ 3`  |
| `^=`     | Bitwise XOR assignment    | `x ^= 3`  | `x = x ^ 3`  |
| `<<=`    | Left shift assignment     | `x <<= 3` | `x = x << 3` |
| `>>=`    | Right shift assignment    | `x >>= 3` | `x = x >> 3` |
## Comparison Operators
> Compare the *values* of 2 objects and return a [[data types#Booleans True, False|boolean]] (`True` or `False`)

- `==` compares values
- `is` compares identity (memory address)

```python
2 == '2' # False (different data types)

a = dict(name="John", age=30)
b = {"name": "John", "age": 30}

a == b   # True
a is b   # False
```

| Operation | Operation             |
| --------- | --------------------- |
| `==`      | equal to              |
| `!=`      | not equal to          |
| `<`       | strictly less than    |
| `<=`      | less than or equal    |
| `>`       | strictly greater than |
| `>=`      | greater than or equal |
## Identity Operators — `is`, `is not`
> Compare the *identity (memory address)*[^2] of 2 objects and return a [[data types#Booleans True, False|boolean]] (`True` or `False`)

| <div style="width:100px">Operator</div> | Description                                    |
| --------------------------------------- | ---------------------------------------------- |
| `x is y`                                | True if both variables are the same object     |
| `x is not y`                            | True if both variables are not the same object |

> [!col]
>
> ```python file="Same object"
> a = []
> b = a
> 
> a == b  # True
> a is b  # True
> ```
>
> ```python file="Different objects"
> a = []
> b = []
> 
> a == b  # True
> a is b  # False
> ```

## Membership Operators — `in`, `not in`
> Check if a given value `is` or `is not` a member of a collection.

| <div style="width:200px">Expression</div> | Description                        | <div style="width:200px">Example</div> |
| ----------------------------------------- | ---------------------------------- | -------------------------------------- |
| `x in collection`                         | True if `x` is in `collection`     | `5 in [4, 5, 6]`                       |
| `x not in collection`                     | True if `x` is not in `collection` | `7 not in [4, 5, 6]`                   |

## Boolean Operators — `and`, `or`, `not`
> Operate on the *boolean values* of operands.[^3]

| Expression | <div style="width:230px">Description</div>                     | Example               |
| ---------- | -------------------------------------------------------------- | --------------------- |
| `x or y`   | ==Logical OR==: True if *at least one* of the operands is true | `if a > 0 or b > 0:`  |
| `x and y`  | ==Logical AND==: True if *both* the operands are true          | `if a > 0 and b > 0:` |
| `not x`    | ==Logical NOT==: True if the operand is false (and vice versa) | `if not a:`           |

> [!alert|no-title]
> Use the built-in `bool()` function to check the boolean value (`True` or `False`) of an object
## Unpacking Operator — `*`, `**`
- A single asterisk `*` *unpacks* items from an **iterable** (lists, tuples, sets, and strings)
- A double asterisk `**` *unpacks* key-value pairs from a **dictionaries**
### Iterable Unpacking
Unpacking allows you to assign the unpacked values to multiple variables:
> [!col]
>
> ```python file="Tuple Unpacking" hlt:2, error:7-8
> my_tuple = (1, 2, 3)
> a, b, c = my_tuple
> print(a)  # 1
> print(b)  # 2
> print(c)  # 3
> 
> a, b, c = (1, 2, 3, 4, 5)
> # ValueError: not enough values to unpack (expected 5, got 3)
> ```
>
> ```python file="With starred expression" hlt:1
> a, *b, c = (1, 2, 3, 4, 5)  
> print(a)   # 1
> print(b)   # [2, 3, 4] - list
> print(c)   # 5
> ```

Or pass the unpacked items into functions as arguments:
> [!col]
>
> ```python file="List Unpacking" hlt:*:]
> def multiply(x, y, z):
>     return x * y * z
>     
> multiply(*[2, 3, 4])   
> # same as: multiply(2, 3, 4)
> ```
>
> ```python file="Dictionary Unpacking" hlt:**{:}
> def greet(name, age):
>     print(f"{name}, {age}")
> 
> greet(**{"name": "Alice", "age": 25})  
> # same as: greet(name="Alice", age=25)
> ```

And merge multiple lists/dicts into one:
> [!col]
>
> ```python file="Merging Lists" hlt:4|[:]
> nums = [1, 2, 3]
> more_nums = [4, 5, 6, 7]
> 
> all_nums = [*nums, *more_nums]
> # [1, 2, 3, 4, 5, 6, 7]
> ```
>
> ```python file="Merging Dictionaries" hlt:4|{:}
> dict_1 = {'a': 1, 'b': 2, 'c': 3}
> dict_2 = {'one': 'two', 'three': 'four'}
> 
> dict_3 = {**dict_1, **dict_2}
> # {'a': 1, 'b': 2, 'c': 3, 'one': 'two', 'three': 'four'}
> ```

See [[packing & unpacking]] for more info.
### Iterable Packing
The `*` operator can be used to create a "catch-all" variable in both functions and assignments.

- `*var` is an **assignment target** collects items into a *list*.
- `*args` is an **arbitrary argument** collects items into a *tuple* (immutable).

> [!col]
>
> ```python file="assignment target" info:1
> a, b, *c = range(5)
> print(a)  # 0
> print(b)  # 1
> print(c)  # [2, 3, 4] - list
> ```
>
> ```python file="arbitrary argument" info:1,6
> def foo(a, b, *c):
>     print(a)  # 0
>     print(b)  # 1
>     print(c)  # (2, 3, 4) - tuple
> 
> foo(range(5))
> ```

[^1]: `id()` returns the **floor** of `+` (**rounds it *DOWN* to the nearest integer**).
  For example: **3/2 = 1.5** whereas **3//2 = 1**
[^2]: You can check the identity of an object with the `id()` function.
[^3]: You can check the boolean value (`True` or `False`) of an object with the `bool()` function.