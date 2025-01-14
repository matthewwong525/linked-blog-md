---
difficulty: Medium
status: Redo
topics:
  - "[[linked list|Linked List]]"
  - "[[two pointers|Two Pointers]]"
source: https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/description/?envType=study-plan-v2&envId=leetcode-75
---
## Task
You are given the `head` of a linked list. **Delete** the **middle node**, and return <i class="default">the `head` of the modified linked list</i>.

The **middle node** of a linked list of size `n` is the `⌊n / 2⌋th` node from the **start** using **0-based indexing**, where `⌊x⌋` denotes the largest integer less than or equal to `x`.


> [!hint]- Hint 
> If a point with a speed `s` moves `n` units in a given time, a point with speed `2 * s` will move `2 * n` units at the same time. Can you use this to find the middle node of a linked list?

## My Solutions
```python
def deleteMiddle(self, head):
	# get the length of the list
	def getLength(head):
		count = 0
		current = head
		while current is not None:
			count += 1
			current = current.next
		return count
	
	# calculate the middle index
	mid = getLength(head) / 2

	# iterate to the index mid-1
	current = head
	for _ in range(mid - 1):
		current = current.next
		
	# delete node
	current.next = current.next.next
	return head
```

## Sample Solutions
### Naive Approach: 2 Passes
> O(n) time and O(1) space

1. Iterate through the entire list to get the length (total number of nodes).
2. Iterate again through the list to the <i class="default">predecessor</i> node of the middle node i.e stop at index `middleIndex - 1`.
3. Remove the node.

```python
def deleteMiddle(self, head):  
	# Edge case: return None if there is only one node.
	if head.next == None:
		return None
	
	count = 0
	p1 = p2 = head
	
	# First pass, count the number of nodes in the linked list using 'p1'.
	while p1:
		count += 1
		p1 = p1.next
	
	# Get the index of the node to be deleted.
	middle_index = count // 2
	
	# Second pass, let 'p2' move toward the predecessor of the middle node.
	for _ in range(middle_index - 1):
		p2 = p2.next
	
	# Delete the middle node and return 'head'.
	p2.next = p2.next.next
	return head
```

- **Time Complexity: O(2n) = O(n)**
	- We iterate over the linked list twice, the first time traversing the entire linked list and the second traversing half of it. Hence there are a total of O(n) steps.
	- In each step, we move a pointer forward by one node, which takes constant time.
	- Remove the middle node takes a constant amount of time.
	- In summary, the overall time complexity is O(n).
- **Space Complexity: O(1)**
	- We only need two pointers, thus the space complexity is O(1).
### Expected Approach: Fast and Slow Pointers
> O(n) time and O(1) space

Have two pointers `fast` and `slow` traversing the linked list at the same time, and `fast` traverses *twice* as fast as `slow`. Therefore, when `fast` reaches the end of the linked list, `slow` is right in the middle! We only need one iteration to reach the middle node!

> <b>Why we initialise `fast` to the <i class="default">third node</i> and not the head at the beginning ? `fast = head.next.next`</b>


The reason for this is that we want to deleted the middle node instead of finding it. Therefore, we are actually looking for the <i class="default">predecessor of the middle node</i>, not the middle node itself. This is like moving `slow` backward one node after the iteration stops. 

Since we can't move a pointer backwards on a singly linked list, we can show this one less step on `slow` by letting `fast` move forward one more step (by two nodes, of course). Hence, `slow` will also point to the predecessor node of the middle node (rather than the middle node) at the end of the iteration.

> [!image]- Visualisation
>  ![[linked-list-delete-middle-node-2-pointer.png|Delete the middle node with fast and slow pointers.|500]]

```python
def deleteMiddle(self, head):
    # Edge case: return None if there is only one node.
    if head.next == None:
        return None
        
    # Initialize two pointers, 'slow' and 'fast'.
    slow, fast = head, head.next.next
    
    # Let 'fast' move forward by 2 nodes, 'slow' move forward by 1 node each step.
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
    # When 'fast' reaches the end, remove the next node of 'slow' and return 'head'.
    slow.next = slow.next.next
    
    # The job is done, return 'head'.
    return head
```

- Time complexity: O(n)
    - We stop the iteration when the pointer `fast` reaches the end, `fast` moves forward 2 nodes per step, so there are at most n/2 steps.
    - In each step, we move both `fast` and `slow`, which takes a constant amount of time.
    - Removing the middle node also takes constant time.
    - In summary, the overall time complexity is O(n).
- Space complexity: O(1)
    - We only need two pointers, so the space complexity is O(1)


<u>Edge Case </u>
If the linked list contains only 1 node, this node is the one to be deleted and there will be no node left after the deletion. Return null.
 
