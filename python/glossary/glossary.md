## dynamically typed
Python is a *dynamically typed* language, as opposed to a statically typed one. This means:
- The **variable type is determined by the data assigned to it at runtime**.
- We do NOT have to explicitly declare variables with a particular type.
- You can assign any type of value to a variable.

In a **dynamically typed language** (JavaScript, Python) variables' types are *dynamic*, meaning after you set a variable to a type, you CAN change it. That is because typing is associated with the value it assumes rather than the variable itself.

For example in Python:

```python
some_str = "Hello"  # variable some_str is linked to a string value
some_str = 5        # now it is linked to an integer value; perfectly OK
```

Type-checking is done at runtime, *during* execution. This allows for greater flexibility—can assign anything to a variable, and the type can change during execution. However, without compile-time checks, any type errors will only appear during execution.


In a **statically typed language** variables' types are *static*, meaning once you set a variable to a type, you cannot change it. That is because typing is associated with the variable rather than the value it refers to. Type-checking is done at compile time, *before* execution. The early detection of type errors saves us from spending time on debugging. However, it requires you to explicitly declare variable types.

For example in Java:

```java
String str = "Hello";  // variable str statically typed as string
str = 5;               // would throw an error since str is
                       // supposed to be a string only
```

## interpreted
Python is an *interpreted* language, as opposed to a compiled one. This means that **source files can be run directly** without the explicitly creating an executable which is then run.

This **reduces the edit-test-debug cycle** because there's **no compilation step required**.

In an interpreted language, the source code can be executed directly without compiling it into machine instructions. The source code is executed line-by-line by an **interpreter** without pre-compilation step.

In a compiled language, the source code is converted into machine code by a **compiler** before execution.
## heterogeneous
**Heterogeneous collections can store elements of any data type**. In contrast, homogeneous collections can only store elements of 1 data type.
## hashable
An object is <i>hashable</i> if has a hash value that is **immutable** (does not change).
Hashable objects can be used as ==dictionary keys== and ==set members==.

**Mutable objects like `lists`, `sets` or `dictionaries` are not hashable.** This is because their values change during their lifetime.

**Most immutable objects such as `numbers` and `strings` are hashable.**

> [!alert]
> Immutable containers like `tuples` are *only* hashable if *their elements are hashable*. <b>Tuples that contain only strings, numbers or tuples are hashable.</b>
## mutable
**Mutable objects can change their value in place[^1]** i.e. the contents can be changed.

Mutable objects are *not hashable* and *cannot be used for dictionary keys* or as an *element of set*.

For example, lists can be modified in place using index assignments, slice assignments, or methods like `append()` and `extend()`.

Mutable Built-in Data Types in Python
- Lists
- Dictionaries
- Sets
## immutable
**An object with a fixed value.** Immutable objects include `numbers`, `strings` and `tuples`. An immutable object cannot be changed after it is created.

i.e. We cannot add, remove or change items in an immutable collection.

Immutable Built-in Data Types in Python
- Numbers (`int`, `float`)
- Booleans (`bool`)
- Strings (`str`)
- Bytes
- Tuples (`tuple`)
## ordered collection
**A collection is *ordered* if you can retrieve its elements in *insertion order*.** An ordered collection preserves insertion-order. Items are stored in the order they are added. This order will not change. If you add new items, it will be placed at the end.

This means if you iterate through the elements of a `list`, `tuple` or `str`, you are iterating over the exact order that the elements are stored in the collection.
> [!note|outlined]
> Collections with the *same items* but in *different order* are still EQUAL (i.e. `[1, 2, 3] == [3, 1, 2]` is true).
## unordered collection
**A collection is *unordered* if it does not store elements in order of insertion**. Unordered collection do not record element position or order of insertion. They do not store items in a defined or specific order.

This means if you iterate through the elements of a `dict` or `set`, you are not guaranteed to get the elements in a particular order.
## iterable
**An object capable of returning its members one at a time.** An iterable is a collection of elements that you can loop/iterate through one element at a time. For example:

- `str`, `list`, `tuple`, `range` (all sequences)
- `dict`  
- `set`
- `file`
- Iterables can be used in a `for` loop and in many other places where a sequence is needed (`zip()`, `map()`, …).
- When an iterable object is passed as an argument to the built-in function `iter()`, it returns an <i>iterator</i> for the object. This iterator is good for one pass over the set of values.
- When using iterables, it is usually not necessary to call `iter()` or deal with iterator objects yourself. The `for` statement does that automatically for you, creating a temporary unnamed variable to hold the iterator for the duration of the loop.
## REPL
REPL stands for *read-eval-print loop*. It is another name for the **interactive interpreter shell**.

REPL is a **command line shell** which allows you to type in commands and see the results immediately.

> [!NOTE|no-title]
> **Note:** interactive shell, interactive session, REPL session are all used interchangeably.

Python has an **interactive interpreter** which means you can enter commands at the interpreter prompt, immediately execute them and see their results.

To use the REPL, type `python3` in your console. You'll get a prompt similar to the below output, which then waits for you to input commands:

```
Python 3.9.14 (main, Oct 29 2022, 22:18:10) 
[GCC 11.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

With the REPL, you can do most things you would be able to do in a code file. For example:

- **Run and evaluate statements**. You can have the REPL evaluate a statement like so:

    ```python
    >>> 1+1
    2
    >>>
    ```

- **Declare variables and functions**. You can also create variables and functions, and REPL will remember that they exist, should you try to use them later:

    ```python
    >>> PI = 3.14
    >>> PI
    3.14
    ```

- **Use the built-in help**. You can start interactive help by calling `help()` with no arguments.

## expression
An expression is a piece of code that **produces a value** when evaluated. It *always* returns a value.

- [[assignment expression]]
- [[conditional expression]]
- Expression list
- Lambda
- Operators & their operand(s)
## statement
A statement is a complete unit of execution that **performs an action**.

**Simple statements** are a single-line instruction that performs a specific action.

- [[pass]]
- [`del`](https://docs.python.org/3/reference/simple_stmts.html#the-del-statement)
- [`return`](https://docs.python.org/3/reference/simple_stmts.html#the-return-statement)
- [[loops#break / continue|break]]
- [[loops#break / continue|continue]]

**Compound statements** consists of one or more 'clauses': a header and a suite (body). The clause header starts with a keyword and ends with a colon `:`. A suite is a group of statements controlled by a clause.

- [[conditionals#if|if]]
- [[loops#while|while]]
- [[loops#for|for]]
- [[conditionals#match / case|match]]
## Footnotes
***
[^1]: In place means that the object is **modified directly** without creating a new object in memory.