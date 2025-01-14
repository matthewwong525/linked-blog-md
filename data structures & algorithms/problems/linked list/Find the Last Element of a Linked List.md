---
difficulty: Easy
status: Solved
topics:
  - "[[linked list|Linked List]]"
  - "[[recursion|Recursion]]"
---
## Task
Your task is to implement this function in `listTail.c`:

```c
int listTail(struct node *list);
```

This function should use *recursion* to find the last value in the given list. 
You can assume that the list is not empty.

> [!warning|red]
> You must not use while loops, for loops, do loops or goto statements. Solutions that use any of these will not receive any marks.

```bash file="Example Usage"
$ ./listTail
Enter list size: 7
Enter list values: 6 8 9 2 5 1 3
List: [6, 8, 9, 2, 5, 1, 3]
The last element is: 3

$ ./listTail
Enter list size: 4
Enter list values: 2 5 2 1
List: [2, 5, 2, 1]
The last element is: 1 

$ ./listTail
Enter list size: 1
Enter list values: 42
List: [42]
The last element is: 42
```
## My Solutions
```python
def list_tail(list):
    assert list is not None
    
    # Base Case
    if list.next is None:
        return list.value
    # Recursive Case
    else:
        return list_tail(list.next)
```
