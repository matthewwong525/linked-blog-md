---
cssclasses:
  - table-formatted
  - col-fit-content
  - first-col
---
> [!quote|no-title]
> "Big O notation is a mathematical notation that describes the *limiting* behavior of a function when the argument tends towards a particular value or infinity."
>
> <p align="right">— Wikipedia’s definition of Big O notation</p>

Big-O notation describes the *upper-bound* [[data structures & algorithms/appendix/glossary#asymptotic|asymptotic behaviour]] of an algorithm's [[data structures & algorithms/appendix/glossary#growth rate|growth rate]]. It is denoted as a **function** of the **input $n$** for some particular [[data structures & algorithms/appendix/glossary#best, worst, and average cases|case]].

In other words, given an input of size $n$ for some particular class (worst-, average-, or best-case), the Big-O notation represents the maximum amount of resources[^1] the algorithm will require to find a solution.

> [!note|no-title]
> Recall that the complexity isn't always dependent on the input size. Some algorithms like searching algorithms depend on the distribution or order of input for a given size. For example, binary or insertion sort performs better on sorted input. Therefore, it is important we analyses the different cases for such inputs.

The “O” in Big O Notation stands for “order of” the function and refers to the upper bound of the growth rate.

For example, an algorithm with $T(n) = O(1)$ means that its runtime does not change as the input size increases. It will execute the same number of operations regardless of the input size.
## Asymptotic Analysis
To determine the growth rate, we look at how the algorithm scales as the input size increases, and express that as a function. Then, we simplify the function according to these rules to get the big-O notation:
## Simplifying Rules
1. If some function $g(n)$ is an upper bound for your cost function, then any upper bound for $g(n)$ is also an upper bound for your cost function.
2. Ignore any constant factors and lower-order terms for the growth rate.
3. Focus on the dominant terms with the fastest growth rate. Given 2 parts of the program run in sequence [^2] (whether 2 statements or 2 sections of code), you only need to consider the more expensive part.
4. If some action is repeated some number of times, and each repetition has the same cost, then the total cost is the cost of the action multiplied by the number of times that the action takes place. — **used to analyse loops**.
	- time complexity of the loop $=$ # loop iterations in the worst-case $\times$ # work done at each iteration

> [!pin|yellow] Key Points
> 1. Lower-order terms becomes insignificant as the input size $n$ increases
> 2. Growth rate is unaffected by constant factors [^3]
> 3. Higher-order terms (with the highest exponent) becomes significant as the input size $n$ increases.
## Best Practices
1. Consider the worst-case scenarios

Common Mistakes
1. Using Big O Notation to compare algorithms that have different input sizes.

## Orders of Growth
The big-O notation is a convenient notation because it hides the constant factor and ignores low-order terms, making it easy to compare the efficiency of algorithms,


| Notation                                                            | Name        | Explanation                                                                  |
| ------------------------------------------------------------------- | ----------- | ---------------------------------------------------------------------------- |
| <span style="font-family: 'Source Serif 4'">O(1)</span>             | constant    |                                                                              |
| <span style="font-family: 'Source Serif 4'">O(log n)</span>         | logarithmic | At each step, the problem size decreases by a constant factor (e.g. halves)  |
| <span style="font-family: 'Source Serif 4'">O(n)</span>             | linear      |                                                                              |
| <span style="font-family: 'Source Serif 4'">O(n log n)</span>       | log-linear  |                                                                              |
| <span style="font-family: 'Source Serif 4'">O(n<sup>2</sup>)</span> | quadratic   |                                                                              |
| <span style="font-family: 'Source Serif 4'">O(n<sup>3</sup>)</span> | cubic       |                                                                              |
| <span style="font-family: 'Source Serif 4'">O(2<sup>n</sup>)</span> | exponential | At each step, the problem size increases by a constant factor (e.g. doubles) |
| <span style="font-family: 'Source Serif 4'">O(n!)</span>            | factorial   |                                                                              |
> [!pin|teal|no-title]
> Note that *log* here means *log2* or the logarithm base 2, although the logarithm base doesn't really matter since logarithms with different bases differ by a constant factor and Big-O notation is a rough approximation rather than mathematically precise.

**Logarithmic Growth = Exponential Decrease**
If you reduce the problem size (n) by a constant factor each step:
$$n \to n/2 \to n/4 \to n/8 \to \ldots \to 1$$
The number of steps k to reduce n to 1 is k = log(n).

Examples include binary search.

```c hlt:1|*=,3|/=
for (int i = 0; i < n; i *= 2)
// same as
for (int i = n; i > 0; i /= 2)
```

```c
void recurse(int n) {
    // some base case
    if (n <= 0) return;

    // O(1) work
    recurse(n/2); // Problem size halves each step/level => logarithmic
}
```

**Exponential Growth**
If you increase the problem size (n) by a constant factor (e.g. squared, cubed) each step:
$$n \to n^2 \to n^4 \to n^8 \to \ldots \to m$$
The number of steps k is increase n to m is k = 2<sup>n</sup>.

```c
int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n-1) + fibonacci(n-2); // each call spawns 2 more calls
}
```

![[big-o-cheatsheet.pdf]]

[^1]: i.e. number of steps
[^2]: Sequence means sequential execution; one runs after another.
[^3]: Note that this is not always the case. In rare situations, such as comparing algorithms that run on small input sizes of n, the constants can have a large impact.