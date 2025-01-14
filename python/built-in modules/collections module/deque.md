[`deque`](https://docs.python.org/3/library/collections.html#collections.deque "collections.deque") (pronounced “deck”) is a [double-ended queue](https://en.wikipedia.org/wiki/Double-ended_queue) — a list-like data structure with ==fast O(1) insertions and deletion== on either end.

It uses an implementation of a [[linked list|linked list]] in which you can access, insert/remove elements from the beginning or end with constant O(1) performance.

```python
from collections import deque
deque()   # empty deque
```

Pass an **iterable** as input to initialise it:

```python
deque(['a','b','c'])

deque('abc')

deque([{'data': 'a'}, {'data': 'b'}])
```

Methods
- `append(x)`: Add *x* to the **right** side (end).
- `pop()`: Remove and return an element from the **right** side (end).
- `appendLeft(x)`: Add *x* to the **left** side (start; the head).
- `popleft()`: Remove and return an element from **the** left side (start; the head).
## Implement Queues and Stacks
Deques are a generalization of [[stacks|stacks]] and [[queues|queues]], since they support efficient appends and pops from either side (front or back) with constant O(1) performance.
### Queues
With queues, you want to add values to a list (`enqueue`) and later on, remove the element that has been on the list the longest (`dequeue`).

To add (enqueue) values to the back of the list, use `append()`:

```python
from collections import deque
queue = deque()
# deque([])

queue.append("Mary")
queue.append("John")
queue.append("Susan")
# deque(['Mary', 'John', 'Susan'])
```

To remove (dequeue) values from the front of the list, use `popleft()`:

```python
queue.popleft()  # removed 'Mary' 
# deque(['John', 'Susan'])

queue.popleft()  # removed 'John'
# deque(['Susan'])
```

### Stacks
Stack uses the LIFO approach so the last element to be inserted in the stack should be the first to be removed.

To add (push) values to the top of the stack, use `appendleft()`:

```python
from collections import deque
stack = deque()

stack.appendleft("https://realpython.com/")
stack.appendleft("https://realpython.com/pandas-read-write-files/")
stack.appendleft("https://realpython.com/python-csv/")
```

To remove (push) values from the top of the stack, use `popleft()`:

```python
stack.popleft()
stack.popleft()

# deque(['https://realpython.com/'])
```
