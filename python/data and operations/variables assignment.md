- **Variables are names for objects.** Variables are simply labels for an object's location in memory. When we assign a value to a variable, we are creating an object with the value and assigning it a name/label. Each object is referred to by its assigned name (variable).
- **No type declarations**. Python is [[python/glossary/glossary#dynamically typed|dynamically typed]], meaning that variables are not bound to a specific type of object. Instead, the variable type is determined by the object assigned to it at runtime.

> [!note|no-title]
> In Python, variables don’t have data types. Instead, the objects that the variable points to has types.
## evaluation order
Python evaluates expressions from left to right.
However, when evaluating an assignment, the RHS is evaluated before the LHS:

```
expr3, expr4 = expr1, expr2
```

## variable assignment
> Assignment statements re(bind) *names* to values.

A variable is created the moment you first assign a value to it.

```python
n = 300      # n points to an integer object with a value of 300
m = n        # m points to the same object as n
```

![caption|centre|300](https://files.realpython.com/media/t.d368386b8423.png)
<i class="figcaption" id="centre">Multiple References to a Single Object</i>

If a variable is not “defined” (assigned a value), trying to use it will give you an error:

```python
>>> n        # try to access an undefined variable
```

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'n' is not defined
```

Because Python is dynamically typed, you can make variables refer to objects of different data types in different moments just by reassigning the variable:

```python
>>> age = "19"
>>> type(age)
<class 'str'>

>>> subjects = {"Math", "English", "Physics", "Chemistry"}
>>> type(subjects)
<class 'set'>
```

## multiple assignment
We can assign *multiple* values to *multiple* variables in one line:

```python
x, y, z = "Orange", "Banana", "Cherry"  
```

or assign the *same* value to *multiple* variables in one line:

```python
x = y = z = "Orange"  
```
## packing
In an assignment where you assign *multiple* values[^1] to a *single* variable:

```python hlt:":
my_tuple = "hello", "world", 123, [1, 2, 3]
```

The values above are "**packed**" together in a single tuple:

```
('hello', 'world', 123, [1, 2, 3])
```

This is because the RHS is evaluated first (see [[#evaluation order]]).

And by default, an [[expression list]] that contains **at least one comma** such as `1,` creates a tuple:

```python
my_tuple = 1,    # Creates a tuple (1,)
my_tuple = (1,)  # Same as above
```

So an assignment like this:

```
var = 1, 2
```

evaluates to this:
1. RHS creates a tuple `(1, 2)`
2. Assign the LHS to the tuple `var = (1, 2)`
## unpacking
The reverse operation is called *unpacking*, where each variable is assigned to the corresponding tuple item:

```python hlt:a:d
a, b, c, d = my_tuple
print(a)  # hello
print(b)  # world
print(c)  # 123
print(d)  # [1, 2, 3]
```

We can also "unpack" multiple values from a list like this:

```python hlt:a:c
a, b, c = [1, 2, 3]
print(a)  # 1
print(b)  # 2
print(c)  # 3
```

> [!alert|no-title]
> The **number of assignment targets** must match the **number of elements in the iterable

```python error:1
a, b = [1, 2, 3]    # ValueError: trying to assign 3 values to 2 variables
```

To solve this, we can use the unpacking operator `*` to create a [[starred expression]] that collects all left-over values into a **list** and assigns it to a "catch-all" variable (`*b`):

```python hlt:*b
a, *b = [1, 2, 3] 
print(a)  # 1
print(b)  # [1, 2]
```
## swaps
In Python, we use multiple assignment to swap values without needing a temporary variable.

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
Instead of this:
```
temp = a  # save the value of `a`
a = b
b = temp
```
`````

`````col-md
flexGrow=1
===
We can do this in one line like this:
```
a, b = b, a
```
`````
``````

<u>Syntax</u>
```python
# swap the values of a and b
a, b = b, a
```

1. RHS creates a tuple `(b, a)`
2. LHS unpacks the tuple, assigning the first value to `a`, and the second value to `b`.
## throwaway variable `_`
The single underscore `_` as a variable indicates a temporary or throwaway variable.

Usages:
1. Throwaway variables in loops and other constructs: **`_` is used to store unused values**
2. Placeholder variable in REPL sessions: **`_` holds the result of the last executed expression**
3. Wildcards in structural pattern matching ([[control flow#match / case|match-case]]): **`_` will match with everything**

> [!example] Example 1: `_` as a throwaway variable
> Use the variable name `_` to store an unneeded or unused value:
>
> ```python
> # we don't need the loop variable 
> for _ in range(5):
>     print("Hi")  
> 
> # we don't need a specific value when unpacking values
> fname, lname, _ = ["John", "Smith", "New York"] 
> print(fname, lname)  # John Smith
> 
> # in list comphrehension
> matrix = [[number for number in range(5)] for _ in range(5)]  
> # outer [... for _ in range(5)] creates 5 lists
> # inner [number for number in range(5)] fills each row with `number`
> ```

> [!example] Example 2: `_` as a placeholder variable in REPL
> In a REPL session, `_` stores the result of the last evaluated expression:
> ```python hlt:3,8
> >>> 12 + 30  
> 42
> >>> _
> 42
> 
> >>> pow(4, 2)
> 16
> >>> _
> 16
> ```
> You can access and use the `_` variable as you’d use any other variable:
>
> ```python hl:6
> >>> numbers = [1, 2, 3, 4]
> 
> >>> len(numbers)
> 4
> 
> >>> sum(numbers) / _  # sum(numbers) / 4
> 2.5
> ```
>
> > [!alert|no-title]
> > Note: This behaviour for `_` will only work in interactive mode (not script mode).

> [!example] Example 3: `_` wildcard in match/case
>
> ```python hlt:8
> match status:
> 	case 400:
> 		return "Bad request"
> 	case 404:
> 		return "Not found"
> 	case 418:
> 		return "I'm a teapot"
> 	case _:
> 		return "Something's wrong with the internet"
> ```

[^1]: Multiple values separated by at least one comma evaluates to a **tuple**. It is also referred to as an [[expression list]].