---
difficulty: 
status: Todo
topics:
  - "[[linked list|Linked List]]"
---
```python
def insert_after_max(head, data):
    """
    Find the last occurence of the maximum value in the list
    Insert the new node after that
    """
    if head is None:
        return head
        
    # Find the last occurence of the max value
    max_value = head.data
    current = max_node = None
    while current is not None:
        if current.data >= max_value:
            max_value = current.data
            max_node = current

        current = current.next
        
    # Insert the new node after the max node
    new_node = Node(data)
    new_node.next = max_node.next
    max_node.next = new_node

    return head
```
