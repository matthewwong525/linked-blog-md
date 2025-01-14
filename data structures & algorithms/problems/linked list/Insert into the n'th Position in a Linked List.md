---
difficulty: Medium
status: Redo
topics:
  - "[[linked list|Linked List]]"
  - "[[recursion|Recursion]]"
---
## Task
Your task is to implement this function `list_insert_ordered`:

```py
class LinkedList:
    def __init__(self):
        self.head = None
           
    def list_insert_ordered(self, value):
		#TODO 
```

This function should use *recursion* to insert the given value before position `n` of the linked list.

The list elements are numbered in the same manner as array elements, so the first element in the list is considered to be at position 0, the second element is considered to be at position 1, and so on.

If there are less than `n` elements in the list, the new value should be inserted at the end of the list. You can assume that `n` is non-negative.

``` file='Example Usage'
$. /listInsertNth
Enter list size: 3
Enter list values: 16 7 8
List: [16, 7, 8]
Enter position and value to insert: 0 12
List after inserting 12 at position O: [12, 16, 7, 8]

$ ./listInsertNth
Enter list size: 3
Enter list values: 16 7 8
List: [16, 7, 8]
Enter position and value to insert: 1 12
List after inserting 12 at position 1: [16, 12, 7, 8]

$ ./listInsertNth
Enter list size: 3
Enter list values: 16 7 8
List: [16, 7, 8]
Enter position and value to insert: 2 12
List after inserting 12 at position 2: [16, 7, 12, 8]

$ ./listInsertNth
Enter list size: 3
Enter list values: 16 7 8
List: [16, 7, 8]
Enter position and value to insert: 3 12
List after inserting 12 at position 3: [16, 7, 8, 12]

$ ./listInsertNth
Enter list size: 3
Enter list values: 16 7 8
List: [16, 7, 8]
Enter position and value to insert: 4 12
List after inserting 12 at position 4: [16, 7, 8, 12]

$ ./listInsertNth
Enter list size: 1
Enter list values: 42
List: [42]
Enter position and value to insert: 0 16
List after inserting 16 at position O: [16, 42]

$ ./listInsertNth
Enter list size: 0
List: []
Enter position and value to insert: 0 2
List after inserting 2 at position 0: [2]

$ ./listInsertNth
Enter list size: 0
List: []
Enter position and value to insert: 10 2
List after inserting 2 at position 10: [2]
```

## My Solutions

1. Find the node before the point of insertion at index `n-1`.
2. Add a counter in the recursive helper function to get the index of the current node.
3. If the counter = n-1 then insert the new node and return the head of the updated list
4. Otherwise, recurse until counter = n-1 or until list is empty (i.e. reached the end and n was not found)

```python
def insert_nth(self, n, value):
	new_node = Node(value)
	
	def do_insert_nth(head, index):
		# If list is empty - return new node as head
		if head is None:
			return new_node
			
		# At the point before insertion - insert new node after head
		elif head.next and index == n - 1:
			new_node.next = head.next
			head.next = new_node
			return head
			
		# Not at the insertion point - attach head to subcall
		else:
			head.next = do_insert_nth(head.next, index + 1)
			return head
			
	# If n is 0, insert as head
	if n == 0:
		new_node.next = self.head
		self.head = new_node
	# Otherwise, insert into list recursively
	else:
		self.head = do_insert_nth(self.head, 0)
```

## Sample Solutions
The goal is to insert the new node before position `n` in the list. 
With each recursive call, we move through the list by 1 node ⇒ 1 step closer to `n`.
Therefore, each recursive call decrements `n` by 1 to keep track of how many positions we have left to reach the insertion point.
When `n` reaches 0, we have reached the current node at position `n`. 

> **How do we insert the new node <em>before</em> the current node?**

When `n = 0`, we have reached the node at the insertion point. We want to insert the new node before the current node, so we insert it as the **head** of the list, and attach the current node to the new node's `next` field.

> **Why do we stop at `head is None` or `n <= 0`?** 

In the case where `n` is greater than the length of the list, the recursion will eventually reach the end of the list (`head is None`). At that point, we want to insert the new node at the end of the list. The `n <= 0` is just a safeguard in case of negative input since `head is None` will stop `n` from being decremented until it's negative.

```python hlt:5
def insert_nth(self, n, value):
	def do_insert_nth(head, n, value):
		if head is None or n <= 0:
			new_node = Node(value)
			new_node.next = head
			return new_node
		else:
			head.next = do_insert_nth(head.next, n - 1, value)
			return head
			
	self.head = do_insert_nth(self.head, n, value)
```

> [!function|green] Algorithm
> <u>Base Case</u>
> - If the current node is NULL, we reached the end of the list without finding n. In this case, we just return the new node as the head. 
> - If n = 0, we reached the point of insertion. To insert the new node before the node at this point of insertion, we insert the new node as the head of the sublist.
> 
> <u>Recursive Case</u>
> - If we haven't reached n = 0  or the end of the list, we need to traverse further.
> - Move to the next node by making a subcall with `head.next` and `n - 1`.
> - Once the subcall returns the updated sublist, we link it back to the current node.

> [!time|teal] Complexity Analysis
> - **Time Complexity: O(n)**
> 	- Each recursive call processes one node, up to position `n` or the end of the list.
> - **Space Complexity: O(n)**
> 	- The recursion depth corresponds to the number of nodes traversed.
> 	- In the worst case, we traverse all n nodes to the end of the list.

