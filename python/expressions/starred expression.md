The `*` iterable unpacking operator placed **BEFORE** a *name* (variable or parameter) is called a **starred expression** that allows for the [[packing & unpacking#Unpacking|unpacking]] of elements from iterables:

```
first, *rest = seq
```

The starred expression `*rest` unpacks the iterable assigned or passed to it and collects all <abbr data-title="values that haven't been assigned to a variable">remaining</abbr> values in the **"catch-all"** name that uses the asterisk (`rest` in this case).

The tuple unpacking feature is used in 2 ways:

1. [[variables assignment|Assignment]]
2. [[functions#arbitrary arguments|Arbitrary Arguments]]

> [!info] Difference between starred expression VS arbitrary arguments
> - `*var` is an **starred assignment target** that collects all remaining items from an iterable in a ***list***.
> - `*args` is an **arbitrary argument** that collects all remaining arguments into a ***tuple***.
> 
> > [!col]
> >
> > ```python file="assignment target" info:1
> > a, b, *c = range(5)
> > print(a)  # 0
> > print(b)  # 1
> > print(c)  # [2, 3, 4] - list
> > ```
> >
> > ```python file="arbitrary argument" info:1,6
> > def foo(a, b, *c):
> >     print(a)  # 0
> >     print(b)  # 1
> >     print(c)  # (2, 3, 4) - tuple
> > 
> > foo(range(5))
> > ```

## assignment target
In an assignment `first, *rest = iterable`, the "starred" expression unpacks all the <abbr data-title="items that haven't been assigned to a variable">remaining</abbr> iterable items and collects them into a **list**.

For example, we can split a **sequence** into 3 different variables:

```python hlt:1|*middle,1|2:4
first, *middle, last = (1, 2, 3, 4, 5)  

print(first)   # 1
print(middle)  # [2, 3, 4] - list
print(last)    # 5
```

```python hlt:*a,*b,*c,1|1:3,6|2:4,11|3:5
*a, b, c = [1, 2, 3, 4, 5]
print(a)  # [1, 2, 3]
print(b)  # 4
print(c)  # 5

a, *b, c = [1, 2, 3, 4, 5]
print(a)  # 1
print(b)  # [2, 3, 4]
print(c)  # 5

a, b, *c = [1, 2, 3, 4, 5]
print(a)  # 1
print(b)  # 2
print(c)  # [3, 4, 5]
```

- `*var` is called a "starred" expression (while others are called "mandatory")
- `*var` is creates a =="catch-all" variable== (`var`) that collects all *unassigned* items from the iterable in a **list (not tuple)** — similar to how `*arg` and `**kwargs` works

> [!alert] Problem
> 
> 1. Only one `*` operator is allowed in an assignment statement:
> 
> ```python
> a, *b, c = 1, 2, 3, 4, 5 # SyntaxError
> ```
> 
> 2. `*var` cannot be used as the only assignment target:
> 
> ```python
> *a = range(5) # Error
> ```
> 

> [!solution]
> If you want to unpack all of the items in an iterable into a single variable, you need to convert it to a list or tuple first. Adding a trailing comma will do the trick; it will make our variable a list that can take as many arguments as you want:
> 
> ```python hlt:4
> my_range = range(5)
> # SyntaxError: starred assignment target must be in a list or tuple
> 
> *my_range, = range(5) 
> # 0, 1, 2, 3, 4
> ```

## argument unpacking: arbitrary arguments
In the same manner as above, a starred expression in a function parameter unpacks the iterable passed, assigns the values to the mandatory (positional) arguments first and then collects all remaining values in a <mark class="orange">tuple</mark> (not list):

```python hlt:1|first:s
def calculate_average(first, *others):
    # first = 10
    # others = (20, 30, 40, 50)  <class 'tuple'>
    total = first + sum(others)
    average = total / (1 + len(others))
    return average


grades = [10, 20, 30, 40, 50]

# Unpack the list inside the function call
average_grade = calculate_average(*grades)

# 30.0
print(average_grade)
```

This enables passing a variable number of arguments to the function.

