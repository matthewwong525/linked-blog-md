A Python program is made of many lines of code, stored in a `.py` file. Functions are important because they divide the code up into units of functionality, and control the flow of execution. 

- Use `lowercase_with_underscores` for functions and methods names
- Functions are first-class objects. They can be returned or pass around.
- Use docstrings

> [!info]
> **Parameter** is the variable named in the function definition:
>
> ```hlt:x,y
> function sum(x, y)
> ```
>
> **Argument** is the actual values passed to the function when called:
>
> ```hlt:(:)
> sum(5, 6)
> ```
>
## Defining Functions
The `def` keyword defines the name of the function along with its parameter list:

```python
def function_name(parameter1, parameter2, ...):
    # function body (must be indented)
    return value  # optional return statement
```

The first line of a function can be a [[documentation string ("docstring")]] that describes what the function does. 

```python
# Defines a "fib" function that takes 1 argument. 
def fib(n):   
    """
    Print a Fibonacci series less than n.
    """
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()

# Now call the function we just defined:
fib(100)

# Returns None
print(fib(0))  
```

> [!note|no-title]
> Functions without a return statement return `None` (not nothing)!

> [!alert|no-title]
> **Functions must be defined before they can be called** as Python executes code line-by-line.
## Function Parameters
By default, <i>parameters</i> have positional behavior, so in a call to the function, you need to supply values for the parameters in the same order that they were defined. When the function is called, the values in the function call are known as <i>arguments</i>.

- **Default arguments (optional)** assign a default value to the argument if it is not passed. This allows some arguments to be omitted when the function is called.
- **Arbitrary arguments** collect the remaining arguments in a tuple (`*arg`) or dict (`**kwarg`)
### default arguments values (optional arguments)
Parameters in the form `name=value` have a default argument value. If an argument is not provided in the function call, it will assume the default value. 

**Parameters with default arguments are optional.** If no argument is provided, the default value is used. If an argument is provided, it will overwrite the default value. 

> [!alert|no-title]
> **Default arguments must follow (appear after) the position arguments.** Keyword arguments should always follow positional arguments.

```python
# Defines a 'greet' function that accepts 1 required argument (name) 
# and 1 optional argument (greeting)
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")               # Hello, Alice!
greet("Bob", greeting="Hi")  # Hi, Bob!
```
### arbitrary arguments 
Arbitrary arguments allows **any number of arguments (including `0`)** to be passed in the function.

The asterisk operator `*` and `**` <i>before</i> a parameter creates a <i>"catch-all" parameter</i> that packs all remaining arguments into a tuple or dictionary:

1. `*args` collects **non-keyword (positional) arguments** into a [[data types#Tuple `(,)`|tuple]]
2. `**kwargs` collects **keyword arguments** (key-value pairs) into a [[data types#Dictionary `{ }`|dictionary]] 

> [!note|no-title]
> **Note**: Arbitrary keyword arguments (`**kwargs`) must follow arbitrary positional arguments (`*args`)

```python
def func(*args, **kwargs): 
	print('positional arguments:', args) 
	print('keywords arguments:', kwargs)

# Call the function
func('COMP', 2041, 9044, answer=42, option=False)
```

```
positional arguments: ('COMP', 2041, 9044)
keywords arguments: {'answer': 42, 'option': False}
```

> [!NOTE]
> When you use variable arguments, each value is no longer assigned a variable name. All values are now part of the _catch-all_ variable name that uses the asterisk (`args` and `kwargs` in this examples).
## Function Arguments
Function can be called with both positional (non-keyword) and keyword arguments.
However, all positional arguments must come before any keyword arguments:

1. **Positional arguments** match in order with the parameters declared in the function definition.
2. **Keyword arguments** match to the name of declared parameters, and may be specified in arbitrary order.
### positional arguments
Positional arguments means we pass arguments in the order in which the parameters are defined in the function.

```python
def nameAge(name, age):
    print("Hi, I am", name)
    print("My age is ", age)

nameAge("Prince", 20) # Correct output
nameAge(20, "Prince") # Incorrect output
```

> [!alert|no-title]
> The **order** of the arguments in the call must match the order of the parameters in the definition.
### keyword arguments
Functions can be *called* using keyword arguments with the syntax `kwarg=value`.
This will match `value` to the parameter named `kwarg`:

```python
def greet(name, greeting):
    print(f"{greeting}, {name}!")

greet(name="Alice", greeting="Hi")  # Keyword arguments
greet(greeting="Hi", name="Alice")  # Order doesn't matter
```

The **order of keyword arguments does not matter** because they are explicitly matched by name.
## Unpacking Function Arguments
The [[operators#Unpacking|unpacking asterisk operators]] `*` and `**` can be used in reverse for function calls:

- `*` unpacks an iterable (e.g. **list**, **tuple**, **range**) into [[#positional arguments]]
- `**` unpacks a **dict** into [[#keyword arguments]]

This allows us to "unpack" a collection into its elements so that it can be passed as individual parameters:

```python file="Unpacking Lists" hlt:*numbers
def sum_(a, b, c):
    return a + b + c

numbers = [1, 2, 3]

# same as sum_numbers(1, 2, 3)
print(sum(*numbers)) 
```

```python file="Unpacking Dictionaries" hlt:**person_info
def introduce(name, age, occupation):
    print(f"Name: {name}, Age: {age}, Occupation: {occupation}")

person_info = {'name': 'Alice', 'age': 30, 'occupation': 'Engineer'}

# same as introduce('name'='Alice', 'age'=30, 'occupation'='Engineer')
introduce(**person_info)  
```
