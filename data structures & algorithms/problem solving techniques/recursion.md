---
aliases:
  - Recursion
cssclasses:
  - defaultCode
---
## Recursion
Recursion is a problem-solving technique where problems are solved by solving *smaller* instances of the same problem.

It involves repeatedly breaking down a big problem into smaller sub-problems, until we get to the simplest form with an obvious answer. The final solution is then found by combining the solutions of the subproblems.

Recursion involves a function^[we call this function a '**recursive function**'] that calls itself.

```python hlt:return:
def factorial(n):
    if n == 0:      # base case: 0! = 1 
        return 1
    else:           # recursive case: n! = n * (n - 1)!
        return n * factorial(n - 1)
```

A recursive function typically has 2 main parts:

1. **Base case(s)**: The simplest instance of the problem that can be solved directly. This is the *termination condition* for the recursion which stops the function from repeatedly calling itself. The base case — <i>edge case</i> or <i>initial condition</i> — is the case where we know the answer to. When the function meets the base case, it returns a value (terminates).
2. **Recursive case(s)**: This is where the function calls itself but on *smaller or simpler input*. We assume the recursive call will return the correct answer and we construct the solution to the problem using the returned value from the call.


<u>Recursive Thinking</u>
1. Can the problem be broken down into smaller subproblems?
2. Can the solution be expressed in terms of smaller instances of itself?
3. Can the task be simplified into an easy action + a smaller variant of the task?
4. How can the result be built from the base & recursive cases?

> [!example]- Example: Factorial
> For example, say we want to compute the factorial of a number.
>
> To solve for `5!`, instead of:
> ```
> 5! = 5 * 4 * 3 * 2 * 1
> ```
> We can break it down into smaller subparts[^1] like so...
> ```
> 5! = 5 * 4!
>    = 5 * (4 * 3!)
>    = 5 * (4 * (3 * 2!))
>    = 5 * (4 * (3 * (2 * 1!)))
>    = 5 * (4 * (3 * (2 * (1 * 0!))))
> ```
> ... until we reach a subproblem we know immediate answer to. In this case: `0! = 1`.
> Now we can work backwards:
> ```
> 5! = 5 * (4 * (3 * (2 * (1 * 1))))
>    = 5 * (4 * (3 * (2 * 1)))
>    = 5 * (4 * (3 * 2))
>    = 5 * (4 * 6)
>    = 5 * 24
>    = 120
> ```
>
> In maths: $n! = n \times (n-1)!$
>
> ```python
> def factorial(n):
>     if n == 0:
>         return 1
>     else:
>         return n * factorial(n - 1)
> ```

> [!example]- Example: Exponentiation
> **Problem:** Implement `pow(x, n)` that calculates $x^n$. In other words, it multiples `x` by itself `n` times.
>
> There are 2 ways to implement this:
>
> ``````col
> borderWidth=0
> textAlign=start
> ===
> `````col-md
> flexGrow=1
> ===
> Iterative Solution
> 
> ```python
> def pow(x, n):
>     result = 1
>     # iterate n times and multiply x
>     for i in range(n):
>         result *= x
> 
>     return result
> ```
> - Time Complexity: `O(n)`
> - Space Complexity: `O(1)`
> `````
> 
> `````col-md
> flexGrow=1
> ===
> Recursive Solution
> 
> ```python
> def pow(x, n):
>     # base case: x^1 = x
>     if n == 1:
>         return x
>     # recursive case: x^n = x * x^(n-1)
>     else:
>         return x * pow(x, n - 1)
> ```
> - Time Complexity: `O(n)`
> - Space Complexity: `O(n)`
> `````
> ``````
>
>
> We can rewrite the problem `pow(x, n)` as `x * pow(x, n - 1)` instead. In maths: x<sup>n</sup> = x * x<sup>n-1</sup>.
>
> This is called a *recursive case/step*: we rewrite the problem in terms of smaller instances of itself. Here, $x^n$ (the problem) depends on $x^{n-1}$ (a smaller instance of the problem).
>
> For example, to calculate `pow(2, 4)`:
>
> 1. `pow(2, 4) = 2 * pow(2, 3)`
> 2. `pow(2, 3) = 2 * pow(2, 2)`
> 3. `pow(2, 2) = 2 * pow(2, 1)`
> 4. `pow(2, 1) = 2`
>
> Each recursive call reduces the problem to a simpler one, until the result is obvious—*base case*.

