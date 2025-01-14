---
aliases:
  - Tortoise and Hare Algorithm
  - Floyd’s Cycle Finding Algorithm
  - Two Pointers
  - Two Pointer Technique
cssclasses:
---
## Two Pointer Technique
The **two-pointer technique** is a strategy that can be used to solve certain types of problems, particularly those that involve **arrays** or [[linked list#Linked List|linked lists]].

This technique involves using **two pointers**, which navigate through the data structure in various ways, depending on the nature of the problem. The pointers could traverse the array/linked list from **opposite ends**, or at **different speeds** where one moves faster than the other - often referred to as the `slow` and `fast` pointer method.

This technique can greatly optimise performance by reducing time complexity, often enabling solutions to achieve **O(n)** time complexity (by eliminating pairs).

<u>Common Use Cases</u>
- [Two Sum in Sorted Arrays](https://www.geeksforgeeks.org/pair-with-given-sum-in-sorted-array-two-sum-ii/) 
- [Closest Two Sum](https://www.geeksforgeeks.org/two-elements-whose-sum-is-closest-to-zero/)
- [Three Sum](https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/) 
- [Four Sum](https://www.geeksforgeeks.org/find-four-numbers-with-sum-equal-to-given-sum/) 
- [Trapping Rain Water](https://www.geeksforgeeks.org/trapping-rain-water/)
- [[Find the Middle Node in a Linked List]]

> [!url|green] Resources
> [Floyds Cycle Finding Algorithm | GeeksForGeeks](https://www.geeksforgeeks.org/floyds-cycle-finding-algorithm/)
> [Two-Pointer Technique, an In-Depth Guide | Reddit](https://www.reddit.com/r/leetcode/comments/18g9383/twopointer_technique_an_indepth_guide_concepts/)

```
left                            right
 ↓                                ↓
 --- --- --- --- --- --- --- --- ---
| 2 | 1 | 2 | 0 | 1 | 0 | 1 | 0 | 1 |
 --- --- --- --- --- --- --- --- ---
```

This technique should be your go-to when you see a question that involves **==searching for a pair (or more!) of elements in an array that meet a certain criteria==**.

## Cycle Detection in a Linked List
**Floyd’s cycle finding algorithm** is a specific application of the two-pointer technique. The algorithm initialises two pointers, `fast` and `slow` from the head of a linked list. The fast pointer moves at twice the speed of the slow pointer. That’s why this algorithm also known as the **Tortoise and Hair Algorithm**.

<u>What does it do?</u>
1. Detect the presence of a *cycle* or *loop* in a linked list.
2. If a cycle exists, it also helps find the **starting node** of the cycle.

<u>How does it work?</u>
The idea is to have the two pointers `slow` and `fast`, both starting at the *head* of the linked list. The **fast** pointer moves **twice faster** than the slow pointer:

```
fast = fast.next.next
slow = slow.next
```

If the linked list has a cycle (i.e if the tail is connected to another node) the two pointers will meet together at some point. If not, the pointers will never meet.

```
# fast pointer touches the slow pointer
fast == slow
```

- When traversing the list ...
	- `slow` pointer will move *one* step at a time.
	- `fast` pointer moves *two* steps at a time.
- ==When the `slow` and `fast` pointers meet, a cycle or loop exists!==
	- If there’s no cycle, the `fast` pointer will reach the end of the list (i.e. it will become NULL).
	- If there is a cycle, the `fast` pointer will eventually catch/meet up with the `slow` pointer **inside the cycle** because it’s moving faster.

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.value = x
        self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
    
        slow, fast = head, head
        while fast is not None and fast.next is not None:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                print("fast meets slow at node", fast.value)
                return True
            
        return False
```

> [!code|black]- Annotated Version
>
> ```python
> class ListNode:
>     def __init__(self, val):
>         self.val = val
>         self.next = None
> 
> def detectCycle(head):
>     # Initialize two pointers, slow and fast, both initially at the head of the linked list.
>     slow = head
>     fast = head
>     
>     # Step 1: Detect the cycle (Floyd's algorithm)
>     while fast and fast.next:
>         # Move the slow pointer one step at a time.
>         slow = slow.next
>         # Move the fast pointer two steps at a time.
>         fast = fast.next.next
>         
>         # If the slow and fast pointers meet, it indicates the presence of a cycle.
>         if slow == fast:
>             return True  # Cycle detected
>             
>     # If the fast pointer reaches the end of the list (or becomes None), there is no cycle.
>     return False  # No cycle found
> ```

> [!image|green]- Step-By-Step Walkthrough
> ![[cycle-detection-linked-list.png|Detect Loop In a Cycle|400]]

## Find the Start of a Cycle in a Linked List
Using the same algorithm, we can find the starting node of a cycle in a linked list.
Once the slow and fast pointers meet:
1. Reset one pointer to the **head of the list**. (Keep the other at the intersection point)
2. Move both pointers **1 step at a time**.
3. When they meet again, they’re at the **start of the cycle**.

```python
def findFirstNode(head):
  
    # Initialize two pointers, slow and fast
    slow = head
    fast = head
    
    # Traverse the list
    while fast and fast.next:
      
        # Move slow pointer by one step
        slow = slow.next
        
        # Move fast pointer by two steps
        fast = fast.next.next
        
        # Detect loop
        if slow == fast:
          
            # Move slow to head, 
            # keep fast at meeting point
            slow = head
            
            # Move both one step at a time until they meet
            while slow != fast:
                slow = slow.next
                fast = fast.next
                
            # Return the meeting node, which is the 
            # start of the loop
            return slow
    
    # No loop found
    return None
```

> [!image|green]- Step-By-Step Walkthrough
> ![[cycle-detection-start-linked-list.png|Find starting node of a loop|400]]


<u>Why do the pointers meet in a cycle?</u>
This approach works because:
1. The fast pointer travels **twice as fast** as the slow pointer and covers **twice the distance** as the slow pointer.
2. When the slow pointer enters the loop, the fast pointer must <i class="default">already</i> be inside the loop.
4. Inside the cycle, the fast pointer reduces the distance between itself and the slow pointer by **1 step per iteration**. Eventually, the gap becomes 0.

***
Since the fast pointer moves 2 steps and the slow pointer moves 1 step in the same iteration, we can notice that <mark class="green">distance between them (from slow to fast) <b>increase by one</b> after every iteration</mark>:
![|400](https://upload.wikimedia.org/wikipedia/commons/5/5f/Tortoise_and_hare_algorithm.svg)

Initially, if the `slow` pointer is at a distance **k** from a certain point in the cycle, then after one iteration, the distance between the `slow` and `fast` pointers becomes **k+1**. After two iterations, this distance becomes **k+2** and so on.

Let <span style="font-family: 'Source Serif 4'">d</span> be the distance from the fast pointer to the slow pointer:

<center><span style="font-family: 'Source Serif 4'">d = (position of fast pointer) – (position of slow pointer)</span></center>

If the pointers are initially at the same position (e.g. both start at the head), then the distance between them after <span style="font-family: 'Source Serif 4'">k</span> iterations is:

<center><span style="font-family: 'Source Serif 4'">d = k</span></center>

Inside the loop, this distance will eventually equal the cycle length **n**.

<center><span style="font-family: 'Source Serif 4'">d = k &nbsp mod n</span></center>

At this point, **since the distance wraps around the cycle** and both pointers are moving within the same cycle, they will meet.
***

