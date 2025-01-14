> [!quote] Everything in Python is an object
> In Python, all data is represented by objects. Everything you can assign to a variable is an object — including strings, numbers, functions and even classes and modules.
> - <b>All values are objects.</b>
> - **An object has a data type (its *class*).** 
> - <abbr data-title="Every class is a type. When you define a class, you create a new type. Objects created from the same class have the same type."><b>A <em>class</em> defines a <em>type</em>.</b></abbr>

> [!quote] Variables are names that point to an object
> A variable is simply a *name* that stores reference to an object's *location*. In contrast, objects are actual <i>data</i> stored in memory.
> 
> When we create a ==variable== of a ==certain type== ...
> We have actually created an ==object== that is an instance of a ==certain class== ...
> And have also created a name that points to the object.
> 
> When you assign a value to a variable, Python creates an object with that value, and you can then refer to the object by the variable name:
> 
> ```python
> x = [1, 2, 3]  # A list object is created in memory, and x points to it
> ```
> 
> This is why Python is dynamically typed — variables are not tied to a specific type.  They can reference any object, and their type is determined by the object they reference.

> [!quote] Every object has an identity, a type and a value.
> - **Identity**: An object’s address in memory. 
> 	- `is` operator compares the identity of 2 objects. 
> 	- [`id()`](https://docs.python.org/3/library/functions.html#id) returns an object’s identity.
> 
> - **Type**: The type of an object is which <i>class</i> an object derives from. Different types of objects have different built-in functions available to them. 
> 	- @ Use the built-in [`type()`](https://docs.python.org/3/library/functions.html#type) function to get an object’s type.
> 	- $ Type casting (setting the type) is done using constructor functions e.g. `int()`, `str()` 
> 
> - **Value:** The data the object contains/stores. 
> 	- Objects whose value can change are *mutable*. 
> 	- Objects whose value is unchangeable once they are created are called _immutable_. 

> [!quote] Python is an object-oriented programming language.
> - **Every data is an object.** Every piece of data is represented as an *object* of a specific *class* type. For example, strings are objects of the built-in `str` class. 
> - **Every class is a type.** The object's type is the <i>class</i> it derives from. The result of `type(obj)` is the class of the object. 
> - **An object is an <i>instance</i> of a class** with specific values for its attributes. An object's class is a blueprint that specifies the **data (attributes)** and **behaviour (methods)** of a particular object. 


## Objects in Python

> [!example]
>
> ```python
> >>> 300
> ```
>
> When presented with the statement `300`, Python:
>
> 1. Creates an integer object (which is an instance of the built-in `int` class)
> 2. Gives it a value of `300` 
>
> You can see that an integer object is created using the built-in [`type()`](https://realpython.com/python-built-in-functions/#creating-and-checking-types-type-isinstance-and-issubclass) function:
>
> ```python
> >>> type(300)
> <class 'int'>
> ```
## Variables in Python
Variables are simply symbolic _labels (names)_ that <i>point to</i> an object's memory address.

![|500](https://files.realpython.com/media/py_memory1.2b6e5f8e5bc9.png)

Once an object is assigned to a variable, you can refer to it by the variable’s name. 
But the data itself is contained within the object (and not in the variable).

> [!example] Variables hold references to objects.
> 
> ```python
> >>> n = 300
> ```
> 
> This variable assignment:
> 
> 1. Creates an integer object with a value of `300` 
> 2. Makes the variable `n` point to that object
> 
> 
> ![|centre|200](https://files.realpython.com/media/t.2d7bcb9afaaf.png)
> <i class="figcaption" id="centre">Variable Points to a Single Object</i>