> [!note] Recursion and the Stack
>
> ![[recursion and the call stack.png|Recursion and the Call Stack.]]
> **Stack Winding**
> 1. `pow(2, 3)` makes a subcall to `pow(2, 2)` to evaluate and return `2 * pow(2, 2)`
> 2. `pow(2, 2)` makes a subcall to `pow(2, 1)` to evaluate and return `2 * pow(2, 1)`
> 3. `pow(2, 1)` triggers the base case and returns `2` => the stack unwinds and `pow(2, 2)` resumes execution.
>
> **Stack Unwinding**
> 1. `pow(2, 2)` receives the result of the subcall `pow(2, 1)` and returns `2 * 2`
> 2. `pow(2, 3)` receives the result of the subcall `pow(2, 2)` and returns `2 * 2 * 2`
>
> **Note:**
> - Each function is waiting on its nested subcall to return.
> - Each function returns its own result to the function that called it.
## Recursion and the Stack
The **call stack** (or execution stack) is an internal data structure that stores information about the <abbr data-title="functions that have been called but have not yet returned"><b>active functions</b></abbr> in a program. Each active function has a <b>stack frame</b> that holds information about the function's execution context, including:
- arguments (parameter values) passed to the function
- local variables
- the function's current position (which line of code it is at)
- return address (where to go back when it returns)

> [!NOTE|no-title]
> Each recursive call has its own separate set of local variables in its own stack frame. Therefore, local variables do not get shared between different recursive calls.

**The call stack is a LIFO data structure.**
- Each function call *pushes* a new stack frame onto the top of the stack.
- The *last* function to be added will be the *first* to execute and *popped* from the stack.
- The top of the stack is the current execution context — the function that is executing now
- In a recursive function:
	- the first frame to be popped off is the call that triggers the base case
	- the last frame to be popped off is the first call to the function

<u>How it works:</u>
1. **Recursive call**: When the function is called, a stack frame is added to the stack. If that function calls another function (recursive call), a new frame is created for that subcall and pushed onto the stack.
2. **Stack winding:** Each recursive call *pushes* a new stack frame *on top* of the existing stack. This creates a chain, where ==each layer (frame) is waiting for the one above it to complete and return==. Execution is paused at each frame until it is at the top of the stack.
3. **Stack unwinding:** When the base case is reached, the function returns. The top frame is popped off and returns its result to the frame below, and so on. Each frame receives the returned value from the frame above, and uses it to complete its own calculations.

> [!alert|no-title]
> **Stack overflow**. If the call stack gets too large (i.e. recursion goes too deep), we can exhaust the stack space leading to a stack overflow error.
## Recursion vs. Iteration
A recursive solution is usually shorter than an iterative one.
However, if there is a simple iterative solution, a recursive solution will generally be slower.

**Memory Considerations**
- Each recursive call creates a new stack frame that holds its own copy of the variables and the return address.
- If you call the function recursively $n$ times, you will end up with $n$ stack frames.
- This consumes much more memory than an iterative solution (iteration only has 1 frame).
- Therefore, creating a stack frame takes time → slower
### Factorial
**Problem:** Calculate the factorial of `n`.

``````col
borderWidth=0
textAlign=start
height=shortest
===
`````col-md
flexGrow=1
===
Iterative Solution

```c
int factorial(int n) {
    int ret = 1;
    for (int i = 1; i <= n; i++) {
        ret *= i;
    }
    return ret;
}
```
- Time Complexity: `O(n)` 
- Space complexity: `O(1)`

***
- Loop iterates from 1 to n doing constant work.
- The stack frame for the function only contains 2 local variables (`ret` and `i`) and some additional overhead for the return address and previous frame pointer. There is no additional memory allocation beyond this.
`````

`````col-md
flexGrow=1
===
Recursive Solution

```C
int factorial(int n) {
    if (n == 0) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}
```

- Time Complexity: `O(n)`
- Space complexity: `O(n)`

***
- The function is called once for each value of n down to 0; total of `n + 1` recursive calls. Each call does constant work (multiplication). Therefore, total time is `O(n)`. 

- Each recursive call to `factorial(n - 1)` creates a new stack frame that holds its own copy of the variable `n` and the return address. If you call the function recursively `n` times, you would end up with `n` stack frames. This would consume more memory compared to the iterative implementation.
`````
``````

