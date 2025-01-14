---
difficulty: Easy
status: Redo
topics:
  - "[[linked list|Linked List]]"
  - "[[recursion|Recursion]]"
---
## Task
Given a sorted linked list and a value to insert, implement the following function `list_insert_ordered()` to insert the value in a sorted way:

```python
class Node:
    def __init__(self, data):
        self.data = data 
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
        
	def list_insert_ordered(self, value):
		# TODO
```

This function takes a linked list which is sorted in *increasing order* and inserts the given value into the list such that the list remains ordered. The function should be able to insert duplicates.

Implement this function in 2 ways:
1. Use *iteration* to insert the given value into an ordered linked list.
2. Use *recursion* to insert the given value into an ordered linked list.

``` file='Example Usage'
$ ./listInsertOrdered
Enter list size: 4
Enter list values (must be in ascending order): 2 5 7 8
List: [2, 5, 7, 8]
Enter value to insert: 6
List after inserting 6: [2, 5, 6, 7, 8]

$ ./listInsertOrdered
Enter list size: 5
Enter list values (must be in ascending order): -8 -3 -1 2 4
List: [-8, -3, -1, 2, 4]
Enter value to insert: -9
List after inserting -9: [-9, -8, -3, -1, 2, 4]

$ ./listInsertOrdered
Enter list size: 6
Enter list values (must be in ascending order): -5 0 2 6 9 14
List: [-5, 0, 2, 6, 9, 14]
Enter value to insert: 2
List after inserting 2: [-5, 0, 2, 2, 6, 9, 14]
```

> [!hint]-
> **Base case:**
> - Where should the value be inserted if the list is empty?
> - In what circumstances should you insert the value at the beginning of the list? Be careful - you need to make sure the new node is connected to the rest of the list.
>
> **Recursive case:**
> - After inserting into the rest of the list recursively, make sure to assign the result to the current node's `next` field.
## My Solutions
```python
def list_insert_ordered(self, value):
        new_node = Node(value)
        
        # Find the first value that is > value
        current = self.head
        previous = None
        while current is not None and current.value <= value:
            previous = current
            current = current.next
            
        # current is > value
        # insert the new node before current
        
        if previous is None:
            # current is the head node
            new_node.next = current
            self.head = new_node
        else:
            previous.next = new_node
            new_node.next = current
```

## Sample Solutions
### Recursive Approach

```python
def list_insert_ordered(self, value):
	def do_list_insert_ordered(head, value):
		"""
		Insert the given value into the list in a sorted way
		Return the head of the updated list
		"""
		if (head is None) or (value <= head.value):
			new_node = Node(value)
			new_node.next = head
			return new_node
		else:
			head.next = do_list_insert_ordered(head.next, value)
			return head
			
	self.head = do_list_insert_ordered(self.head, value)
```

> [!function|gray]- Algorithm
> <u>Base Cases</u>
> 1. If the list is empty, we reached the end. Return the new node as the head.
> 2. If the new node $≤$ head, insert the new node as the head of the updated list.
> 
> <u>Recursive Case</u>
> 1. If the new node $>$ head, the new node is to be inserted after the head. 
> 	1. Make a subcall to insert the value in the next sublist starting at `head.next`.
> 	2. Once the subcall inserts the value and returns with the head of the updated sublist, make sure to re-link it to the current node's next field.

- **Time Complexity:** O(n). 
	- In the worst case, the value is to be inserted at the end of the list.
	- Each recursive call processes one node and moves to the next.
	- Therefore, the total time complexity is O(n).
- **Auxiliary Space:** O(n).
	- Each recursive call adds a frame to the call stack, so there will be one frame for each node traversed.
	- In the worst case, the recursion depth is equal to the length/size of the list.
	- Therefore, the total space complexity is O(n).
### Iterative Approach

```python
def list_insert_ordered(self, data):
        new_node = Node(data)
        
        # If the linked list is empty
        if self.head is None:
            self.head = new_node
            
        # If the data is smaller than the head
        elif self.head.data >= new_node.data:
            new_node.next = self.head
            self.head = new_node
            
        else:
            # Locate the node before the insertion point
            current = self.head
            while current.next and new_node.data > current.next.data:
                current = current.next
                
            # Insertion
            new_node.next = current.next
            current.next = new_node
```

- **Time Complexity:** O(n). Only one traversal of the list is needed.
- **Auxiliary Space:** O(1). No extra space is needed.
