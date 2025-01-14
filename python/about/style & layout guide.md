[PEP9 style guide]([PEP-257](http://www.python.org/dev/peps/pep-0257/))
[Google Python style guide](https://google.github.io/styleguide/pyguide.html)

- Use 4-space indentation
- Limit all lines to a maximum of 79 characters.
- Write [[documentation string ("docstring")]] for all public modules, functions, classes, and methods.
- `lowercase_with_underscores` for function/method names
- Use consistent quote marks for strings: either `'` or `"`
- Do not write `if x == True` or `if x == False` for truth testing ([[#truth value testing don't do `if x == True`|more info]])
- Use an hash mark (`#`) to start a **single-line comment**
- Use triple quotes (`"""`) around a **multi-line comment**
## function and variable names
The convention is to use `lowercase_with_underscores` names for functions and methods (and `UpperCamelCase` for classes).

- Use **verbs** that reflect what the **function does** (since functions are actions).
	- e.g `compute_x`
- Use `is_xxx()` and `has_xxx()` for **boolean functions** (that return true or false)
- Use **nouns** that reflect what the **variable stores**. Some idiomatic short variable names:
	- `s` - generic string
	- `n` - generic integer
	- `f` - opened file
	- `d` - dictionary
	- `ch` or `char` - character from a string
	- `i`, `j`, `k` - loop index

```python
delete_files(files)

count = count_duplicates(coordinates)

if is_weak(password):
	...
```
## comments
- Use an hash mark (`#`) to start a single-line **comment**
- Use triple quotes (`"""`) around a multi-line **comment**

Comments start with a `#`  and Python will render the rest of the line as a comment.

```python
print("Hello, World!")    # This is an inline comment
# print("Hello, World!")
```

Python does not have a syntax for multiline comments. You can either put a `#` in front of each line, or use a multiline string. Since Python ignores string literals that are not assigned to a variable, you can place your comment in triple quotes:

```python
"""  
This is a comment  
written in  
more than just one line  
"""
print("hello")
```

As long as the string is **not assigned to a variable**, Python will read the code, but then ignore it.
## statements
Python **doesn’t require** the use of semicolon _`;`_ between statements or to end statements.

Instead,  we use **newlines (not semicolons)** to mark the end of a statement.

Each statement is written on its own line:

```python
x = 10
print(x)
```

While semicolons are not required, you **can** use them to separate multiple statements on the same line. However, this is generally discouraged in Python as it reduces readability.

## indentation
Indentation refers to the number of spaces at the start/beginning of a code line.

**code blocks and indentation**
A code block is one or more lines of code that are intended to be executed as a set. For example, a code block can be a function body, or the statements within a loop.

> [!quote|no-title]
> In Python, a code block is defined by the amount of indentation:
> **Lines of code that have an equal amount of indentation are in the same code block**
> 
> ```hl:3-5
> # lines 2-4 belong to one code block
> line1
>     line2
>     line3
>     line4
> line5
> ```

Indentation is mandatory in Python and must be exact. This is different from other programming languages like C, where a code block is denote by curly brackets, and indentation is used only to improve the readability of the code.

```python 
if 5 > 2:  
  print("Five is greater than two!")
```

**A logical block of statements must all have the same indentation.** If one of the lines in the group has a different indentation, Python will flag it as a syntax error.

```python
# Aligned with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# Add an extra level of indentation to distinguish arguments from the rest.
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# Hanging indents should add a level.
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
```
## spacing
### single space between operators and items
Use a single space to separate the operators and items and operators from each other:

```python
bound = x * 12 + 13
if x >= 4:
    print(x + 2)
```

### parenthesis no space
The left and right parenthesis `()` and square brackets `[]` do not have spaces separating them from their contents.

```python hlt:(),(1,'),[1,6]
run_along(1, 2 * 3, 'hi')
bark()
lst = [1, 2, z * 6]
```

### space after comma / colon
A comma or colon has 1 space after it, but no spaces before it.

```python
foo(1, 'hello', 42)  # comma: 0 space before, 1 space after
[1, 2, 3]            # e.g. list
{'a': 1, 'b': 2}     # e.g. dict
```

*EXCEPTION:* Slices are an exception to the above rule. The slice colon should have no spaces (or 1 space on either side).

```python
s[start:end + 1]     # slice - no spaces
```
## truth value testing
### don't do `if x == True`
In Python, the `if` statement can distinguish `True` vs. `False` values itself, so you don't need to explicitly compare an object to `True` or `False`.

```python error:2 success:3
def print_greeting(words, shout_mode):
    if shout_mode == True:   # NO not like this
    if shout_mode:           # YES like this
        print(words.upper())
    else:
        print(words)
```

```python error:2 success:3
def print_greeting(words, shout_mode):
    if shout_mode == False:   # NO not like this
    if not shout_mode:        # YES like this
        print('Not shouting')
    else:
        print(words)
```
### do `x is not None` instead of `not x` 
Avoid `if obj:` or `if not obj:` if we are testing for `None` because it evaluates all falsy values like `0`, `False`, `[]`, `''`. So if we want to specifically check for `None`, do this:
```python
if obj is not None:             ## YES
    print("Object exists!")

if not obj:                     ## NO! 
    print("Object is None or falsy!")
    
if obj != None:                 ## Not recommended
    print("Object exists!")
```
## keywords
These identifiers are used as *reserved words*, or *keywords* so you cannot use them as variable or function names.

```python
>>> import keyword
>>> keyword.kwlist
```

```
False      await      else       import     pass
None       break      except     in         raise
True       class      finally    is         return
and        continue   for        lambda     try
as         def        from       nonlocal   while
assert     del        global     not        with
async      elif       if         or         yield
```
