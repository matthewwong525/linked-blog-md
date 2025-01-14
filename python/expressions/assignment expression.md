The `:=` operator allows you to **assign a value** to a variable **within an expression**:

```hlt::= tsep:^
variable := expression    # returns expression
```

This *assignment expression* (also called a “*named expression*”):

1. Returns the result of the expression ... and
2. Assigns that result to the variable 

> [!alert|no-title]
> `:=` differs from `=` in that `x = y` is an assignment [[python/glossary/glossary#statement|statement]] that does not return anything, whereas an [[python/glossary/glossary#expression|expression]]  always returns a value.

It is commonly used as a conditional expression (condition) to return a value to be evaluated as a condition while also executing the expression as a side effect:

```python hlt:2|x:),{x}
def validate_length(string):
    if (x := len(string)) < 8:   # if (len(string) < 8)
        print(f"Length is too short: {x}")  # x = len(string)
    else:
        print(f"Length {x} is OK!")  
```

Another common use case is when handling matched regular expressions:

```python
if matching := pattern.search(data):
    do_something(matching)
```

Or, when processing a file stream in chunks:

```python
while chunk := file.read(9000):
    process(chunk)
```