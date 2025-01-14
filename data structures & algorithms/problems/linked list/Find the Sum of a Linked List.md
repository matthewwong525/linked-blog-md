---
difficulty: Easy
status: Solved
topics:
  - "[[linked list|Linked List]]"
  - "[[recursion|Recursion]]"
---
## Task
Your task is to implement this function:

```python hl:10-11
class Node:
    def __init__(self, data):
        self.data = data 
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

	def list_sum(self):
		#TODO
```

```c
int listSum(struct list *list);
```

This function should use a [[recursion#Recursive Helper Functions|recursive helper function]] that takes in a node pointer to find the sum of a linked list.

> [!details]-
> Often in this course, a list will be represented by two structures, one for the usual list node, and one which contains a pointer to the head of the list (along with other data about the list such as its size), usually called a wrapper or container struct.
>
> In this case, since we want to recurse on the nodes, not the wrapper struct, we need to implement a helper function which takes in a node pointer and then call it from the original function. For example:
>
> ```c
> int listFunc(struct list *list) {
> 	return listFuncHelper(list->head);
> }
> ```
>

``` file="Example Usage"
$ ./listSum
Enter list size: 9
Enter list values: 8 1 5 9 6 4 9 5 1
List: [8, 1, 5, 9, 6, 4, 9, 5, 1]
The sum of the values in the list is: 48

$ ./listSum
Enter list size: 6
Enter list values: 2 4 3 7 0 4
List: [2, 4, 3, 7, 0, 4]
The sum of the values in the list is: 20

$ ./listSum
Enter list size: 5
Enter list values: 3 5 2 4 1
List: [3, 5, 2, 4, 1]
The sum of the values in the list is: 15

$ ./listSum
Enter list size: 2
Enter list values: 42 -4
List: [42, -4]
The sum of the values in the list is: 38

$ ./listSum
Enter list size: 0
List: []
The sum of the values in the list is: 0
```

## My Solutions
```python error:6-7
def list_sum(list):
    def do_list_sum(head):
        # Base Cases
        if head is None:
            return 0
        elif head.next is None:
            return head.value
            
        # Recursive Case
        else:
            return head.value + do_list_sum(head.next)
            
    return do_list_sum(list.head)
```

> [!solution] Improved Solution
> **The base case for explicitly handling the last node is not needed!**
> 
> ```python hlt:4,6
> def list_sum(list):
>     def do_list_sum(head):
>         if head is None:
>             return 0
>         else:
>             return head.value + do_list_sum(head.next)
>             
>     return do_list_sum(list.head)
> ```
> 
> 1. When you're one step past the last node, the recursive call will trigger the base case and return 0.
> 2. The stack unwinds and execution resumes to the previous call on the last node, returning `node.value + 0` where `node.value` is the value of the last node.
> 


