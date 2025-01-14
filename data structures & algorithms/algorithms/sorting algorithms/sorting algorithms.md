Sorting algorithms are used to rearrange a given array or list elements according to a comparison operator on the elements. The comparison operator is used to decide the new order of element in the respective data structure. For example, the numerical order is a commonly used sequence but a lexicographical order is also a commonly used sequence type. There are several types of sorting algorithms: quick sort, bubble sort, merge sort, insertion sort, selection sort, heap sort, radix sort, bucket sort among others. Each has its own properties and are suited to specific types of tasks and data.


Elementary sorting algorithms:
- Selection sort
- Bubble sort
- Insertion sort
- Shell sort

More efficient sorting algorithms:
- Merge sort
- Quick sort

Non-comparison-based sorting algorithms:
- Radix sort
- Key-indexed counting sort


Insertion Sort and Bubble Sort are **exchange sorts** — they rely solely on exchanges (swaps of adjacent records). The biggest bottleneck is that only *adjacent* records are compared and swapped. Therefore, the cost of an exchange sort is at best, the total number of steps that the records must move to reach their “correct” location. This is at least the number of [[data structures & algorithms/appendix/glossary#inversions|inversions]] for the record. 

All exchange sorts require $O(n^2)$ in the worst case. Because for the worst-case input (reverse-sorted array), all $n$ records require $n$ steps to move it to the opposite end.


```dataview
TABLE WITHOUT ID
file.link AS "Comparison Sorts",
best, average, worst, adaptive, stable, in-place
FROM "data structures & algorithms/algorithms/sorting algorithms" and !"data structures & algorithms/algorithms/sorting algorithms/theory"
SORT file.name ASC
```

## Motivation
Sorting is important for optimising the efficiency of other algorithms that require sorted input. For example, search and merge algorithms.

Sorting enable faster searching — e.g. binary search.
Sorting provides a useful intermediate for other algorithms — e.g. duplicate detection/removal, merging two collections.
## Sorting Problem
> [!maths|grey] Formal Definition
> Given a set of [[data structures & algorithms/appendix/glossary#record|records]] $r_1, r_2, \ldots, r_n$ with [[data structures & algorithms/appendix/glossary#key|key]] values $k_1, k_2, \ldots, k_n$, the sorting problem is to arrange the records in any order $s$ such that the records have keys obeying the property $k_{s_1} \leq k_{s_2} \leq \ldots \leq k_{s_n}$.
>
> Formally, the output of any sorting algorithm must satisfy two conditions:
> 1. The output is in **monotonic order** (each element is no smaller/larger than the previous element, according to the required order).
> 2. The output is a **permutation** (a reordering, yet containing all of the original elements) of the input.

In other words, the sorting problem is to arrange a **collection of items**[^1] so that their items are in **non-decreasing order**.

Items are sorted based on their **key** — a field, property or the entire item itself if it is a value, used for the purpose of searching or comparing.

Note that the sorting problem allows for duplicate keys values — all sorting algorithms can handle input with two or more records that have the same key value. However, we might want to maintain

The order for sorting is defined by the comparison operator or comparison function used in the actual implementation of the algorithm. The sorting algorithm itself only defines the steps to perform the sorting; the specific order depends on how comparisons are made.

The most frequently used orders are numeric order and lexicographical order, either ascending or descending.
## Sorting Properties
Sorting algorithms can be classified by whether they have the following properties:

- [[stability]]: stable sorting algorithms maintain the relative order of records with equal/duplicate keys.
- [[adaptability]]: adaptive sorting algorithms sort faster on nearly- or pre-sorted input.
- [[in-place]]: in-place sorting algorithms do not use extra memory; they directly sort and modify the input data in-place without creating temporary arrays.
## Sorting Analysis
When analysing sorting algorithms, we want to count the number of the **swap and comparison operations**, which are the main/key operations that perform the sorting. 

Count the number of:
- ==Swaps==: swaps made between records 
- ==Comparisons==: comparisons made between keys (with a comparison operator)

Assumptions:
- Records (input) are of a fixed length $n$. 
- All records and keys are of fixed length (i.e. constant).
- All comparisons and swaps take constant time.

Input Cases (Best, Worst, Average):
- Random order
- Sorted order
- Reverse-sorted order




[^1]: Can be any collection of items like arrays, linked lists, etc.
