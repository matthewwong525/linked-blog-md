A class in Python is a user-defined template/blueprint for creating objects.
It allows us to encapsulate data and behaviour into a single entity.
Creating a new class creates a new *type* of object, and allows us to create objects, which are instances of the class.
## class definition 
To define a class, use the `class` keyword followed by the class name and a colon.
The class body will start at the next indentation level:

```python
class MyClass:
    def __init__(self, arg1, arg2):
        self.arg1 = arg1  
        self.arg2 = arg2
    
    def some_method(self):
        # Method definition
        pass
```

> [!info|no-title]
> **Note:** The recommended naming convention for Python classes is the `PascalCase`, where each word is capitalized.

> [!function|yellow] Special Methods
> - [`.__init__()`](https://docs.python.org/3/reference/datamodel.html#object.__init__ "object.__init__") is called automatically every time the class is instantiated.  
> - [`.__repr__()`](https://docs.python.org/3/reference/datamodel.html#object.__repr__) returns a **formal string representation** of the class object. You can access an object’s formal string representation using the built-in `repr()` function
> -  [`.__str__()`](https://docs.python.org/3/reference/datamodel.html#object.__str__) returns an **informal string representation** of the class object. You can access this string using either `str()` or `print()`.
> - The `self` parameter is a reference  to the current instance of the class. It allows us to access the attributes and methods of the object.
## class instantiation
To create an object from the class, we call the class constructor. The class constructor accepts the same arguments as the `.__init__()` method.

```
x = MyClass()
```
## class attributes
Attributes are variables defined inside the class and represent the properties of the class. They can be accessed using the dot `.` operator.

```python
# Define a class
class Dog:
    sound = "bark"     # class attribute

# Create an object from the class
dog1 = Dog()

# Access the class attribute
print(dog1.sound)
```

```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name} is {self.age} years old."  
      
dog1 = Dog("Buddy", 3)
dog2 = Dog("Charlie", 5)

print(dog1)   # Buddy is 3 years old.
print(dog2)   # Charlie is 5 years old.
```
### attributes
Classes can have two types of attributes:

1. **Class attributes:** A variable that you define in the class body directly. Class attributes belong to their containing class. Their data is common to the class and all its instances.

1. **Instance attributes:** A variable that you define inside an instance method using the `self` argument and dot notation, like in `self.attribute = value`. Instance attributes belong to a concrete instance of a given class. Their data is only available to that instance and defines its state.

```python
class ObjectCounter:
	num_instances = 0   # class attribute
	
	def __init__(self):
		ObjectCounter.num_instances += 1  # update the class attribute
```

```python
class Dog:
	# class attribute
    species = "Canine"  

    def __init__(self, name, age):
        # instance attributes
        self.name = name
        self.age = age

# Create objects
dog1 = Dog("Buddy", 3)
dog2 = Dog("Charlie", 5)

# Access class and instance variables
print(dog1.species)  # (Class variable)
print(dog1.name)     # (Instance variable)
print(dog2.name)     # (Instance variable)

# Modify instance variables
dog1.name = "Max"
print(dog1.name)     # (Updated instance variable)

# Modify class variable
Dog.species = "Feline"
print(dog1.species)  # (Updated class variable)
print(dog2.species)
```


### class methods
A class method is a method that takes the class object as its first argument instead of taking `self`. In this case, the argument should be called `cls`, which is also a strong convention in Python.

You can create class methods using the [`@classmethod`](https://docs.python.org/3/library/functions.html#classmethod) decorator.

```python
class ThreeDPoint:
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z

    @classmethod
    def from_sequence(cls, sequence):
        return cls(*sequence)
```

