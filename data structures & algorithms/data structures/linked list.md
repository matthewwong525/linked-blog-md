---
cssclasses:
  - banner-image
  - table-nowrap
  - table-header
aliases:
  - Linked List
---
>[!banner-image] ![Linked Lists](https://miro.medium.com/v2/resize:fit:1400/0*N0O2O3BctckgyNIG)
## Linked List
A linked list is a linear collection of elements called **nodes**.
- The first node is called the **head**.
- The last node has its `next` reference pointing to `None`.

![Graphical representation of a list](https://javascript.info/article/recursion/linked-list.svg)


A **node** has 2 different fields:
1. `data` contains the *value* in the node
2. `next` contains a reference to the *next node* in the list


Linked Lists are mostly used because of their effective insertion and deletion.  We only need to change few pointers (or references) to insert (or delete) an item in the middle.
## Types of Linked Lists
There are four basic forms of linked lists:

1. **Singly Linked List**: Each node points to the next node in the sequence.
2. **Doubly Linked Lis**t: Each node points to both the next and previous nodes.
3. **Circular Linked List**: Last node points back to the first node, forming a circle.
4. **Sorted Linked Lis**t: Elements are stored in a sorted order based on a specific criterion.

***
**Singly Linked Lists**
A singly linked list is the simplest type of linked list.
![A singly linked list.](https://www.w3schools.com/dsa/img_linkedlists_singly.svg)
- Each node has 1 reference to the next node in the list ⇒ Takes up less memory.
- The list can only be traversed in one direction — from the head to the tail.
- Cannot iterate back to the previous node if required.
***

**Doubly Linked Lists**
A doubly linked list has nodes with references to both the previous and the next node.

![A doubly linked list.](https://www.w3schools.com/dsa/img_linkedlists_doubly.svg)

- Each node has 2 references: `next` and `prev` ⇒ Takes up more memory.
- Bidirectional traversal: the list can be traversed both up and down.

***
**Circular Linked Lists**
A circular linked list has the head and tail connected, creating a circular list structure.

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
![A circular singly linked list.](https://www.w3schools.com/dsa/img_linkedlists_circsingly.svg)
<i class="figcaption" id="centre" style="width:200px">A circular singly linked list.</i>
`````

`````col-md
flexGrow=1
===
![A circular doubly linked list.](https://www.w3schools.com/dsa/img_linkedlists_circdoubly.svg)
<i class="figcaption" id="centre" style="width:200px">A circular doubly linked list.</i>
`````
``````

- Can be singly or doubly linked. Nodes can contain 1 or 2 pointers.
- Cyclic traversal: the list can be cycled through continuously (i.e. loop back from the last item to the first)
- More complex code is needed to explicitly check for start and end nodes (in singly or doubly linked lists, we can find the start and end of a list by just checking if the links are null).
***

## Doubly Linked Lists
Doubly linked lists are different from singly linked lists in that they have two references — `previous` and `next`:
> [!col]
>
> ```python hlt:4-5,10-11
> class Node:
>     def __init__(self, value):
>         self.value = value
>         self.next = None
>         self.prev = None
> 
> 
> class DoublyLinkedList:
>     def __init__(self):
>         self.head = None
>         self.tail = None
>         self.length = 0
> ```
>
> ![Example Node of a Doubly Linked List](https://files.realpython.com/media/Group_23.a9df781f6087.png)
> <i class="figcaption" id="centre" style="width:200px">Node (Doubly Linked List).</i>

- Traverse the list in both directions.
- Use `next` to go forward and `previous` to go backward
## Circular Linked Lists
Circular linked lists are a type of linked list in which the last node points back to the `head` of the list instead of pointing to `None`.

- Traverse the entire list starting at any node.
- Used for implementing a [Fibonacci heap](https://en.wikipedia.org/wiki/Fibonacci_heap)

> [!important|no-title]
> **IMPORTANT**: Not all cyclic lists are entirely cyclic (where every node loops back to the start). They can also come in forms where only one part of the list is cyclic, and the rest is linear.

## Implementation

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
```python
class LinkedList:
    def __init__(self):
        self.head = None  
```
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
```
`````

`````col-md
flexGrow=1
===
The linked list class stores the **head** of the list. It is a [[data structures & algorithms/appendix/glossary#wrapper|wrapper class]] that will encapsulate all the operations for managing the nodes.

The node class stores **data** and a **reference** to the next node.
`````
``````

> [!code|red]- Adding a LinkedList iterator
> Implement an `__iter__` method in the `LinkedList` class to make it [[python/glossary/glossary#iterable|iterable]] .
> ```python
> def __iter__(self):
>     node = self.head
>     while node is not None:
>         yield node
>         node = node.next
> ```
> This means we can iterate over the linked list directly using Python's [[loops#for|for]] loop, and also use other constructs such as list comprehensions and functions like `map()` and `zip()`.
>
>
> ```python
> for node in linked_list:
> 	print(node.data)
> ```
> > [!tip]
> > The `for` loop stops (exits) with the loop variable pointing to the last node.
> > This lets us access the last node easily like this:
> >
> > ```python
> > for current_node in linked_list:
> > 	pass
> > 
> > # access the last node `current_node`
> > current_node->next = new_tail
> > ```

^2d86df

> [!code]- Modifying the linked list’s constructor
> We can also modify the linked list’s `__init__()` to quickly create linked lists with some data:
>
> ```python
> class LinkedList:
>     def __init__(self, nodes=None):
>         self.head = None
>         if nodes is not None:
>             node = Node(data=nodes.pop(0))
>             self.head = node
>             for elem in nodes:
>                 node.next = Node(data=elem)
>                 node = node.next
> ```
>
> For example:
> ```python
> list = LinkedList(nodes=[1, 2, 3, 4])
> ```

> [!code]- Adding a string representation
> You can add a `__repr__` to both classes to have a more helpful representation of the objects:
>
> ```python
> class Node:
>     def __init__(self, data):
>         self.data = data
>         self.next = None
> 
>     def __repr__(self):
>         return self.data
> 
> class LinkedList:
>     def __init__(self):
>         self.head = None
> 
>     def __repr__(self):
>         node = self.head
>         nodes = []
>         while node is not None:
>             nodes.append(str(node.data))
>             node = node.next
>         nodes.append("None")
>         return " -> ".join(nodes)
> ```
## Operations

### Pretty Print Linked List
In Python, we can add a `__repr__` to both `LinkedList` and `Node` classes to have a **formal string representation** of the objects:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

    def __repr__(self):
        return self.data


class LinkedList:
    def __init__(self):
        self.head = None

    def __repr__(self):
        node = self.head
        nodes = []
        while node is not None:
            nodes.append(str(node.data)) # convert data to string
            node = node.next
        nodes.append("None")
        return " -> ".join(nodes)
```

```output
1 -> 2 -> None
```

Or alternatively, we can add a `__str__` instead which is what `print()` will call by default:

```python
class LinkedList:
    def __init__(self, head=None):
        self.head = head
 
    def __str__(self):
        # defining a blank res variable
        res = ""
         
        # initializing ptr to head
        ptr = self.head
         
       # traversing and adding it to res
        while ptr:
            res += str(ptr.val) + ", "
            ptr = ptr.next
 
       # removing trailing commas
        res = res.strip(", ")
         
        # chen checking if 
        # anything is present in res or not
        if len(res):
            return "[" + res + "]"
        else:
            return "[]"

```

```output
[1, 2, 3]
```

### Traversal
> [!attention|no-title]
> **Number of `next` pointers that are None = Position from the *back* of the list**
>
> - `current.next = None` means current is the **last** node
> - `current.next.next = None` means current is the **2nd-last** node
> - `current.next.next.next = None` means current is the **3rd-last** node
#### Iterate the entire list

```python file="Iterate the entire list"
current = self.head
while current is not None:
	current = current.next

# current is None (after loop)
```

#### Iterate to the last node

```python file="Iterate to the last node"
current = self.head
while current.next is not None:
	current = current.next

# current is the last node
```

#### Iterate to the 2nd last node

```python file="Iterate to the second-last node"
if self.head is None:
	return
	
current = self.head
while current.next != None and current.next.next != None:
	current = current.next
	
# current is the second last node
```

### Length/Size
Return the size (i.e total number of elements) of the list.

```python file="Iterative Solution"
def get_length(self):
	count = 0
	current = self.head
	while current is not None:
		count += 1
		current = current.next
		
	return count
```

```python file='Recursive Solution'
def get_length(self):
	def get_length_helper(node, count):
		if node is None:
			return count
		else:
			return get_length_helper(node.next, count + 1)
			
	return get_length_helper(self.head, 0)
```

### Node Insertion
#### Insert between 2 nodes

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
Insert *before* a given node:

``` py
prev.next = new
new.next = current
```
1. Link `previous` to `new`
2. Link `new` to `current` 

<i class="default">Need reference to 2 nodes here</i>
`````

`````col-md
flexGrow=1
===
Insert *after* a given node:

``` py
new.next = current.next
current.next = new
```
1. Link `new` to `current.next`
2. Link `current` to `new`

<i class="default">Only need 1 reference for this</i>
`````
``````

Insert *at* a specified index:

> [!list-ol|purple] Insert a node at index `n`
> 1. Traverse to the node *before the point of insertion* at index `n-1`.
> 2. Insert the node *after* the node at `n-1`:
> 	1. Link the new node to the next node
> 	 2. Link the previous node to the new node
>
> ![[linked-list-insertion-before-node.drawio.png|Insert a node at index n]]

^1a0b7b

> [!warning|red]-
><br/>
>
> ``````col
> borderWidth=0
> textAlign=start
> ===
> `````col-md
> flexGrow=1
> ===
> Do this:
> ```python
> new.next = current.next   
> current.next = new
> ```
> 1. Update `new.next` to `current.next`
> 2. Then update `current.next` to `new`
> `````
> 
> `````col-md
> flexGrow=1
> ===
> Not this:
> ``` py
> current.next = new        
> new.next = current.next  
> ```
> 1. `current.next` points to `new`
> 2. `new.next` points to `current.next` which is actually itself
> `````
> ``````
>
> ![[linked-list-insert-between.png|Inserting a new node after current node.|400]]

#### Insert at the head

```python
def insert_head(self, node):
    node.next = self.head
    self.head = node
```

1. Update the next pointer of the node to point at the head.
2. Update the head node to new node.

> [!info|blue]- No need to check if the list is empty.
> If `head == None` then `node.next` will simply point to `None`.
>
> ```python
> def insert_head(self, data):
> 	new_node = Node(data)
> 	
> 	if self.head is None:
> 		self.head = new_node
> 		return
>     else:
> 		new_node.next = self.head
> 		self.head = new_node
> ```

#### Insert at the tail

```python
def insert_tail(self, data):
    new_node = Node(data)
    
    # empty list: return new node as head
    if self.head is None:
        self.head = new_node
        return
        
    # non-empty list: traverse to the last node
    current_node = self.head
    while current_node.next is not None:
        current_node = current_node.next
        
    current_node.next = new_node
```

> [!alert|no-title]
> **Recall**: the last node has its `next` reference pointing to `None`.

1. Traverse to the last node.
2. Update its next pointer to point to the node.

> [!example]- Alternative Method with LinkedList Iterators
> Alternatively, if you have implemented the `__iter__` method in the `LinkedList` class like [[#^2d86df|this]] , you can traverse the linked list like this:
>
> ```python
> def add_last(self, node):
>     if self.head is None:
>         self.head = node
>         return
>         
>     for current_node in self:
>         pass
>         
>     current_node.next = node
> ```
>
> - The `for` loop iterates the whole list until it reaches the last node (it stops with `current_node` pointing to the last node)
> - After the loop, `current_node` points to the last node. Update its next pointer.

#### Insert at a given position
> [!danger] Edge Cases
> 1. **Empty List** or **Position= 0** (insert at head)
> 2. **Position is out of bounds** (negative or greater than the list length)

> [!1|black] Method 1: Find the node *before* the point of insertion at index `n-1`
>
> ```python
> def insert_at_index(self, data, index):
>     new_node = Node(data)
>     
>     # Insert as head
>     if (index <= 0) or (self.head is None):
>         new_node.next = self.head
>         self.head = new_node
>         return
>         
>     # Find the node before point of insertion (index - 1)
>     position = 0
>     current_node = self.head
>     while current_node is not None and position != index - 1:
>         current_node = current_node.next
>         position += 1
>         
>     # Insert node after the `current_node`
>     if current_node is not None:
>         new_node.next = current_node.next
>         current_node.next = new_node
>     else:
>         print("Index not present")
> ```
>
> When we exit the loop:
> - `current` is the node BEFORE point of insertion
> - `current.next` points to the node AT point of insertion
>
>  See [[#^1a0b7b|here]] for more details.


> [!2|black] Method 2: Find both the node *before* and the node *at* the point of insertion.
>
> ```python
> def insert_at_index(self, data, index):
>     new_node = Node(data)
>     
>     position = 0
>     previous = None         # node before point of insertion (index - 1)
>     current = self.head     # node at point of insertion (index)
>     while current and position != index:
>         previous = current
>         current = current.next
>         
>     if previous is None:
>         # insert as head
>         new_node.next = self.head
>         self.head = new_node
>     else:
>         # insert b/w previous and current
>         previous.next = new_node
>         new_node.next = current
> ```
>
> When we exit the loop, there are 2 cases to consider:
> - `previous is None`: Loop not entered
> 	- Either the list is empty i.e. `current is None`
> 	- Or **index = 0**
> -  `current is None`: Loop entered
> 	- index is not present in the list
> 	- either way, we insert the node as the tail in this example
#### Insert as the 2nd last node

```python
def insert_second_last(self, data):
	new_node = Node(data)
	current = self.head
	
	# Insert as head
	if current is None:
		self.head = new_node
		return
		
	# Traverse to the second-last node
	while current.next and current.next.next:
		current = current.next
		
	# Insert node after the second-last node
	new_node.next = current.next
	current.next = new_node
```

> [!alert|no-title]
> **Note:** The second-last node is the node before the last node. Therefore, we want to insert the node before the last node = after the second-last node.

> [!example]- Another Method
>
> ```python
> def insert_second_last_again(self, data):
>         new_node = Node(data)
>         list_length = self.get_length()
>         
>         # Insert as head
>         if (self.head is None) or (list_length == 1):
>             new_node.next = self.head
>             self.head = new_node
>             
>         # Traverse to index list_length-2
>         p = self.head
>         i = 0
>         while (p.next is not None) and (i < list_length - 2):
>             p = p.next
>             i += 1
>             
>         # Insert node after the second-last node
>         new_node.next = p.next
>         p.next = new_node
> ```

### Node Deletion
> Unlink the node to delete by removing all references pointing to it.


Deleting the First Node

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
```python
self.head = self.head.next
```
`````

`````col-md
flexGrow=1
===
![[linked-list-delete-head.png|Deletion at the start.]]
`````
``````

Deleting the Last Node

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
```python
# current is the last node
current.next = None
```
`````

`````col-md
flexGrow=1
===
![[linked-list-delete-tail.png|Deletion at the end.]]
`````
``````

Deleting the Middle Node

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
```python
# current is the node before
current.next = current.next.next
```
```python
# or alternatively
previous.next = current.next;
```
`````

`````col-md
flexGrow=1
===
![[linked-list-delete-middle.png|Deletion in the middle.]]
<i class="default">Removing a node in the middle requires updating the previous node to point to the next node.</i>
`````
``````

> [!info|gray]- more info
> **Removing a node requires removing all references that point to it**, making the original node no longer accessible in the linked list. However, it still exists in memory. Python uses **automatic garbage collection**, so once the original node has no references pointing to it, it becomes eligible for garbage collection.
#### Delete the head
Remove the first node by making the second node the new head.

```python
def delete_first(self):
	if self.head is None:
		return
		
	self.head = self.head.next
```

`self.head` is updated to `self.head.next`, removing the reference to the original head.
#### Delete the tail
Remove the last node by traversing to the second last node, and pointing it to `None`.

```python
def delete_last(self):
    if self.head is None:
        return
        
    current = self.head
    while (current.next != None and current.next.next != None):
        current = current.next
        
    current.next = None
```

#### Delete a node at a given position
> [!danger] Edge Cases
> 1. **List is empty.**
> 2. **Index = 0**. Trying to access the previous node at `index - 1` won't work.
> 3. **Index is out of bounds**. Node to delete is not found.

```python
def delete_at_index(self, index):
	# empty list
	if self.head is None:
		return
		
	# delete head
	if index == 0:
		self.delete_first()
		return

	# traverse to the previous node at index - 1
	i = 0
	current = self.head
	while current and i < index - 1:
		current = current.next
		i += 1
		
	if current is None or current.next is None:
		# out of bounds index
		print("index not found")
	else:
		# delete middle/last node
		current.next = current.next.next
```

The loop continues until *current* is *None* or position reaches *index – 1*.
- If index is the last node, index-1 is the 2nd last node so `current.next != None`.
- Thus, if either `current == None` OR `current.next == None`, then the index is out of bounds.
#### Delete a node of a given data
> [!danger] Edge Cases
> 1. List is empty.
> 2. Node to delete is the head.
> 3. Node to delete is not found.

> [!1|black] Method 1: Find the previous node
>
> ```python
> def delete_node(self, data):
> 	current = self.head
> 	
> 	# check if head contains the data
> 	if current.data == data:
> 		self.delete_first()
> 		return
> 		
> 	# traverse to the node before 
> 	while current is not None and current.next.data != data:
> 		current = current.next
> 		
> 	if current is None:
> 		return
> 	else:
> 		current.next = current.next.next
> ```

> [!1|black] Method 2: Find both the previous node AND the node with data
>
> ```python
> def delete_contains(self, data):
> 	if self.head is None:  
> 		# empty list
> 		return 
>         
> 	previous = None
> 	current = self.head
> 	
> 	while current and current.data != data:
> 		previous = current
> 		current = current.next
> 		
> 	if current is None:
> 		# data not found
> 		print("Data not found")
> 	elif previous is None:
> 		# delete head node
> 		self.head = current.next
> 	else:
> 		# delete middle/last node
> 		previous.next = current.next
> ```
#### Delete the 2nd last node

```python
def delete_second_last(self):
	# List has 0 or 1 node
	if self.head is None or self.head.next is None:
		return
		
	# List has 2 nodes: delete head
	if self.head.next.next is None:
		self.head = self.head.next
		return
		
	# Traverse to the third-last node
	current = self.head
	while current.next.next.next != None:
		current = current.next
		
	# Remove the second-last node
	current.next = current.next.next
```

### Multiple Node Deletion
The approach is to traverse the entire list, while maintaining pointers to the current (and/or previous node). Inside the loop, we check if the current node is the node to delete. If so, we update the pointers. 

> [!caution]
> **The updating/moving of pointers to one step forward is (usually) different when a node is deleted vs when it isn't.**
> 
> After deleting a node, we need to <i class="default">carefully</i> update all `current` and/or `previous` pointers to their correct location in the <i class="default">now modified</i> list to avoid skipping nodes or causing infinite loops.
#### Delete all occurrences of a given key
Note that **after deleting the current node, we do NOT move the previous node forward to the current node** since the previous node <i class="default">after</i> deleting the current node is <i class="default">also</i> the previous node for the next node (since current is now removed).

```python
def delete_occurrences(head, key):
    # Initialize pointers to traverse the linked list
    curr = head
    prev = None
    
    # Traverse the list to delete all occurrences
    while curr is not None:
    
        # If current node's data is equal to key
        if curr.data == key:

            # If node to be deleted is head node
            if prev is None:
                head = curr.next
            # Delete the node
            else:
                prev.next = curr.next
                
            # Move to the next node 
            curr = curr.next

        else:
            # Move pointers one position ahead
            prev = curr
            curr = curr.next

    return head
```



## Performance Comparison
### Arrays vs Linked Lists
![linked_vs_array.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1637603328903/E1PjE0gz9.jpeg?auto=compress,format&format=webp)

|                        | Linked List                                    | Array                                   |
| ---------------------- | ---------------------------------------------- | --------------------------------------- |
| **Data Structure**     | Non-contiguous                                 | Contiguous                              |
| **Memory Allocation**  | Dynamically allocated one by one to each node  | Statically allocated to the whole array |
| **Insertion/Deletion** | Efficient                                      | Inefficient                             |
| **Access**             | Sequential                                     | Random                                  |
| **Memory Overhead**    | High. Each node contains both data + pointers. | Low. Each node only contains data.      |
| **Size**               | Dynamic size; No resizing needed               | Fixed size; Resizing required if full   |


| Operation                           | Linked List                                             | Array                                         |
| ----------------------------------- | ------------------------------------------------------- | --------------------------------------------- |
| Random Access (via index)           | <mark class="red">O(n)</mark> due to traversal          | ==O(1)==                                      |
| Lookup or Search (via value)        | O(n)                                                    | O(n)                                          |
| Insertion/Deletion at the **start** | ==O(1)==                                                | <mark class="red">O(n)</mark> due to shifting |
| Insertion/Deletion at the **end**   | <mark class="red">O(n)</mark>  if we maintain only head | O(1) if not at full capacity                  |
| Insertion/Deletion at **random**    | O(n) due to traversal                                   | O(n)                                          |

> [!pros] Advantages of Linked List over Arrays
> - **Dynamic size/No Resizing**: Linked lists are dynamic and flexible and can expand and shrink their size. Arrays are fixed-length so they incur **O(n)** memory movement costs for all insert/remove operations which change both the **size** and **position** of the data representation.
> - **Efficient Insertion/Deletion:** Insertion and deletion at any point in a linked list take O(1) time. Whereas in an array, insertion / deletion in the middle takes O(n) time.
> - **Better Use of Memory/No Wasted Memory:** From a memory allocation point of view, linked lists are more efficient than arrays. Unlike arrays, the size for a linked list is not pre-defined, allowing the linked list to increase or decrease in size as the program runs.
> - **More Space Efficient**: ==In cases where the total number of elements is unknown in advance==, linked lists are more space efficient compared to arrays. In arrays, the whole memory of items is allocated together. Even with dynamic-sized arrays like [[data types#List `[ ]`|list]] in Python or ArrayList in Java, the internal workings involves de-allocation of whole memory and allocation of a bigger chunk when insertions happen beyond the current capacity.
> - **Implementation of Queue and Deque**: Linked lists are a common choice for implementing queues and dequeues because of its dynamic memory management and efficient O(1) insertion/removal. In contrast, array implementation is not efficient at all. We must use circular array to efficiently implement which is complex.

> [!cons] Disadvantages of Linked List over Arrays
> - **No Random Access**: If the array is sorted we can apply binary search to search any element which takes O(log(n)) time. But even if the linked list is sorted we cannot apply binary search (which requires direct access to an element given an index) and the complexity of searching elements in the linked list is O(n).
> - **Slow Access Time**: Accessing elements in a linked list can be slow, as you need to traverse the linked list to find the element you are looking for, which is an O(n) operation. This makes linked lists a poor choice for situations where you need to access elements quickly.
> - **Higher overhead**: Linked lists have a higher overhead compared to arrays, as each node in a linked list requires extra memory to store the reference to the next node.
> - **Cache Inefficiency**: Linked lists are cache-inefficient because the memory is not contiguous. This means that when you traverse a linked list, you are not likely to get the data you need in the cache, leading to cache misses and slow performance.

> [!question|teal] When should you use a linked list over an array?
> 1. You don't know how many items will be in the list
> 2. You don't need random access to an element at a particular index.
> 3. You want to be able to insert items in the middle of the list.
> 4. You need constant time insertion/deletion (unlike an array, you don't need to shift every other item in a list first).
> 5. You need to frequently insert and delete many elements.
### Lists vs Linked Lists
In Python, lists are [dynamic arrays](https://docs.python.org/3.7/faq/design.html#how-are-lists-implemented-in-cpython), means that the memory usage of both lists and linked lists is very similar. Read this article on [how lists are implemented in Python](http://www.laurentluce.com/posts/python-list-implementation/).

<u>Insertion and Deletion</u>
In Python, you can insert or remove elements in a list using these methods:
- Use `.insert()` and `.remove()` to insert or remove at a **specific position** in a list.
- Use `.append()` and `.pop()` to insert or remove elements at the **end** of a list.

Inserting elements at the end of a list using `.append()` or `.insert()` will have constant time `O(1)`. Inserting or removing elements that are *not* at the end of the list requires some element shifting in the background, making the operation more complex in terms of time spent: `O(n)`.

Linked lists have constant O(1) insertion and deletion of elements at the beginning or end of the list.

For this reason, <mark class="green">linked lists have a performance advantage over normal lists when implementing a queue (FIFO)</mark>, in which elements are continuously inserted and removed at the beginning of the list. <mark class="red">But they perform similarly to a list when implementing a stack (LIFO)</mark>, in which elements are inserted and removed at the end of the list.

<u>Element Lookup</u>
Lists perform better than linked lists in [[data structures & algorithms/appendix/glossary#random access|random access]] (direct access to an element).

When you know which element you want to access, lists can perform this operation in `O(1)` time. Trying to do the same with a linked list would take `O(n)` because you need to traverse the whole list to find the element.

<u>Element Search</u>
When searching for a specific element, however, both lists and linked lists perform very similarly, with a time complexity of `O(n)`. In both cases, you need to iterate through the entire list to find the element you’re looking for.

## Applications
Linked lists can be used to implement [[queues]], [[stacks]] and [[graphs]].

Queues and stacks differ only in the way elements are retrieved:
- For a queue, you use a FIFO approach: insert at the rear, retrieve from the front.
- For a stack, you use a LIFO approach: insert at the rear, retrieve from the rear (top).

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
![|300](https://files.realpython.com/media/Group_6_3.67b18836f065.png)
<i class="figcaption" id="center" style="width:200px">Queue.</i>

`````

`````col-md
flexGrow=1
===
![Example Structure of a Stack|200](https://files.realpython.com/media/Group_7_5.930e25fcf2a0.png)
<i class="figcaption" id="center" style="width:200px">Stack.</i>
`````
``````

Because of the way you insert and retrieve elements from the **edges** of queues and stack, linked lists are convenient with O(1) insertion and deletion of elements at the **beginning or end** of a list.

Graphs can be implemented with an **adjacency list**. An adjacency list is a list of linked lists where each vertex of the graph is stored alongside a collection of connected vertices.


