---
cssclasses:
  - table-array
---
## type
**A collection of values.** For example, the Boolean type consists of the values `True` and `False`.
### simple type, primitive type
**A data type that cannot be broken down into smaller types.** Examples include integers, booleans, characters.
### aggregate type, composite type
**A data type that consists of multiple subparts (i.e. combines multiple other data types or primitives).** Examples include arrays and lists (a collection of data elements). 
## data type
**A [[#type]] together with a collection of operations to manipulate the type.** For example, an integer variable is a member of the integer data type. Addition is an example of an operation on the integer data type.
## abstract data type
**The specification of a [[#data type]] within some language, independent of an implementation**.

An ADT is a <i class="default">high-level description of a data type</i> that defines what operations can be performed and what behavior is expected but does not specify how these are implemented or how data is stored.

For example, a Stack ADT supports operations like `push`, `pop`, and `peek` but does not specify how the data type is implemented (is it an array? a linked list?).

The [[#interface|interface]] of an ADT provides a concrete way for users to interact with the ADT. Users of the ADT only see and interact with the interface. The interface for the ADT is defined in terms of a [[#type]] and a set of operations on that type.

<u>Features</u>
- **Abstraction**: Users of the ADT only need to know *what* operations that can be performed on the data, and *not how* the data type is implemented. They do not need to know the implementation details. 
- **Encapsulation**: An ADT hides the internal details of the data structure (protects it from outside access) and provides a public [[#interface|interface]] for users to interact with. 
- **Independent from Implementation**: ADTs can be implemented using different data structures, such as arrays or linked lists, without affecting the functionality of the ADT.
## interface
An interface is a class-like structure that only contains method signatures and fields. It does not contain an implementation of the methods or any data members.

> [!info|outlined]
> The ADT **interface** defines the "**what**" — what operations are available and what should they do?
> 
> The ADT **implementation** defines the "**how**" — how the data is stored and how the operations are implemented/carried out.

For example, in C, the interface of an ADT is defined in a `.h` file that provides:
-  Function prototypes for all operations 
- An opaque view of a data structure — via the declaration of the data structure
- Semantics of operations via documentation (comments)
	- Comments provide documentation that explain what each function does, its input and output, and any conditions or constraints etc.

```c file='stack.h'
// stack.h
typedef struct Stack Stack;  // opaque struct type for the ADT

Stack* create_stack(int capacity);  
void push(Stack* stack, int item);
int pop(Stack* stack);
int is_empty(Stack* stack);
```

The user defines the internal structure of the data structure and implements the functions declared in the ADT interface:

```c file="stack.c"
// stack.c
#include "Stack.h"   // #include the interface

struct Stack {
    int* data;
    int top;
    int capacity;
};

// Implementing the StackPush function
void push(Stack stack, int value) {
  // Actual code here...
}
```

## data structure
**The implementation for an [[#abstract data type|ADT]]**. In an object-oriented language, an ADT and its implementation together make up a *class*. Each operation associated with the ADT is implemented by a [[#method, member function|member function or method]]. The variables that define the space required by a data item are referred to as [[#data member|data members]]. An *object* is an instance of a class, that is, something that is created and takes up storage during the execution of a computer program.

## wrapper
**A wrapper is a data structure that contains other data.** It "wraps", "encapsulates" or "hides" an existing class to provide a different interface or additional functionality.

For example, a Linked List is often represented by 2 structures: one for the usual list node, and one wrapper which contains a pointer to the head of the list (along with other data about the list such as its size).

> [!details]- More Details
> Often, a linked list will be represented by two structures, one for the usual list node, and one which contains a pointer to the head of the list (along with other data about the list such as its size), usually called a wrapper or container struct.
> 
> The `LinkedList` data structure serves as the **public interface** for manipulating a list of `Node` objects.
> 
> Because we have a struct that contains a pointer to the head of the list, we can add more fields to this struct. It gives us a place to provide methods for insertion, deletion etc, (along with other data about the list such as its size).
> 
> **Separation of Concerns**: 
> `struct list` handles the overall list.
> `struct node` handles individual elements.
> 
> > [!col]
> > ```python file="Linked List class in Python" ins:8-20
> > # Node class
> > class Node:
> >     def __init__(self, item):
> >         self.item = item
> >         self.next = None
> > 
> > # LinkedList class
> > class LinkedList:
> >     def __init__(self):
> >         self.head = None  # Pointer to the first node in the list
> > 
> > 	# Method to add a new node
> >     def add_node(self, data):
> >         ...
> >         
> > 	# Method to remove a node
> >     def remove_node(self, data):
> > 		...
> > ```
> > 
> > ```C file="Linked List struct in C" ins:8-12
> > // Node struct
> > struct node {
> >     int value;
> >     struct node *next;
> > };
> > 
> > // List struct
> > struct list {
> >     struct node *head;   // Pointer to the first node in the list
> >     struct node *tail;
> >     int size;
> > };
> > ```
> 

Wrappers are commonly used for several reasons:
1. **Abstraction**: They hide the complexity of the underlying implementation, allowing users to interact with a simpler interface.
2. **Encapsulation**: They "hide" or "encapsulate" underlying components.
3. **Separation of Concerns**: They provide a higher-level interface for managing data.
4. **Enhancement**: Wrappers allow you to add new features or behaviours to the original functionality without modifying the original code.
5. **Adaptation**: They can adapt an interface to be compatible with a different interface (often referred to as the Adapter pattern in design patterns).
## data member
The variables that together define the space required by a data item are referred to as data members. Some of the commonly used synonyms include data field, attribute, and instance variable.
## encapsulation
In programming, the concept of ==hiding implementation details== from the user of an ADT, and ==protecting data members of an object from outside access==.



## method, member function
Each operation associated with the ADT is implemented by a member function or method.
In OOP, a method is an operation on a class.





## resource constraints
Examples of resource constraints include the ==total space available== to store the data (possibly divided into separate main memory and disk space constraints) and the ==time allowed to perform each subtask==.

A solution is said to be *efficient* if it solves the problem within the required resource constraints.
## complexity
Algorithmic complexity is a rough sense of how much computing resources will be required for an algorithm to handle **input data of various sizes or values**, particularly in terms of time and space (memory or storage.)
## cost
The amount of resources (time or space) that the algorithm consumes.

## growth rate
The rate at which the [[#cost]] of the algorithm grows as the input size grows.

## asymptotic
For a function $f(n)$ the *asymptotic* behavior is the growth of $f(n)$ as $n$ gets large.
Small input values are not considered.

A good rule of thumb is: the slower the asymptotic growth rate, the better the algorithm.
## constant time
The cost of a function whose running time is not related to its input size. In Theta notation, this is traditionally written as O(1).
## best, worst, and average cases
The best, worst, or average cases each define a [[#cost|cost]] for a specific *input* instance of size $n$. They determine what we are measuring (the best, worst, or average case) the algorithm with, and from there we determine the [[#growth rate|growth rate]] of the cost measure.

For some algorithms, the cost depends on the **input size**. For others, the cost depends on the **distribution/order of inputs of the same size**.

e.g. For linear search, the best-case is when the key is the first element in the array (and worst-case is when the key is the last element). For binary search, the best-case is when the input is sorted.

Therefore, for a given input size $n$, the problem can behave differently depending on the case of inputs:

- **Worst case**: The worst-such input (out of the inputs of size $n$) that cause the algorithm to take the maximum possible time or resources (greatest cost).
	- ! Note that the worst case is **not** when the input size $n$ is big.
	- We are referring to the [[#problem instance|problem instance]] for a given input size $n$ which has the **greatest cost**.
- **Average case**: The average of all possible inputs.
- **Best case**: The best such input (most favorable input) where the algorithm takes the minimum possible time or resources (minimum cost).
	- ! Note that the best case is **not** when the input size $n$ is small.

## problem instance
A specific selection of values for the parameters to a problem. In other words, a specific set of inputs to a problem.
## problem -> algorithm -> program
### problem
A problem is a task to be performed. It is best thought of as a function[^1] or a mapping of inputs to outputs. In general, it is the desired input/output relationship.
### algorithm
An algorithm is a method or a process followed to solve a problem. It describes a procedure for achieving the input/output relationship.

An algorithm defines step-by-step instructions that are followed in a specific order to perform a specific task.

We typically use pseudocode (a plain language description) to write the steps in an algorith. For example:

```
linearSearch(A, key):
	Input: array A of n integers
	Output: index of key in A if it exists, otherwise -1

	for i from 0 up to n-1 do
		if A[i] = key then
			return i

	return -1
```

### program
A program is an instantiation of an algorithm in a programming language. A program *implements* an algorithm.


## record
An **item**, **element**, **object** that contains data (information). Many data structures are containers for a collection of records.

Formally, a record is data structure (also called a **struct**) that stores a collection of fields. Every field has an identifier (field name) and a data type.

In object-oriented programming languages, a record is typically implemented as an **object**, that contains state and method fields.

In C, a record is defined as a `struct` type, for example:

```C
public struct PlayerRecord {
    public string name;
	public int id;
	// other fields
}
```

## key
A **field**, **property** or part of a record that is used to represent the record when **searching** or **comparing**. The key can be the entire record itself if it is a value, or one or more fields if the record is a struct.

For example, in a collection of customer records, we want to search records by name. In this case, the name field is used as the **search key**.
### primary vs secondary key
In sorting, keys are classified based on their priority in determining the order:

- **Primary Key**: The main criterion used for sorting. Elements are ordered first based on this key.
- **Secondary Key**: Used to break ties when two elements have the same value for the primary key.

## exchange sorts
A sort that relies solely on **exchanges** (swaps of adjacent records) to reorder the list. [[Insertion Sort]] and [[Bubble Sort]] are examples of exchange sorts. All exchange sorts require $Θ(n^2)$ time in the worst case.
 
## inversions
An inversion in a sequence is a pair of elements that are out of order: `A[i] > A[j]`.
For example: (5, 3).

To count the number of inversions in a sequence, look at each value and count the number of times that a bigger value is to its left.

For example, this array has a total number of <u>5</u> inversions:

| 986 | 544 | 240 | 750 | 943 |
| --- | --- | --- | --- | --- |
| 0   | 1   | 2   | 3   | 4   |

## random access
Also referred to as **direct access**. The ability to access an element of a sequence directly (i.e. can skip directly to the desired element to retrieve it). For example, arrays allow direct access to any element in the array via indexing, whereas linked lists sacrifice direct access for efficient inserts, deletes and re-ordering of data. To access an arbitrary element of a linked list, we need to traverse the list starting from the head.

## sequential access
**Accessing data in a linear order, one after the other.** It's the opposite of random access, which allows data to be accessed in any order. 

## memory overhead
The extra memory required by a data structure beyond what is needed to store the actual data values. For example, linked lists have higher memory overhead than arrays because each node must store a pointer in addition to data.
## Footnotes
[^1]: A subroutine that takes input parameters and uses them to compute and return a value.