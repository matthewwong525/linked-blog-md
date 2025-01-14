---
difficulty: Easy
status: Attempted
topics:
  - "[[linked list|Linked List]]"
  - "[[recursion|Recursion]]"
---
## Task
Your task is to implement this function in `listMax.c`:

```c
int listMax(struct node *list);
```

This function should use *recursion* to find the largest value in the given list.

You can assume that the list is not empty.

> [!warning|red]
> You must not use while loops, for loops, do loops or goto statements. Solutions that use any of these will not receive any marks.

> [!hint]-
> **Base case**: If there is one element in the list, what would the maximum element be?
> 
> **Recursive case**: Suppose you found the maximum element among all the elements from the 2nd element onwards. In what case would this element be the maximum element of the entire list? In what case would it not be?
> 

```bash file="Example Usage"
$ ./listMax
Enter list size: 5
Enter list values: 7 2 6 8 0
List: [7, 2, 6, 8, 0]
The maximum element is: 8

$ ./listMax
Enter list size: 5
Enter list values: 9 6 1 8 8 
List: [9, 6, 1, 8, 8]
The maximum element is: 9 

$ ./listMax
Enter list size: 4
Enter list values: 2 5 2 1 
List: [2, 5, 2, 1]
The maximum element is: 5

$ ./listMax
Enter list size: 1
Enter list values: 42
List: [42]
The maximum element is: 42
```
## My Solutions
```python
def list_max(list):
    # Base Case
    if list.next is None:
        return list.value
        
    # Recursive Case
    else:
        m = list_max(list.next)
        return m if m > list.value else list.value
```

List needs at least 2 nodes in order to compare values.
Compare `list` and `list->next` and return the largest value of the 2.
Then compare this value with `list->next->next`.
Keep going down the list, comparing 2 nodes at the time until we reach the last node.

<u>Base Case</u>
If the list has only one node, the largest value is the value of that node.

<u>Recursive Case</u>
Assume that `listMax(list.next)` will correctly return the largest value in the sublist starting from `list.next`.

Compare the value of the current node with the largest value found in the remainder of the list. Return the largest between those two.

> [!example] Example: 1 → 4 → 2 → 5
> 1. listMax() is called with the head node and makes a subcall to the next node
> 2. ....
> 3. ....
> 4. `listMax(5)` triggers the base case and returns 5 => stack unwinds and the previous call to listMax(2) resumes execution.
> 5. `listMax(2)` evaluates 5 > 2 ? 5 : 2 and returns 5 =>
> 6. `listMax(4)` evaluates 5 > 4 ? 5 : 4 and returns 5 =>
> 7. `listMax(1)` evaluates 5 > 4 ? 5 : 4 and returns 5.
> 


## Sample Solution
```c
int listMax(struct node *list) {
	assert(list != NULL);
	
    if (list->next == NULL) {
        return list->value;
    } else {
        int max = listMax(list->next);
        if (list->value > max) {
            return list->value;
        } else {
            return max;
        }
    }
}
```