The [`pass`](https://docs.python.org/3/reference/simple_stmts.html#pass) statement does nothing. 

It can be used when a statement is required syntactically but the program requires no action:

```python
while True:
	pass 
```

This is commonly used for creating minimal classes:

```python
class MyEmptyClass:
	pass
```

It can be used is as a place-holder for a function or conditional body. The `pass` is silently ignored:

```python
def initlog(*args):
	pass   # Remember to implement this!
```
