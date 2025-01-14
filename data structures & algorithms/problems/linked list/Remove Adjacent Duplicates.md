```python hl:12-14
"""
Delete any adjacent duplicate values
Leave the first instance of the duplicate value in the list
"""
def delete_duplicates(self):
    current = self.head

    while current is not None and current.next is not None:
        if current.data == current.next.data:
            # remove current.next
            current.next = current.next.next
        else:
            # move to the next node
            current = current.next
```

> [!alert|no-title]
> When `current.next` is deleted, we don't update `current` to the next node because `current.next` is now pointing to the new next node in the modified list!

> [!question]
> What is wrong with this?
> ```py ln=true
> if current.data == current.next.data:
> 	#  remove current.next
> 	current.next = current.next.next
> 
> # move to the next node
> current = current.next
> ```
>
> > [!answer]-
> >
> > > [!error] Wrong
> > >
> > > ```py ln=true info:3 error:5-6
> > > if current.data == current.next.data:
> > > 	#  remove current.next
> > > 	current.next = current.next.next
> > > 
> > > # move to the next node
> > > current = current.next
> > > ```
> > > After removing `current.next` (a duplicate) in lines 1-3, <mark class="grey">`current` is now linked to a new node `current.next.next`</mark>.
> > >
> > > Once we move to the next node in line 6, we will skip comparing `current` with `current.next.next` (the *new adjacent node* to current).
> >
> > > [!correct|green]
> > >
> > > ```py ln=true success:4-6
> > > if current.data == current.next.data:
> > > 	# remove current.next 
> > > 	current.next = current.next.next
> > > else:
> > > 	# move to the next node only if no duplicate is found
> > > 	current = current.next
> > > ```
> > >
> > > When `current.next` is deleted, we don't advance to the next node for the next iteration because we want to re-check `current` with its updated `current.next`.
> > >
> > > In the next loop iteration, `current` is compared with `current.next.next`.
> > >