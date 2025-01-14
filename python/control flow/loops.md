## while
The `while` loop will execute a set of statements as long as a condition is true.

```python
 while boolExpr: 
	# statements
```

> [!col]
>
> > [!div]
> >
> > ```python file="while i < 5..."
> > i = 0
> > while i < 5:
> >     print(i, end=" ")
> >     i += 1 
> > ```
> > ```
> > 0 1 2 3 4
> > ```
>
> > [!div]
> >
> > ```python file="while list still has items..."
> > a = ["apple", "banana", "cherry"]
> > while a:
> >     print(a.pop(-1))
> > ```
> > ```
> > cherry
> > banana
> > apple
> > ```
> > Note that `a` is true as long as it has elements in it. Once all the items have been removed and the list is empty, `a` is false.
>

```python file="do-while loop equivalent"
while True:
    # Execute loop body...
    # Check the condition...
    if condition:
        break
```

> [!col]
> > [!div]
> > A do-while loop executes its body **BEFORE** evaluating the loop condition.[^1]
> > Therefore, the loop’s body will run even if the condition is false.
> >
> > ```c hlt:5,9
> > #include <stdio.h>
> > 
> > int main() {
> >     int number;
> >     do {
> >         printf("Enter a positive number: ");
> >         scanf("%d", &number);
> >         printf("%d\n", number);
> >     } while (number > 0);
> >     return 0;
> > }
> > ```
>
> > [!div]
> > The most common technique to emulate a do-while loop in Python is to use an <font color="#245bdb">infinite</font> `while` loop with a `break` statement
> > 
> > ```python hlt:1,4-5
> > while True:
> >     number = int(input("Enter a positive number: "))
> >     print(number)
> >     if number > 0:
> >         break
> > ```

## for
In Python, the `for` loop *only* iterates over the elements of an [[python/glossary/glossary#iterable|iterable]] (a collection of objects).

This includes [[data types#Sequences|sequences]] such as *list*, *tuple* or *string* or **other collections** like *dict* and *set*:

```python
 for item in iterator: 
	# statements
```

> [!code]- Iterate over sequences
> For example, to iterate over each `item` of a [[data types#Sequences|sequence]]:
>
> ```python file="Loop over Sequences"
> # List
> words = ['cat', 'window', 'lamb']
> for w in words:
> 	print(w)
> 
> # String
> for char in "banana":
>     print(char)
> ```
>
> Note that sequences such as a *list*, *tuple* or *string* are **ordered** so items will appear in the same order they are stored in the sequence:

> [!code]- Iterate over dictionaries
>
> ```python file="Loop over dictionaries"
> # By default, we iterate over the keys (not values)
> dict = {"a": 1, "b": 2, "c": 3}
> for key in dict:
>     print(key)  # a, b, c
> 
> # Loop over values with dict.values()
> for value in dict.values():
>     print(value)  # 1, 2, 3
> 
> # Loop over (key, value) pairs with dict.items()
> for key, value in dict.items():
>     print(key, "->", value)  # a -> 1, b -> 2, c -> 3
> ```
> Note: By default, the `for` loop iterates over the dictionary **keys**.

> [!code]- Iterate over sets
>
> ```python file="Loop over sets"
> fruits = {"apple", "cherry", "banana"}
> for x in fruits:
>     print(x) 
> ```
>
> Note: *Sets* are **unordered**, so you cannot be sure in which order the items will appear:
>
> ```output
> cherry
> banana
> apple
> ```

See [[looping techniques]] for more examples.
> [!danger|outlined] Important
> This is the *pythonic* method of looping over iterables as opposed to using a numeric counter:
>
> > [!col]
> >
> > ```python file="Not Pythonic"
> > for i in range(len(food)):
> >     print(food[i])
> > ```
> >
> > ```python file="Cleaner, Pythonic Way"
> > for piece in food:
> >     print(piece)
> > ```
>
## for and range()
### loop with counter
You can loop over a [[data types#Range|range()]] to create loops with numeric counters similar to these in C:
> [!col]
>
> ```C hlt:1|(:)
> for (int i = 0; i < 10; i++) {
> 	printf("%d\\n", i);
> }
> ```
>
> ```python hlt:range:)
> for i in range(0, 10, 1):
> 	print(i)
> ```

The [[data types#Range|range()]] constructor creates a **numeric sequence** which allows us to iterate a specified number of a times.
### loop with index
To iterate over the indices of a sequence or collection, you can combine [`range()`](https://docs.python.org/3/library/stdtypes.html#range "range") and [`len()`](https://docs.python.org/3/library/functions.html#len "len"):
> [!col]
>
> ```python
> for i in range(0, len(seq)):
> 	# 0-based 
> ```
>
> ```python
> for i in range(1, len(seq)):
>     # 1-based
>     if seq[i - 1] <= seq[i]:
>         return False
> ```

However, it is convenient to use the [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate "enumerate") function
## for and enumerate()
The built-in `enumerate()` function adds a counter to an iterable and returns it as an `enumerate` object, which can be directly used in loops.

```python
>>> list(enumerate(["a", "b", "c", "d"]))
[(0, 'a'), (1, 'b'), (2, 'c'), (3, 'd')
```

### loop with index and value
This is particularly useful when you need both the index and the value of items in an iterable.

> [!col]
> > [!div]
> > With a list of strings as an argument:
> > ```python
> > >>> letters = ["a", "b", "c"]
> > >>> for index, letter in enumerate(letters):
> > ...     print(index, letter)
> > ...
> > 0 a
> > 1 b
> > 2 c
> > ```
> >
>
> > [!div]
> > With a custom start value:
> > ```python
> > >>> for count, letter in enumerate(letters, start=1):
> > ...     print(count, value)
> > ...
> > 1 a
> > 2 b
> > 3 c
> > ```
>
## break / continue
`break` and `continue` are control flow statements used *inside* loops:

- `break` will "break out of" and "end" the <i>innermost</i> enclosing loop immediately
- `continue` will start the next iteration of the loop

> [!col]
> > [!div]
> >
> > ```python file="break"
> > for i in range(5):
> >     if i == 3:
> >         break  # Exits the loop when i is 3
> >     print(i)
> > ```
> > ```
> > 0
> > 1
> > 2
> > ```
>
> > [!div]
> >
> > ```python file="continue"
> > for i in range(5):
> >     if i == 3:
> >         continue  # Skip this iteration
> >     print(i)
> > ```
> > ```
> > 0
> > 1
> > 2
> > 4
> > ```

## else on loops
The `else` block can also be used on loops (a unique Python construct) to execute some code if the loop exits normally (without a `break`).

> [!alert|no-title]
> The `else` block will NOT be executed if the loop is terminated early, either by a `break` or a `return`.

> [!col]
>
> > [!div]
> >
> > ```python
> > for i in range(4):
> >     print(i)
> > else:
> >     print("Loop completed normally.")
> > ```
> >
> > ```
> > 0
> > 1
> > 2
> > 3
> > Loop completed normally
> > ```
>
>
> > [!div]
> >
> > ```python
> > for i in range(4):
> >     print(i)
> >     if i == 1:
> >         break
> > else:
> >     print("Loop completed normally.")
> > ```
> >
> > ```
> > 0 
> > 1 
> > ```
>


