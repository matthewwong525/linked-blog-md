---
cssclasses:
  - table-formatted
  - column-nowrap
  - second-col
---
The running time of an algorithm can be analysed in 2 ways:

1. **Empirically**: Measure the time that a program implementing the algorithm takes to run. See [[empirical analysis]]. 
2. **Theoretically**: Counting the number of basic operations performed by the algorithm as a function of input size.
## Theoretical Analysis
Time complexity expresses the **number of operations or steps** needed for an input of size $n$ as a **function**.

We usually express time complexity using [[big O notation]]. That is, we find the *maximum* number of operations performed in the *worst-case* scenario, in terms of its input size.

1. **Count the basic operations**
2. **Express the growth rate w.r.t the input size**: Determine how the number of operations changes as the input size increases or changes.
3. **Determine the Big O notation**: Leave the dominant terms. Ignore/remove any constants, coefficients and lower order terms (the terms with lower exponents).

![[big O notation#Simplifying Rules]]
## Basic Operations
Basic operations take constant time, denoted as $O(1)$, since the time taken doesn’t depend on the input size. The following operations take exactly one time step:

- Arithmetic operations (`x + y`, `x * y`, `i++`, `i--`, etc.)
- Logic/comparison operations (`<`, `>`, `==`, etc.)
- Statements like `if` or `return`
- Accessing a memory location, such as writing or reading a variable:
	- Assignment of a variable (`i = 0`)
	- Array access/Indexing into an array (`A[i]`)

These operations are called basic or primitive operations because the number of basic operations is *constant* (always the same) regardless of the input size $n$.

Since growth rate is not affected by constant factors, instead of counting basic operations we can simply count the number of **line executions**.
## Time Complexity Analysis
- Loops are analysed by counting the number of iterations in the worst case. 
- For nested loops, we count the total number of times the inner loop executes. 
- The cost of an `if` statement in the worst case is the greater of the costs for the `then` and `else` clauses.
- For `switch` statements, the worst-case cost is that of the most expensive branch.
- For subroutine calls, simply add the cost of executing the subroutine.


> [!EXAMPLE]-
> For example, consider this pseudocode for linear search:
>
> ```
> linearSearch(A, key):
>     Input: array A of size n, key to search for
>     Output: index of key in A, or -1 if not found
> 
>     for i from 0 to n - 1:     
>         if A[i] == key:        
>             return i
>     return -1                   
> ```
>
> > [!answer]
> > > [!col]
> > > > [!div]
> > > > Instead of counting each basic operation:
> > > > ```
> > > > for i from 0 to n - 1:      1 + (n + 1) + n
> > > > 	if A[i] == key:         2n
> > > > 		return i
> > > > return -1                   1
> > > > 							------
> > > > 							4n + 3
> > > > ```
> > > > Linear search requires $4n + 3$ basic operations in the worst case.
> > > > Therefore, time is $O(n)$ in the worst case.
> > > >
> > > > > [!maths|black]- Explanation
> > > > > Assuming the for loop is implemented as:
> > > > >
> > > > > ```infot:'i = 0' impt:'i < n' warnt:'i++'
> > > > > for (int i = 0; i < n; i++)
> > > > > ```
> > > > >
> > > > > - There is <mark class="grey">1 assignment</mark>, <mark class="orange">n increments</mark> and ==(n + 1) checks of the condition== (Including the last failed check when `i = n`).
> > > > > - Note that we assume the worst case scenario where key is not found in the array.
> > > > >
> > > > > ```inst:A[i] hlt:'=='
> > > > > if A[i] == key:
> > > > > 	return i
> > > > > ```
> > > > >
> > > > > In the worst case (key not found), only the condition of the if statement is executed.
> > > > >
> > > > > This conditional expression has $2$ basic operations: ==1 array access== and <mark class="orange">1 equality check</mark>
> > > > > and runs $n$ times (once for each element).
> > > > >
> > > >
> > >
> > > > [!div]
> > > > We can count the number of loop iterations $\times$ work done on each iteration:
> > > >
> > > > ```
> > > > for i from 0 to n - 1:      executes n times
> > > > 	if A[i] == key:         1
> > > > 		return i
> > > > return -1                   1
> > > > 							------
> > > > 							n
> > > > ```
> > > > Loop has at most N iterations in the worst case.
> > > > Loop does O(1) work each iteration.
> > > > Therefore, linear search is $O(n)$ in the worst case.
>

> [!example]-
>
> ```c 
> sum = 0;
> for (i = 1; i <= n; i++) { 
>    sum += n;
> }
> ```
>
> > [!answer]-
> >
> > ```c ln=true
> > sum = 0;  // O(1)
> > for (i = 1; i <= n; i++) {  // executes n times
> >    sum += n;  // O(1) * n 
> > }
> > ```
> >
> > - The first line is $O(1)$.
> > - The `for` loop is repeated $n$ times. The third line takes constant time so, by [[big O notation#Simplifying Rules|rule (4)]], the total cost for executing the two lines making up the `for` loop is $O(n)$.
> > - The total cost is $O(1) + O(n)$ which simplifies to $O(n)$.
>

> [!example]
>
> ```hlt:i<=n delt:j<=n,j<=i
> sum1 = 0;
> for (i=1; i<=n; i++)     // First double loop
>    for (j=1; j<=n; j++)  //   do n times
>       sum1++;
> 
> sum2 = 0;
> for (i=1; i<=n; i++)     // Second double loop
>    for (j=1; j<=i; j++)  //   do i times
>       sum2++;
> ```
>
> In the first double loop, the inner loop *always* executes $n$ times.
> Because the outer loop executes $n$ times, ==`sum1++` is executed precisely $n^2$ times===.
>
> In the second double loop, the inner loop executes $i$ times.
> The outer loop executes $n$ times, but each time the cost of the inner loop is different with $i$ changing each time, from $i=1 \ldots n$.
>
> For the first execution of the outer loop, $i = 1$. For the second execution of the outer loop, $i = 2$. Each time through the outer loop, $i$ becomes one greater, until the last time through the loop when $i = n$.
>
> Therefore the total cost of the `sum2++` is the sum of the integers 1 through $n$. We known that $\sum_{i=1}^{n}i = \frac{n(n+1)}{2}$. ==Thus `sum2++` is executed approximately $\frac{1}{2}n^2$ times==.
>
> > [!alert|no-title]
> > **Important**: Although both double loops cost $O(n^2)$, the second one requires about half the time of the first => $\frac{1}{2}n^2$ vs $n^2$.
>

#TODO 
> [!example]
> ```hlt:j<=n,j<=k
> sum1 = 0;
> for (k=1; k<=n; k*=2)    // Do log n times
>    for (j=1; j<=n; j++)  // Do n times
>       sum1++;
> 
> sum2 = 0;
> for (k=1; k<=n; k*=2)    // Do log n times
>    for (j=1; j<=k; j++)  // Do k times
>       sum2++;
> ```
> 
> Assume that $n$ is a power of two. In the first double loop, the outer for loop is executed $\log n + 1$[^1] times because on each iteration, $k$ is multiplied by 2 until it reaches $n$. Because the inner loop always executes $n$ times, the total cost for the double loop can be expressed as:
> $$\sum_{i=0}^{\log n} n = n \log n.$$
> So the cost of this first double loop is $O(n \log n)$. Note that a variable substitution takes place here to create the summation, with $k = 2^i$.
> 
> In the second double loop, the outer loop is also executed $\log n + 1$ times. The inner loop has a cost $k$, which doubles each time. The summation can be expressed as:
> $$\sum_{i=0}^{\log n} 2^i = O(n).$$
> where $n$ is assumed to be a power of two and again $k = 2^i$.
> 
> > [!maths|gray]- Explanation
> > In the outer loop, $k$ starts at 1 and doubles in each iteration:
> > 
> > | Iteration | Loop Counter (before update) |
> > | --------- | ---------------------------- |
> > | 1         | $k = 2^0 = 1$                |
> > | 2         | $k = 2^1 = 2$                |
> > | 3         | $k = 2^2 = 4$                |
> > | 4         | $k = 2^3 = 8$                |
> > | $n$       | $k = 2^n$                    |
> > For each value of $k$ (before $k$ doubles), the inner loop executes $k$ times.
> > Therefore, the inner loop executes $1 + 2 + 4 + 8 + \ldots + n$ times. The summation can be expressed as:
> > $$\sum_{k=1}^{n} k = \sum_{i=0}^{\log n} 2^i = 2^{\log n} = O(n).$$
> > Note that the progression of $k$ corresponds to powers of 2 so we can substitute with $k = 2^i$ and represent the iterations with $i$ which grows linearly ($i = 0, 1, 2, \ldots, \log_2 n$). 
> 
> 
## Loops
Approach:
1. Count the total number of loop iterations in the **worst case**
2. Calculate the time complexity of the code in the loop body
3. Time Complexity = # Loop iterations in the worst case $\times$ Work done on each iteration

Another approach:
1. Identify the most critical operation inside the loop, which executes the maximum number of times in the worst case. This critical operation would be the dominating factor in the time complexity function.
2. Now calculate the total count of this operation for the complete loop in terms of input size.

> [!maths|black|outlined] Counting Loop Iterations
> **Exclusive End**:
>
> $$\text{Iterations} = \frac{\text{end} - \text{start}}{\text{step}}$$
> **Inclusive End**:
> $$\text{Iterations (inclusive)} = \left\lfloor \frac{\text{end} - \text{start}}{\text{step}} \right\rfloor + 1$$

```c exclude
for (int i = n; i >= 1; i--)

// equivalent to

for (int i = 1; i <= n; i++)
```

### O(1)
> If the loop condition does not depend on $n$, then the loop runs a constant number of times regardless of the input. The time complexity is always $O(1)$, even if the loop does alot of work.

```c hlt:'i <= c'
for (int i = 1; i <= c; i = i + 1)   // c iterations
```

### O(n)
> If the loop counter is incremented/decremented by a constant amount, it is O(n).

``````col
textAlign=start
===
`````col-md
flexGrow=1
===
n iterations from [0, n)
```c 
for (int i = 0; i < n; i++)
```

n / c iterations
```c
for (int i = 0; i < n; i += c)  
```
`````

`````col-md
flexGrow=1
===
n iterations from [1, n]
```c 
for (int i = 1; i <= n; i++)
```

c $\times$ n iterations
```c 
for (int i = 1; i <= c*n; i++)
```
`````
``````

```c
void recurse(int n) {
    // some base case
    if (n == 0) return;

    // O(1) work
    recurse(n - 1); // problem size reduced by 1 each time: linear O(n)
}
```

### O(log n)
> If the loop counter increments/decrements by a constant factor on each iteration, the <abbr data-title="remaining number of iterations">remaining problem size</abbr> is reduced by that factor for each iteration.
> The total number of iterations decreases exponentially = increases logarithmically.
> Therefore, the loop runs <span style="font-family: 'Source Serif 4'">O(log n)</span> times $\times$ <span style="font-family: 'Source Serif 4'">O(1)</span> operations each step.

```c hlt:*=
for (int i = 1; i <= n; i *= 2)  // runs log n + 1 times
```

```c hlt:/=
for (int i = n; i > 0; i /= 2)   // runs log n times
```

Assume the loop stops after k steps.

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
| Iteration | Loop Counter          |
| --------- | --------------------- |
| 0         | i = 1 = 2<sup>0</sup> |
| 1         | i = 2 = 2<sup>1</sup> |
| 2         | i = 4 = 2<sup>2</sup> |
| 3         | i = 8 = 2<sup>3</sup> |
| k         | i = 2<sup>k</sup>     |
`````

`````col-md
flexGrow=1.75
===
1. The last term must be i $\leq$ n. 
2. Therefore <span style="font-family: 'Source Serif 4'">2<sup>k</sup> $\leq$ n</span>.
3. Taking the log base 2 of both sides: 
	1. $\log_2(2^k) \leq \log_2(n)$
	2. <span style="font-family: 'Source Serif 4'">k $\leq$ log(n)</span>
4. Therefore, the loop runs at most <span style="font-family: 'Source Serif 4'">log(n)</span> times.
`````
``````

The total number of steps is *bounded by* log(n). Therefore, in the worst case, the max number of iterations is log(n).

> [!alert|no-title]
> **Note:** `for (int i = 1; i <= n; i *= 3)` has a time complexity of $O(\log_3 n)$.

Examples: Iterative binary search, find the n-th power of a number, exponential search etc.

> [!maths|grey]- Mathematical Solution
>
> ``````col
> borderWidth=0
> textAlign=start
> ===
> `````col-md
> flexGrow=1
> ===
> Assume the loop stops after k steps.
> 
> | Iteration | Loop Counter                  |
> | --------- | ----------------------------- |
> | 1         | i = n / 2                     |
> | 2         | i = n / 4 = n / 2<sup>2</sup> |
> | 3         | i = n / 8 = n / 2<sup>3</sup> |
> | k         | i = n / 2<sup>k</sup>         |
> `````
> 
> `````col-md
> flexGrow=1.25
> ===
> The loop stop when i > 0 or equivalently i $≥$ 1 so:
> $$
> \begin{align*}
> 	\frac{n}{2^k} &\geq 1 \\
> 	n &\geq 2^k \\
> 	\log_2(n) &\geq \log_2(2^k) \\
> 	\log(n) &\geq k \\
> \end{align*}
> $$
> Therefore, the number of iterations k is log(n).
> `````
> ``````

```c
void recurse(int n) {
    // some base case
    if (n == 0) return;

    // O(1) work
    recurse(n/2); // Problem size halves each step/level => logarithmic
}
```

### O(log(log n))
> If the loop counter increments by a constant factor (e.g. squared, cubed) on each iteration, the loop will run $\log_c(\log(n))$ times.

```c hlt:pow:)
// Here c is a constant greater than 1
for (int i = 2; i <= n; i = pow(i, c))
```

```c hlt:sqrt:)
// Here sqrt or cuberoot or any other constant root
for (int i = n; i > 1; i = sqrt(i)) 
```

At any i-th iteration, the value of i = 2^(c^i).
Loop will end when 2^(c^i) = n.
Total number of iterations = O(log(log(n))).

> [!maths|gray]- Mathematical Solution
> Assume the loop stops after k steps.
>
> | Iteration | Loop Counter                                                        |
> | --------- | ------------------------------------------------------------------- |
> | 0         | 2                                                                   |
> | 1         | 2<sup>c</sup>                                                       |
> | 2         | (2<sup>c</sup>)<sup>c</sup> = 2<sup>c<sup>2</sup></sup>             |
> | 3         | (2<sup>c<sup>2</sup></sup>)<sup>c</sup> = 2<sup>c<sup>3</sup></sup> |
> | k         | 2<sup>c<sup>k</sup></sup>                                           |
> 1. Since i $\leq$ n, we have 2<sup>c<sup>k</sup></sup> = n.
> 2. Taking the log base 2 on both sides, we get c<sup>k</sup> = log(n).
> 3. Taking the log base c of both sides, we get k = log(log n).
>
> Therefore, the total number of steps/iterations k is log(log n).
## Nested Loops
Time complexity = Total number of inner loop iterations.

> [!example]
> Total number of iterations = n $\times$ m iterations
>
> ```c exclude
> for (int i = 0; i < n; i++) {  // n
>     for (int j = 0; j < m; j++) { // m
> ```
>
> Outer loop runs N times. For each outer loop iteration, the inner loop runs M times.
> Inner loop runs a total of N $\times$ M times => total number of iterations.
### O(n)

```c
for (int i = 0; i < n; i++)
	for (int j = i; j < i + 5; j++)
```

Nested loop runs at most k (a constant) times for each iteration of the outer loop, yielding a complexity of O(n k), which is O(n).
### O(n^2)
#### independent loops

```c hlt:'i <= n' impt='j <= n'
for (int i = 1; i <= n; i += c) // n times
    for (int j = 1; j <= n; j += c) // n times
```

```c hlt:'i = n' impt:'j <= n'
for (int i = n; i > 0; i -= c) // n times
	for (int j = i + 1; j <= n; j += c) // n times
```

Outer loop executes n times. For each outer loop iteration, the inner loop *always* executes n times. Therefore, the total count of inner loop iterations is O(n<sup>2</sup>).
#### dependent loops

```c
for (int i = 1; i <= n; i++)  // n times
	for (int j = 1; j <= i; j++)  // i times where i = 1, 2, 3, ..., n
```

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=0.8
===
> [!trend-increasing|black|outlined] Pattern
> If <span style="font-family: 'Source Serif 4'">i = 1</span>, inner loop runs <span style="font-family: 'Source Serif 4'">1</span> time
> If <span style="font-family: 'Source Serif 4'">i = 2</span>, inner loop runs <span style="font-family: 'Source Serif 4'">2</span> times
> If <span style="font-family: 'Source Serif 4'">i = 3</span>, inner loop runs <span style="font-family: 'Source Serif 4'">3</span> times
> <span style="font-family: 'Source Serif 4'">...</span>
> If <span style="font-family: 'Source Serif 4'">i = n</span>, inner loop runs <span style="font-family: 'Source Serif 4'">n</span> times
`````

`````col-md
flexGrow=1
===
1. Outer loop runs <span style="font-family: 'Source Serif 4'">n</span> times, <em>incrementing <span style="font-family: 'Source Serif 4'">i</span> each time</em>.
2. Inner loop runs <span style="font-family: 'Source Serif 4'">i</span> times, <em>for each value of <span style="font-family: 'Source Serif 4'">i</span></em>.
`````
``````

<u>Solution 1</u>
For each outer loop iteration, the inner loop runs i = N times.
Total number of inner loop iterations = N $\times$ N = N<sup>2</sup>.

<u>Solution 2</u>
Total number of inner loop iterations = <span style="font-family: 'Source Serif 4'">1 + 2 + 3 + ... + n</span> = sum of integers from <span style="font-family: 'Source Serif 4'">1</span> to <span style="font-family: 'Source Serif 4'">n</span>.
This is the [sum of arithmetic series](https://en.wikipedia.org/wiki/Arithmetic_progression#Sum):

$$\sum_{i=1}^{n}i = \frac{n(n+1)}{2},$$
which is approximately $\frac{1}{2}n^2$. Thus the total cost of the loop is $O(n^2)$.

```c
for (int i = 0; i < n; i++)  // n times
    for (int j = i + 1; j < n; j++)  // n - (i + 1) times, where i = 0, 1, 2, ..., n-1
```

Outer loop runs <span style="font-family: 'Source Serif 4'">n</span> times.
For every outer loop iteration, inner loop runs <span style="font-family: 'Source Serif 4'">(n – i – 1)</span> times.
Total nested loop iterations <span style="font-family: 'Source Serif 4'">= (n – 1) + (n – 2) + (n – 3) + ... + 1 + 0 = n(n – 1) / 2 = O(n<sup>2</sup>)</span>.

```c
for (int i = 1; i <= n; i++) // n times
    for (int j = n; j >= i; j--) // n - i times, where i = 1, 2, 3, ..., n
```

Outer loop runs <span style="font-family: 'Source Serif 4'">n</span> times.
For each outer loop iteration, the inner loop runs <span style="font-family: 'Source Serif 4'">n - i</span> times.
Total nested loop iterations = (n - 1) + (n - 2) + ... + 0 = O(n<sup>2</sup>).
### O(n logn)

```c
for (int i = 0; i < n; i++)
	for (int j = 1; j < n; j*=2)
```

Outer loop runs n times. Inner loop runs log(n) times for each iteration of the outer loop.
This would give a complexity of O(n logn).

```c
for (int i = 0; i < n; i*=2)
	for (int j = 1; j < n; j++)
```

Outer loop runs log n times. Inner loop runs n - 1 times. Total nested loop iterations = O(n logn).
### O(n^3)

```c
for (int i = 1; i < n; i++) {           // Outer loop
    for (int j = i + 1; j < n; j++) {   // Middle loop
        for (int k = i; k <= j; k++) {  // Inner loop
            // O(1) work
        }
    }
}
```

```c
for (int i = 1; i < n; i++)             // n - 1 times
    for (int j = i + 1; j < n; j++)     // n - (i + 1) times
        for (int k = i; k <= j; k++)    // j - i + 1 times
```

1. Outer loop runs <span style="font-family: 'Source Serif 4'">n – 1</span> times.
2. Middle loop runs <span style="font-family: 'Source Serif 4'">n – i – 1</span> times, where <span style="font-family: 'Source Serif 4'">i = 1</span> to <span style="font-family: 'Source Serif 4'">n – 1</span>.
3. Inner loop runs <span style="font-family: 'Source Serif 4'">j – i + 1</span> times, where <span style="font-family: 'Source Serif 4'">i = 1</span> to <span style="font-family: 'Source Serif 4'">n – 1</span> and <span style="font-family: 'Source Serif 4'">j = i + 1</span> to <span style="font-family: 'Source Serif 4'">n – 1</span>.

The total number of iterations is the sum of inner loop iterations across all values of i and j:

$$\text{Total Iterations} = \sum_{i=1}^{n-1} \sum_{j=i+1}^{n-1} \sum_{k=i}^{j} 1
= \sum_{i=1}^{n-1} \sum_{j=i+1}^{n-1} (j - i + 1)
= O(n^3)$$









[^1]: Note the $+1$ accounts for when $k=n$, the condition $k \leq n$ is still true so the loop executes for this case as well.