

Join list items as a single string 

```python error:4
list = [1, 2, 3, 4, 5]

# not using an asterisk 
print(" ".join(list))  # Error: need to convert list items to string first
print(" ".join(map(str, list)))

# using asterisk operator
print(*list)

# Output: 1, 2, 3, 4, 5
```

Print the argument list as a single string (separated by a space)

```python
import sys

# not using an asterisk
print(" ".join(sys.argv[1:]))

# using asterisk
print(*sys.argv[1:])
```

```shell
python3 file.py Hello there
# Hello there
```

Merge multiple lists into one

```python 
list1 = [1, 2, 3]
list2 = [4, 5, 6]

# with concatenation operator (+) - for sequences only
list3 = list1 + list2

# with unpacking operator
list3 = [*list1, *list2]

# with extend() method - but it modifies the original list
list1.extend(list2)
```

Merge multiple dictionaries into one

```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'c': 3, 'd': 4}

# with unpacking operator
dict3 = {**dict1, **dict2}

# with update() method - but it modifies the original dictionary
dict1.update(dict2)
```

> [!alert|no-title]
> **Note:** if there are duplicate keys, the last key-value pair will be preserved