An expression list is one or more [[python/glossary/glossary#expression|expressions]] separated by commas.
It evaluates to a [[data types#Tuple `(,)`|tuple]] if the expression list contains at least one comma such as `1,`.

## multiple assignment
We can assign *multiple* values in an expression list to *multiple* variables in one line:

```python hlt:1|1:3
x, y, z = 1, 2, 3  
# Assigns x = 1, y = 2, z = 3
```
## tuple packing
By default, an expression list with at least one comma creates a tuple. 

```python hlt:1|1:3
my_tuple = 1, 2, 3  
# Creates a tuple (1, 2, 3)
```

With explicit parentheses:

```python
my_tuple = (1, 2, 3)  # Same as above
```

You can also return a tuple as an expression list:

```python
def example():
    return 1, 2, 3  # Returns the tuple (1, 2, 3)
```
## iterable unpacking
Expression lists can be used to unpack tuples or other iterable objects:

```python hlt:1|x:z
x, y, z = (1, 2, 3)  # Unpacks the tuple into variables
print(x)  # 1
print(y)  # 2
print(z)  # 3
```

```python hlt:1|x:z
x, y, z = [1, 2, 3]  # Unpacks the list into variables
print(x)  # 1
print(y)  # 2
print(z)  # 3
```

> [!alert|no-title]
> The **number of assignment targets** must match the **number of elements in the iterable**

```python error:1
a, b = [1, 2, 3]    # ValueError: trying to assign 3 values to 2 variables
```

