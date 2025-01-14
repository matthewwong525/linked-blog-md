Linked List is a [[recursion#Recursive Data Structures|recursive data structure]] because a list can be defined as either:
1. an empty list or
2. a node followed by a list

```c file="C definition of a linked list node" hlt:3
struct node {
	int data;
	struct node *next;
}
```

*Note*: the node is defined in terms of itself.

> [!tip]
> Because a linked list is recursively defined as an object referencing a list (or null), operations on the linked list can be implemented using recursion.
> 
> This means we usually have a base case where the node pointer is `NULL`, and a recursive case where we do something with the current value and recursively call the function on the rest of the list. Depending on the problem, there may be more base cases or recursive cases.
> 

> [!thought|teal] Recursive Thinking with Linked Lists
> - Base cases
> 	- **Empty List** — either list was initially empty OR we reached the end of the list (past the last node)
> - Recursive cases
> 	- **Non-empty list with next node**
> - Edge cases
> 	- **List with 1 node / Non-empty list but no next node** — at the start & end of the list [^6]
>
> <u>Notes:</u>
> - Handle the edge case where list only has 1 node
> - If we are not at the base case/correct node position:
> 	- call itself on the *next node* to traverse down the list until we are at the base case
> 	- each recursive call moves down the list by 1 node until the base case is met
> - If we need to modify the list:
> 	- base case should return the head of the updated list
> 	- recursive case should update `next` pointers at each step
> 	  
> > <i class="default"><b>How do we keep track of the previous node?</b></i>
> 
> In an iterative approach, you would use a `previous` pointer to keep track of the node before the current node. 
> 
> In recursion, the call stack itself keeps track of the "previous node". When recursion unwinds, each recursive call returns its value back to its caller aka its predecessor. 
> 
> A recursive call like this on the next node would return the updated sublist starting at the `head.next` back to the current node `head`, and we reattach it back:
> ```python hlt:5
> def do_insert(head, new_node):
> 	if (head is None):
> 		return new_node
> 	else:
> 		head.next = do_insert(head.next, value)
> 		return head
> ```
## List Count
``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
Recursive Solution
- **Time Complexity**: O(N)
- **Auxiliary Space**: O(N), extra space is used in the recursion call stack.
  
```python file="Method 1" hlt:'count + 1'
def get_count(self):
	def do_get_count(node, count):
		# Base case
		if node is None:
			return count
		# Recursive case
		else:
			return do_get_count(node.next, count + 1)
			
	return do_get_count(self.head, 0)
```

```python file="Method 2" hlt=' + 1'
def get_count(self):
	def do_get_count(node):
		# Base case
		if node is None:
			return 0
		# Recursive case
		else:
			return do_get_count(node.next) + 1
			
	return do_get_count(self.head)
```

Each of the recursive call returns **1 + count** of remaining nodes.
`````

`````col-md
flexGrow=1
===
Iterative Solution
- **Time Complexity:** O(N)
- **Auxiliary Space**: O(1), as constant extra space is used.
  
```python
def get_count(self):
	count = 0
	current = self.head
	while current is not None:
		count += 1
		current = current.next

	return count
```
`````
``````




## List Sum

```C file="Summing a Linked List" 
int listSum(struct node *list) {
    // Base case: empty list
    if (list == NULL) { 
        return 0;
    }
    // Recursive case: non-empty list
    return list->value + listSum(list->next);
}
```

- ***Base case:* Empty list.** The sum of an empty list is 0.
- ***Recursive case:* Non-empty list.** The sum of the list is the value of the node plus the sum of the rest of the list.

```python file="Summing a Linked List"
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

def sum_linked_list(node):
    # Base case: if the node is None, return 0
    if not node:
        return 0

    # Recursive case: add the current node to the sum of the rest of the list
    return node.data + sum_linked_list(node.next)
```

## List Append

```c
struct node *listAppend(struct node *list, int value) {
    // implement this function
}
```

`listAppend` should insert the given value at the end of the given list and return a pointer to the start of the updated list.

> [!question]
> What's wrong with this?
> ```c file="Append a node to the list"
> struct node *listAppend(struct node *list, int value) {
>     if (list == NULL) {
>         return newNode(value);
>     } else {
>         listAppend(list->next, value);   
>         return list;
>     }
> }
> ```

> [!correct]- Answer
> If `list->next` is `NULL` (list only has one node), the new node does not get attached to the list.
> ```C file="Append a node to the list" error:6
> struct node *listAppend(struct node *list, int value) {
>     if (list == NULL) {
>         return newNode(value);
>     } else {
> 	    // calling listAppend when list has only 1 node does nothing 
>         listAppend(list->next, value);   
>         return list;
>     }
> }
> ```

> [!success]- One solution
> Handle the case where there is only 1 item in the list.
> This works, but is not very elegant, as it repeats the call to `newNode` and repeats `return list`.
> ```c file="Append a node to the list" ins:7-9
> struct node *listAppend(struct node *list, int value) {
>     // Base case: empty list
>     if (list == NULL) {
>         return newNode(value);
>         
>     // Recursive case 1: non-empty list, but no next node
>     } else if (list->next == NULL) {
>         list->next = newNode(value);  // Add newNode after current node
>         return list;
>         
>     // Recursive case 2: non-empty list, with next node
>     } else {
>         listAppend(list->next, value);
>         return list;
>     }
> }
> ```

> [!success|green]- Better solution
>
> ```c hl:5-6
> struct node listAppend(struct node *list, int value) {
> 	if (list == NULL) {
> 		return newNode(value);
> 	} else {
> 		list->next = listAppend(list->next, value);
> 		return list;
> 	}
> }
> ```
>
> **Recursive Case:**
>
> ```c exclude
> // pass the next node to listAppend => listAppend will return the new list
> // and we will update the next node of the current list to the new list
> list->next = listAppend(list->next, value);
> return list;
> ```
>
> 1. The recursive call will repeatedly pass `list->next` (the *next node* in the list) as the new input — **recursive case**
> 2. This continues until we reach the end of the list (`list == NULL`) — **base case is met**
> 3. The base case will return the new node — **recursion unwinds**
> 4. Update `list->next` to point to the new node (which becomes a sub-list) to maintain the linked structure as the call propagates back up the list (to the head).
>
> **TLDR:**
> - `listAppend(list->next)` will return the updated sub-list on `list->next`.
> - Update the `next` pointers to the returned sub-list `listAppend(list->next, value)`.