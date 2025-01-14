---
difficulty: Hard
status: Redo
topics:
  - Linked List
source: https://www.algoexpert.io/questions/shift-linked-list
cssclasses:
---
## Task
Given the `head` of a singly linked list and an integer `k`, the task is to *shift* the linked list $k$ times, and return its new head.

Shifting a Linked List means moving its nodes forward or backward and wrapping them around the list where appropriate. For example, shifting a Linked List forward by one position would make its tail become the new head of the linked list.

Whether nodes are moved forward or backward is determined by whether $k$ is positive or negative.

> [!danger] Constraints
> - You must shift the list in place (i.e. don't create a brand new list).
> - You must not modify the values in any nodes

> [!hint]- Hint 1
> Putting aside the case where $n$ is a negative integer, where $n$ is 0, or where $n$ is larger than the length of the linked list, what does shifting the linked list by $n$ positions entail exactly?

> [!hint]- Hint 2
> Putting aside the cases mentioned in Hint #1, shifting the linked list by $n$ positions means moving the last $n$ nodes in the linked list to the front of the linked list. What nodes in the linked list will you actually need to mutate?

> [!hint]- Hint 3
> There are 4 nodes that really matter in this entire process:
>
> 1. the original tail of the linked list, which will point to the original head of the linked list
> 2. the original head of the linked list, which will be pointed to by the original tail of the linked list
> 3. the new tail of the linked list
> 4. the new head of the linked list
>
> Note that the new head is the node that the new tail points to in the original, unshifted linked list.

> [!hint]- Hint 4
> You can find the original tail of the linked list by simply traversing the linked list, starting at the original head of the linked list that you're given.
>
> You can find the new tail of the linked list by moving $n$ positions from the original tail if $n$ is positive (which means moving to the (`lengthOfList - n`)th position in the list, and you can easily count the length of the list as you traverse it to find its original tail).
>
> You can access the new head of the linked list once you've found its new tail, since it's the new tail's original next node. How will you handle the trickier values of $n$?

> [!hint]- Optimal Space & Time Complexity
> O(n) time | O(1) space — where n is the number of nodes in the linked list.

> [!url] Resources
> [Rotate a Linked List | GeekForGeeks](https://www.geeksforgeeks.org/rotate-a-linked-list/)
> [Shift a linked list according to k-variance](https://discuss.python.org/t/writing-an-algorithm-to-shift-a-linked-list-according-to-k-variance/59108)
## Shift Right
> When a linked list is shifted to the right, the node at the end of the list is moved to the start.

Shifting to the right `k` times means:
- `k`-th node from the end = `n-k`-th node from the start becomes the **new head**
- `k+1`-th node from the end = `n-(k+1)`-th node from the start becomes the **new tail**

Note that the new tail was the node BEFORE the new head.

> [!image|green]-
> ![[shift-linked-list.png|Shift List Right|400]]

> [!thought|gray] Approach
> 1. Close the linked list into the ring ⇒ turn it into a [[linked list#Circular Linked Lists|circular linked list]].
> 2. Break the ring after the new tail and in front of the new head.

> **Where is the new head?**

The new head is at the position `n - k`, where `n` is the number of nodes in the list.
The new tail is just before, in the position `n - k - 1`.

> [!list-ol|gray] Algorithm
> 1. Compute the length of the list `n`. Use this to normalise the shift to `k % n`.
> 2. Find the old tail and connect it with the head.
> 3. Find the new tail and new head
> 	2. The new head is the `n-(k % n)`th node.
> 	3. The new tail is the one before that — the `n-(k % n)-1`th node.
> 4. Break the ring `new_tail.next = None` and return `new_head`.

```python
def shift(self, n):
	# Base cases
	if not self.head:
		return None
	if not self.head.next:
		return head
		
	# Get the size of the list
	size = 1  ## note: start at 1 because we want to exit on the last node
	current = self.head
	while current.next is not None:
		current = current.next
		size += 1

	# Normalise the shift
	shift = n % size
	
	# If shift is a multiple of size, no change needed
	if shift == 0:
		return

	# Link the last node to the head (circular list now)
	current.next = self.head
		
	# Find the new head and tail of the list after shifting
	# The new head is at index (size - shift)
	# The new tail is BEFORE this ^
	previous = None
	current = self.head
	for _ in range(size - shift):
		previous = current
		current = current.next
		
	# Update the pointers for the new head and tail
	previous.next = None  # Break the loop
	self.head = current   # Return new head
```

- Time Complexity: O(n)
- Space Complexity: O(1)
## Shift Left
Shifting left by `k` means:
- the `k`-th node becomes the new head, and
- the `n - k + 1`-th node becomes the new tail (the node after the new head).

> [!image|green]-
> ![[shift-linked-list-left.png|Shift List Left|400]]
### Approach 1: Shifting head node to the end $k$ times
To rotate a linked list to the left $n$ places, we can repeatedly move the head node to the end of the linked list $k$ times.

```python
# Function to rotate the linked list left by k nodes
def rotate(head, k):
    if k == 0 or head is None:
        return head

    # Rotate the list by k nodes
    for _ in range(k):
        curr = head
        while curr.next is not None:
            curr = curr.next
        
        # Move the first node to the last
        curr.next = head
        curr = curr.next
        head = head.next
        curr.next = None
    
    return head
```

- **Time Complexity: O(n * k),** where n is the number of nodes in Linked List and k is the number of rotations.
- **Auxiliary Space: O(1)**
### Approach 2: Optimised
The idea is to first convert the linked list to a circular linked list by updating the next pointer of the last to the head of the linked list. Then traverse to the `k`-th node and update the head of the linked list to the `(k+1)`th node. Finally, break the loop by updating the next point of the `k`-th node to NULL.

```python
def rotate(head, k):
    if k == 0 or head is None:
        return head

    curr = head
    length = 1

    # Find the length of the linked list
    while curr.next is not None:
        curr = curr.next
        length += 1

    # Modulo k with length of linked list to handle
    # large values of k
    k %= length

    if k == 0:
        curr.next = None
        return head

    # Make the linked list circular
    curr.next = head

    # Traverse the linked list to find the kth node
    curr = head
    for _ in range(1, k):
        curr = curr.next

    # Update the (k + 1)th node as the new head
    newHead = curr.next

    # Break the loop by updating the next pointer
    # of kth node
    curr.next = None
    return newHead
```

- **Time Complexity: O(n)**, where n is the number of nodes in linked list.
- **Auxiliary Space: O(1)**
## Shift Both Ways
Key Idea: ==Shifting Wraps Arounds==
When you shift a linked list, nodes that are moved off one end of the list "wrap around" and reappear at the other end, making shifting a cyclic operation.

This means:
$$\begin{align*}
\text{Shifting right by } k \text{ positions} &= \text{moving } k \text{ nodes to the right}\\
\text{Shifting left by } k \text{ positions} &= \text{moving } k \text{ nodes to the left}\\
&= \text{moving } n + k \text{ nodes to the right}\\
\end{align*}$$

> [!list-ol|yellow] Handling Negative Shifts
> 1. <i class="default">Normalise</i> the shift value by calculating modulus size: `shift % size`.
> 	1. e.g. for size 6, that will result in a shift value in the range -5 to +5.
> 2. Eliminate any left (negative) shifts by adding the size and calculating modulus again: `(shift + size) % size` 
> 	1. This converts a negative left shift into a positive right shift
 
```python
def shiftLinkedList(head, k):
	# Base case
    if head is None:
        return

    # Find the size of the list and the tail node
    current = head
    size = 1
    while current.next is not None:
        size += 1
        current = current.next

    # Normalize the shift
    shift = k % size if k >= 0 else (k + size) % size

    # If no shift is needed
    if shift == 0:
        return head

    # Link the tail to the head to form a circular list
    current.next = head

    # Find the new tail (size - shift - 1) and new head (size - shift)
    p = head
    for _ in range(1, size - shift):
        p = p.next

    # Set the new head and break the loop
    new_head = p.next
    p.next = None

    return new_head
```

## Shifting a Linked List - Recursively! 
Implement this function `list_shift`. 

```python 
# This is the class of the input linked list.
class LinkedList:
    def __init__(self, value):
        self.value = value
        self.next = None


def list_shift(head):
    # Write your code here.
```

This function should use *recursion* to shift the given list to the right *once* and return a pointer to the start of the updated list. 

``` file="Example Usage"
$ ./listShift
Enter list size: 3
Enter list values: 16 5 2
List: [16, 5, 2]
List after shifting: [2, 16, 5]

$ ./listShift
Enter list size: 5
Enter list values: 9 6 1 8 8 
List: [9, 6, 1, 8, 8]
List after shifting: [8, 9, 6, 1, 8]

$ ./listShift
Enter list size: 2
Enter list values: 1 0
List: [1, 0]
List after shifting: [0, 1]

$ ./listShift
Enter list size: 1
Enter list values: 1
List: [1]
List after shifting: [1]
```


> [!outline]
> **Approach**
> Recall the recursion works backwards! The recursive calls helps us reach the end of the list first, then we fix the connections as we "walk back" to the front.
> 
> Starting from the last node and working backwards, we want to "shift" the last node aka new head to the front of the list. So on each step, we insert the last node before the current node to move it in front (by setting current.next = last node). All other connections remain the same.
> 
> The only other node that matters in this process is the new tail aka the 2nd last node. Since it is connected to the last node, swapping them creates a circular loop (5 -> 4 -> 5). To break the loop, we need to point it to NULL instead. 
> 
> ![[linked-list-shift-recursive.png|Shifting a Linked List Recursively]]
> 
> 
> **Algorithm**
> 1. Scan to the end to find the last node.
> 2. Make that last node the new head ⇒ return it as the new head of the shifted list
> 3. Make the previous node (2nd last) the new tail ⇒ point it to NULL
> 4. Fix the connections as we walk back to the front ⇒ insert the last node (i.e. the return of each subcall) as the new head of the current list

### Recursive Approach 1
```python
def list_shift(self):
	def shift_once(head):
		# Base case: If list has 0 or 1 nodes, it is already shifted
		if head is None or head.next is None:
			return head
		# Recursive case
		else:
			new_head = shift_once(head.next)
			# If we are one the second last node, make it the new tail
			if new_head.next is None:
				head.next = new_head.next

			# shift the new head to the front
			new_head.next = head
			return new_head

	# Update the head
	self.head = shift_once(self.head)
```

### Recursive Approach 2
This solution has an additional base case that explicitly handles when we're at the second-to-last node. 

```python
def list_shift(self):
	def do_list_shift(head):
		# Base case 1: empty list or single node, list is already shifted
		if head is None or head.next is None:
			return head

		# Base case 2: at the second last node (the new tail)
		if head.next.next is None:
			new_head = head.next    # last node is the new head
			head.next = None        # make second last node the new tail
			new_head.next = head    # insert last node in front
			return new_head

		# Recursive case
		else:
			# insert the new head in front
			new_head = do_list_shift(head.next)
			new_head.next = head
			return new_head

	# Update the head
	self.head = do_list_shift(self.head)
```

