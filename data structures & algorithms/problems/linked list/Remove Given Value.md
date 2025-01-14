## Remove all nodes of a given value
```python hl:9-17,20-22
def delete_value(self, value):
	"""
	Remove all nodes with the given value
	"""
	current = self.head
	previous = None
	while current is not None:
		## (1) value found
		if current.data == value:
			# (1.1) deleting a head node
			if previous is None:
				self.head = self.head.next    # delete head
				current = self.head           # move to the new head
			# (1.2) deleting a middle/tail node
			else:
				previous.next = current.next  # delete current
				current = current.next        # move to current.next

		## (2) value not found
		else:
			previous = current
			current = current.next
```

> [!alert|no-title]
> When `current` is deleted, we do NOT update the `previous` node because it has not changed its position in the list — it's still the node prior to our current position!