### Fibonacci Sequence
**Problem:** Given a positive integer n, find the **n-th** Fibonacci number.

``````col
borderWidth=0
textAlign=start
height=shortest
===
`````col-md
flexGrow=1
===
Iterative Solution
```c 
int fib(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;

    int prev2 = 0;      
    int prev1 = 1;    
    int current;      

    for (int i = 2; i <= n; i++) {
        current = prev1 + prev2;
        prev2 = prev1;   
        prev1 = current; 
    }

    return current;
}
```
- Time Complexity: `O(n)`
- Space Complexity: `O(1)`
***
- The loop iterates from 2 to n, and each iteration does constant work.
- Does not use the call stack; only uses variables.
`````

`````col-md
flexGrow=1
===
Recursive Solution
```C 
int fib(int n) { 
    if (n == 0) return 0;
    if (n == 1) return 1;

    return fib(n - 1) + fib(n - 2);
}
```
- Time Complexity: `O(2^n)`
- Space Complexity: `O(n)` 
---
- The number of recursive calls **doubles** for each call (since each call branches into two more calls). The number of work per call is constant (comparisons and subtraction). Therefore, the time complexity is `O(2^n)` because the number of calls grows **exponentially** to `n`.
- The depth of the recursion tree is `n` because each call reduces n by 1 or 2 at each step. The longest chain of calls occurs at `fib(n - 1)`. Therefore, the **max depth of the recursion stack** is **linear**. 
`````
``````

> [!maths|outlined] Fibonacci Sequence
> Fibonacci is a sequence in which any <abbr data-title="any number in the sequence">term `F(n)`</abbr> is the sum of the <abbr data-title="F(n-1) and F(n-2)">2 previous terms</abbr>:
>
> $$
> \begin{align*}
> F(0) &= 0 \\
> F(1) &= 1 \\
> F(n) &= F(n-1) + F(n-2)
> \end{align*}
> $$
#### Recursive Solution: `O(2^n)` (exponential time)
We can immediately translate this definition[^2] into a recursive procedure:

> [!maths|outlined] Recurrence relation
> - Base Case: `F(0) = 0` and `F(1) = 1`
> - Recursive Case: `F(n) = F(n-1) + F(n-2)`

```python file="Recursive Fibonacci"
def fib(n):
    # Base cases: if n is 0 or 1, return n
    if n in {0, 1}:
        return n
        
    # Recursive case: if n > 1, return sum of the two preceding Fibonacci numbers
    return fib(n - 1) + fib(n - 2)
```

```C file="Recursive Fibonacci"
int fib(int n) { 
    if (n == 0) return 0;
    if (n == 1) return 1;

    return fib(n - 1) + fib(n - 2);
}
```

However, Fibonacci tree-recursion is *inefficient* because it recalculates the same values multiple times. That is, the recursion computes the same subproblems repeatedly:

![[fibonacci recursion tree.png|Recursion tree for fib(5). The colored subproblems represent repetitive solutions to the same problem. If you go further up the tree, you’ll find more of these repetitive solutions.]]
If we draw the recursion tree for `F(n) = F(n-1) + F(n-2)`, we can see that `fib(5)` is calculated 2 times and `fib(3)` is calculated 3 times. So using recursion, we are actually doing redundant computations.

