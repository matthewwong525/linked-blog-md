Analysis of an algorithm is the process of finding the resource consumption or "complexity" of algorithms —the amount of *time* and *space* needed to execute them.
## Motivation: Program Efficiency
Many factors affect the running time of a program — the operating system, hardware, load on the machine etc — but most importantly, it depends on the *space* required for [[data structures & algorithms/appendix/glossary#data structure|data structures]] and the *time* required for [[algorithms]] to run.

Therefore, algorithm efficiency is a critical factor in determining the performance of your program. The efficiency of algorithms impacts the speed at which your code executes and the amount of system resources it consumes. Efficient algorithms are required in order for computers to meet our computational needs.
## Algorithm Complexity
Algorithm complexity is the amount of resources — how much *time* and *space* — an algorithm requires to solve a problem.

An <i>efficient</i> algorithm is one that uses the <i>least amount of resources possible</i> (in terms of time and space) while still producing the correct answer.
## Time vs Space Complexity
The 2 most common measures of resource usage (complexity) are:

- **Time complexity** — how much computational time taken by an algorithm to run
- **Space complexity** — how much space or memory needed by an algorithm to run

Note that time and space are often at odds with each other; optimising an algorithm to be quicker often requires taking up more memory, and decreasing memory usage can often make the algorithm slower. This is known as the space-time tradeoff.
## Complexity as a Function of Input Size
We usually try to estimate the amount of time it takes to run an algorithm (or the amount of space usage) as a **function** of its **input size**. In other words, its growth rate. This is called [[asymptotic analysis]].

Since an algorithm's complexity (running time) may vary among different inputs of the same size, we also consider the [[#Best, Worst, and Average Cases|best, worst, and average cases]] of such inputs. 

For example. inputs of size $n$ can differ in **order** (sorted vs reverse-sorted). Some sorting algorithms perform better on sorted input while others perform better on input that is reverse-sorted. 

Therefore, if an algorithm’s growth rate for the worst-case input is $f(n)$, then $f(n)$ is the worst-case complexity. 
## Best, Worst, and Average Cases
For a problem with a given input of size $n$, we can determine its best, average, and worst case scenarios:

- **Best Case**: the least amount of resource the algorithm takes to run
	- describes an algorithm's behaviour under optimal conditions
	- e.g. the best case for linear search on a list is when the desired element is the first element in the list

- **Average Case**: the average amount of resources over all inputs of size n
	- describes the typical behaviour of the algorithm on different types of data
	- gives the average amount of resources the algorithm uses on a random input

- **Worst Case**: the maximum amount of resource needed over all inputs of size n
	- most important! the worst case analysis gives a <i>safe</i> analysis
	- gives an *upper bound* on the resources required
	- determined from the worst case inputs to the algorithm.

Generally, we look at the **worst-case (upper-bound) complexity** of an algorithm, since it is important to know how much time might be needed _in the worst case_ to guarantee that the algorithm will always finish on time. The algorithm may very well take less time on some inputs of size n, but it doesn't matter.

A popular alternative to worst-case analysis is average-case analysis. Here we do not bound the worst case time, but try to calculate the expected time spent on a randomly chosen input. This kind of analysis is generally harder, since it involves probabilistic arguments and often requires assumptions about the distribution of inputs that may be difficult to justify. On the other hand, it can be more useful because sometimes the worst-case behavior of an algorithm is misleadingly bad. A good example of this is the popular quicksort algorithm, whose worst-case running time on an input sequence of length n is proportional to $n^2$ but whose expected running time is proportional to $n\log n$.

Normally we are not interested in the best case, because best case analysis is not likely to be representative of the behavior of the algorithm. **However, best-case analysis is useful when the best case has high probability of occurring**. For example, [[shell sort]] and [[quick sort]] algorithms both take advantage of the best-case running time of [[insertion sort]] to become more efficient.
## Asymptotic Complexity: Big O, Little O, Omega & Theta
When analysing the running time or space usage of an algorithm, we usually focus on the behavior of the complexity when the input size increases—that is, the *asymptotic* behavior of the complexity.

For a function $f(n)$ the _asymptotic_ behavior is the growth of $f(n)$ as n gets large.

Small input values are not considered. 

There are a few different notations used to describe the asymptotic complexity:

- **Big-O Notation** **O()**: Upper-bounds; the worst-case scenario
- **Theta Notation Θ()**: Tight/exact bounds
- **Omega Notation Ω()**: Lower bounds; the best-case scenario
- **Little-O Notation o()**: Upper bound excluding the exact bound.

## Amortised Analysis
#TODO
Amortised analysis is a method of analysing the costs associated with a data structure that averages the worst operations out over time. It looks at the total cost for a series of operations and amortizes this total cost over the full series. This is as opposed to considering every individual operation to independently have the worst case cost, which might lead to an overestimate for the total cost of the series.
## Theoretical vs Empirical Analysis
The resource usage (complexity/cost) of an algorithm can be analysed in 2 ways:

1. **Empirically**: Program the algorithms and measure their running times. 
	- [Linux `time` command](https://www.geeksforgeeks.org/time-command-in-linux-with-examples/)
	- [Python `timeit` module](https://docs.python.org/3/library/timeit.html)

2. **Theoretically**: Estimate the complexity function for arbitrarily large input; this describes the asymptotic (upper-bound) performance of an algorithm. Typically, this is expressed using [[big O notation]].
	- pros this is preferred method because it has the advantage of being ==machine and data-type independent==
	- cons asymptotic complexity analysis allows us to distinguish between $O(n^2)$ and $O(n \log n)$ algorithms, but it **does not help distinguish between algorithms with the same asymptotic complexity**. This is when we would use empirical analysis.

> [!pros] Prefer Theoretical Analysis
> Theoretical analysis provides a way to analyse and predict the efficiency of algorithms in a way that is **independent** of both the language in which we implement them and the hardware in which they’re executed.
> 
> The goal of theoretical analysis isn't to predict the exact runtime of an algorithm for example, but rather to answer these questions:
> - Given two algorithms that solve the same problem, which one is expected to run faster if the same amount of data is provided to both?
> - If we doubled the data provided to the algorithm, how would the execution time be affected? Will it scale linearly and double as well? Will it remain the same? Or something else entirely?





[^1]: inputs of same size can differ in values, order, structure etc.
