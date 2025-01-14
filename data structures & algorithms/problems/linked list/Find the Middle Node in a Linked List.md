---
difficulty: Easy
status: Redo
topics:
  - "[[linked list|Linked List]]"
  - "[[two pointers|Two Pointers]]"
source: https://leetcode.com/problems/middle-of-the-linked-list/description/
---
## Task
Given the `head` of a singly linked list, return *the middle node of the linked list*.
If there are two middle nodes, return **the second middle** node. [^1]

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
**Example 1:**

![|left|300](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

> **Input:** `head = [1,2,3,4,5]`
> **Output:** `[3,4,5]`
> **Explanation:** The middle node of the list is node 3.

`````

`````col-md
flexGrow=1
===
**Example 2:**

![|left|375](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

> **Input:** `head = [1,2,3,4,5,6]`
> **Output:** `[4,5,6]`
> **Explanation:** Since the list has two middle nodes with values 3 and 4, we return the second one.
`````
``````

## Expected Solution: Fast and Slow Pointers
> O(n) time and O(1) space

We can use the [[two pointers|Two Pointer Technique]] to find the middle of the linked list:

1. Traverse the linked list using a `slow` and `fast` pointer:
	1. The **slow pointer** moves 1 step at a time.
	1. The **fast pointer** moves 2 steps at a time.
2. By the time the **fast pointer** reaches the end of the list (last node) or NULL, the **slow pointer** will be at the middle of the list.

> [!maths|black|outlined]
> Let the length of the list be $n$.
> When `fast` reaches the end of the list, it has traveled `n` steps.
> Then `slow`, which moves at **half the speed**, has traveled `n/2` steps.

> [!attention|yellow]
> In case of **odd** number of nodes in the linked list, `slow` will reach the middle node when `fast` will reach the **last node**.
>
> In case of **even** number of nodes in the linked list, `slow` will reach the middle node when `fast` will become **NULL**.

```python
def middleNode(self, head):
	slow = fast = head
	while fast and fast.next:
		slow = slow.next
		fast = fast.next.next
	return slow
```

```python
def getMiddle(head):

    # Initialize the slow and fast pointer to the
    # head of the linked list
    slow = head
    fast = head
    
    while fast is not None and fast.next is not None:
    
        # Move the fast pointer by two nodes
        fast = fast.next.next
        
        # Move the slow pointer by one node
        slow = slow.next
        
    # Return the slow pointer which is currently pointing to the
    # middle node of the linked list
    return slow.data
```

[^1]: If the number of nodes are even, then there would be two middle nodes.