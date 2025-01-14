
Here is a table indicating the relative level of precedence for operators:

|Operators|
|---|
|`()` (highest)|
|`**`|
|`*, /, %`|
|`+, -`|
|`<, <=, >, >= ==, !=`|
|`is, is not`|
|`not`|
|`and`|
|`or` (lowest)|
## DeMorgan’s law
The `not` operator can make expressions more difficult to understand, especially if it is used multiple times. Try only to use the `not` operator where it makes sense to have it.

Most people find it easier to read positive statements than negative ones. So we can rewrite the boolean expression to use the *opposite* relational operator to avoid using the `not` operator.

This table shows each relational operator and its opposite:

| Operator | Opposite |
| -------- | -------- |
| `==`     | `!=`     |
| `>`      | `<=`     |
| `<`      | `>=`     |

Formally, DeMorgan’s laws state:
1. NOT (a AND b) = (NOT a) OR (NOT b)
2. NOT (a OR b) = (NOT a) AND (NOT b)

So we can use these laws to distribute the `not` operator over boolean expressions. For example:

```python
if not mark < 50:
    print("You passed")

# is the same as

if mark >= 50:
    print("You passed")
```

```python
if not (age > 0 and age <= 120):
    print("Invalid age")

# can be rewritten as

if age <= 0 or age > 120:
    print("Invalid age")
```