![How to calculate the fifth Fibonacci number|center|400](https://files.realpython.com/media/mwong-fib5.afb4734df50f.png)


**Analysis**
- The depth[^3] of the tree is $n$.
- The total number of recursive calls is $2^n$ — at each level, the number of calls doubles because each call spawns 2 more calls.
- The work done at each call is constant — base case checks on the value of $n$ and a final addition.

> [!time]- Alternative time analysis
> Let $T(n)$ be the number of computer steps needed to compute `fib(2)`.
>
> If $n$ is less than $2$, we are at the base case so the function returns immediately.
> Therefore, $T(n) \leq 2$ for $n \leq 1$.
>
> For larger values of $n$, there are 2 recursive invocations of `fib(n)`, taking time $T(n-1)$ and $T(n-2)$ respectively plus 3 computer steps for constant work (base case checks on the value of $n$ and a final addition). Therefore, $T(n) = T(n-1) + T(n-2) + 3$ for $n > 1$.
>
> Compare this to the recurrence relation for $F(n)$. We can see that $T(n) \geq F(n)$. This is very bad news: the running time of the algorithm grows as fast as the Fibonacci numbers!
>
> ***
> The leaves of the recursion tree will always return 1. The value of `fib` is sum of all values returned by the leaves in the recursion tree which is equal to the count of leaves. Since each leaf will take O(1) to compute, `Fib(n)` is equal to `T(n)`.
>
> As a result, you can skip directly to the very close approximation of the Fibonacci series:
>
> ```
> Fib(N) = (1/sqrt(5)) * 1.618^(N+1) (approximately)
> ```
>
> and say, therefore, that the worst case performance of the naive algorithm is
>
> ```
> O((1/sqrt(5)) * 1.618^(N+1)) = O(1.618^(N+1))
> ```
>
**Exponential Time Complexity**
$T(n)$ is exponential in $n$, which implies the algorithm impractically slow except for very small values of $n$.


> [!maths|outlined] Time and Space Complexity
> - Time complexity is `O(2^n)` since every call will split into two calls, each with O(1) work.
> - Space complexity is `O(n)` since the depth of the tree will be proportional to the size of `n`.
#### Iterative Solution: `O(n)` (linear time)
#dynamic_programming #bottom-up

Instead of breaking down the problem recursively, we can iteratively build up the solution by calculating Fibonacci numbers from the bottom up. That is, we loop from i = 0 to n and use variables to store the previous 2 values in the sequence.

This avoids the repeated calculations of the recursive approach.

```c
int fib(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    
    int prev2 = 0;      // first Fib number
    int prev1 = 1;      // second Fib number
    int current;        // current Fib number (where n is the current number in the loop)
    
    /*
    Since we already know the first two numbers in the sequence,
    we start the loop from 2 (skip the first 2 numbers) ...
    and go up to n (n-th number)
    */
    
    for (int i = 2; i <= n; i++) {
        current = prev1 + prev2;
        prev2 = prev1;      // update prev2 to the next number (prev1)
        prev1 = current;    // update prev1 to the next number (current)
    }

    return current;
}
```

> [!maths|outlined] Time and Space Complexity
> - Iteration takes `O(n)` time as it iterates from `i=2` to `n`.
> - The space complexity is `O(1)` since it only uses variables

```python
def fibonacci(n):
    # Base cases
    if n in {0, 1}:
        return n

    # Iterate from 2 to n (inclusive)
    prev, curr = 0, 1
    for _ in range(2, n + 1):
        prev, curr = curr, prev + curr

    return curr
```

## Recursive Data Structures
A **recursive (recursively-defined) data structure** is a data structure that can be defined using itself. For example, [[linked list]] and [[binary tree]] are recursive data structures.

![[recursive structures.png|A linked list is recursively defined as an object (node) referencing a list (or null).]]

> [!col]
>
> > [!div]
> > A [[linked list]] is a recursive data structure because a list can be defined as either
> > (1) an empty list or
> > (2) a node followed by a list.
> >
> > ```C  file="C definition of a linked list node" hlt:3|s:;
> > struct node {
> >   int data;           // some integer data
> >   struct node *next;  // pointer to another struct node
> > };
> > ```
> > *Note*: the node is defined in terms of itself.
>
>
> > [!div]
> > A [[binary tree]] is typically defined as
> > (1) an empty tree or
> > (2) a node pointing to two binary trees, one its left child and the other one its right child.
> >
> > ```C file="C definition of a binary tree node" hlt:3-4|s:;
> > struct node {
> >   int data;            // some integer data
> >   struct node *left;   // pointer to the left subtree
> >   struct node *right;  // point to the right subtree
> > };
> > ```
> > *Note*: the binary tree node is defined in terms of itself.
> >

## Recursive Helper Functions
Sometimes, recursive solutions require *recursive helper functions* (i.e., we can't call the function itself) because:
- Recursive function needs to take keep track of extra information (states) or specific conditions.
	- For example: **counters**, **accumulators**, **references to a specific node** etc.
- Data structure uses a [[data structures & algorithms/appendix/glossary#wrapper|wrapper class/struct]]

> [!details]-
> Often in this course, a list will be represented by two structures, one for the usual list node, and one which contains a pointer to the head of the list (along with other data about the list such as its size), usually called a wrapper or container struct.
>
> In this case, since we want to recurse on the nodes, not the wrapper struct, we need to implement a helper function which takes in a node pointer and then call it from the original function. For example:
>
> ```c
> int listFunc(struct list *list) {
> 	return listFuncHelper(list->head);
> }
> ```

<u>Components</u>
- **Primary Method**: Sets up the necessary starting conditions or parameters for the recursion and then calls the helper method.
- **Helper Method:** Containing the recursive logic, this method is called by the primary method. It often includes additional parameters that assist in the recursion process.

> [!info|no-title]
> Our convention for naming recursive helper functions is to prepend ”do” to the name of the original function.
### Wrappers and Helpers

``````col
borderWidth=0
textAlign=start
height=shortest
===
`````col-md
flexGrow=0.75
===
Consider this list representation:

```C hlt:4,9
// Node struct
struct node {
    int value;
    struct node *next; 
};

// List struct
struct list {
    struct node *head;
};
```
`````

`````col-md
flexGrow=1
===
**Problem**: Implement this function

```C
void listAppend(struct list *list, int value);
```

- ! We can't recurse with this function because our recursive function needs to take in a `Node` (not a `List`)
- ! We can't recurse on the list itself, because the list struct doesn't contain a pointer to the next node. i.e. we can't call `listAppend` on `list->next` because it doesn't exist

`````
``````

**Solution**: Use a recursive helper function

```C hlt:2|do:;,6
void listAppend(struct list *list, int value) {
    list->head = doListAppend(list->head, value);
}

// helper function: accepts a struct node (list->head) 
struct node *doListAppend(struct node *node, int value) {
    if (node == NULL) {
        return newNode(value);
    } else {
        node->next = doListAppend(node->next, value);  // recursive call
        return node;
    }
}
```

> [!example|blue]- Example: Linked List Wrapper Class in Python
>
> ```python file="Linked List representation in Python"
> # Node class
> class Node:
>     def __init__(self, data):
>         self.data = data
>         self.next = None
> 
> 
> # Linked List class - wrapper for the head node
> class LinkedList:
>     def __init__(self):
>         self.head = None
> ```
>
> ```python info:4-9, ins:12
> def append_to_list(list, data):
>     # Helper function: takes in a Node (not a LinkedList) 
>     # and performs the recursive append operation
>     def do_append_to_list(node, data):
>         if not node:
>             return Node(data)
> 
>         node.next = do_append_to_list(node.next, data)
>         return node
> 
>     # Primary function: call the helper function with the head of the list
>     list.head = do_append_to_list(list.head, data)
> ```
### Passing extra information

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1.5
===
**Problem:** Print a linked list in a numbered list format, starting from 1.

```c 
void printNumberedList(struct node *list);
```

- ! We need to keep track of the list number.
- ! Each recursive call needs to know the list number to print but we can't pass it as an argument.

`````

`````col-md
flexGrow=1
===
**Example:** Suppose the input list contains the following elements: `[11, 9, 2023]`.

We expect the following output:

```
1. 11
2. 9
3. 2023
```
`````
``````

**Solution**: Use a recursive helper function that takes the current number as an argument.

```c hlt:'int count' impt:count:1
void printNumberedList(struct node *list) {
    doPrintNumberedList(list, 1);  // call the helper with the initial count
}

void doPrintNumberedList(struct node *node, int count) {
    if (node == NULL) return;

    printf("%d. %d\n", count, node->value);
    doPrintNumberedList(node->next, count + 1); // increment count for next node
}
```

```python info:3-8 hlt:index:1,3|index ins:10
def print_numbered_list(list):

    def do_print_numbered_list(node, index):
        if not node:
            return

        print(f"{index}. {node.data}") 
        do_print_numbered_list(node.next, index + 1) 

    do_print_numbered_list(list.head, 1)
```

[^1]: Each subpart is enclosed in parenthesis `()`
[^2]: We can use recursion to solve this problem because any Fibonacci number `n` depends on previous two Fibonacci numbers `n-1` and `n-2`. Therefore, this approach repeatedly breaks down the problem until it reaches the base cases.
[^3]: Count the number of levels (including level 0 which is the root).