```python hlt:10
def reverse(self):
	"""
	Reverse the linked list
	Need to point current.next to previous
	"""
	previous = None
	current = self.head
	while current is not None:
	    temp = current.next  # save the address of the next node
	    current.next = previous
	    previous = current
	    current = temp       # move to the next node
	    
	self.head = previous
```

For each node in the list, link it to the previous node: `current.next = previous`.
When we exit the loop, `previous` is the last node = new head.
Update the head of the list to previous.