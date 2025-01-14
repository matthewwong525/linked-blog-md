---
adaptive: true
stable: true
in-place: true
tags:
  - adaptive
  - stable
  - in-place
memory: $O(1)$
best: $O(n)$
average: $O(n^2)$
worst: $O(n^2)$
links: https://opendsa-server.cs.vt.edu/ODSA/Books/CS3/html/InsertionSort.html
cssclasses:
  - table-array
method: exchange
---
## Insertion Sort
> **Best Time**: $O(n)$ comparisons and $O(1)$ swaps
> **Average & Worst Time**: $O(n^2)$ comparisons and swaps

#adaptive #stable #in-place

Step through the array, growing the sorted list behind. At each array-position, check the value to the left. If the left is larger, find the correct position within the sorted list, shifting all larger values up to make space, and insert it into the correct position.

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1.5
===
```
void insertionSort(int[] A) {
  n = A.length
  for (int i=1; i<n; i++) 
    for (int j=i; (j>0) && (A[j] < A[j-1]); j--)
      swap(A, j, j-1);
}
```
`````

`````col-md
flexGrow=1
===
![](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)
`````
``````

Insertion sort compares elements to find their correct position. On each pass, we are finding the correct position for the $i$-th key amongst the already sorted $i-1$ elements on the left. On the final pass after the last element is inserted, the array is sorted.

![[insertion-sort.png|Each pass builds the final sorted array, one item at a time.]]



## Notes
- insertion sort is one of the fastest algorithms for sorting very small arrays, even faster than quicksort. Good quicksort implementations use insertion sort for arrays smaller than a certain threshold (threshold is commonly around 10).
- Insertion sort's cost goes up in proportion to the number of [[data structures & algorithms/appendix/glossary#inversions|inversions]]. Thus, insertion sort is **adaptive** (fast) for sorted or nearly sorted input, but inefficient for reverse-sorted and large arrays.
- Insertion sort is more efficient than other $O(n^2)$ sorts such as [[selection sort]] and [[bubble sort]].
## Properties
- [x] **Stable**: Elements are always inserted to the right of any equal elements
- [x] **Adaptive** : Insertion sort is $O(n^2)$ on average, but $O(n)$ if input is sorted. 
- [x] **In-place**: Sorting is done within original array, through swaps.

The time complexity is $O(kn)$ when each element in the input is no more than $k$ places away from its sorted position.
## Analysis
1. The outer loop picks a value to be sorted. It skips the first value and runs $n-1$ times through the unsorted part of the array, from `a[1]` to `a[n-1]`.
2. The inner loop goes through the sorted part of the array, to find where to insert the value The sorted part of the array starts on the **left**, from `a[i]` to `a[i-1]`.
```info:2-3
void insertionSort(int[] A) {
  for (int i=1; i<A.length; i++) // Insert i'th record
    for (int j=i; (j>0) && (A[j] < A[j-1]); j--)
      swap(A, j, j-1);
}
```

> [!summary]- Algorithm Steps
> - Outer loop executes $n-1$ times, from records $1$ to $n$.
> - For each outer loop iteration, the inner loop is executed once for each leftmost value that is out of order.
> 	- compares M times for M values *greater than `A[i]`* in `A[0] -> A[i - 1]`.
> 	- the number of **out of order** records ranges from $0$ up to $i$.
> - Inserting the $i$-th record requires a <u>max</u> of $i$ comparisons in the worst case, and a <u>min</u> of 1 comparison in the best case.

<br/>

- **Worst Case: Reverse-Sorted Array**
	- Every item on the left `A[0] -> A[i-1]` is *greater than* the current item `A[i]`.
	- <mark class="grey">Inserting the $i$-th item requires $i$ comparisons.</mark>
	- Starting at index 1, we have $1 + 2 + 3 + \ldots + n-1 = n(n-1)/2$ comparisons.
	- ==Worst-case time complexity is $O(n^2)$.==
- **Best Case: Sorted Array**
	- Every item on the left `A[0] -> A[i-1]` is *less than* the current item `A[i]`.
	- <mark class="grey">Inserting each item requires $1$ comparison.</mark>
	- $n-1$ comparisons in total = total number of outer loop iterations
	- ==Best-case time complexity is $O(n)$.==
- **Average Case: Randomly-Sorted Array**
	- <mark class="grey">Inserting the $i$-th item requires an average of $i/2$ comparisons.</mark>
	- For records from $1$ to $n-1$, the total cost is: $\sum_{i=1}^{n-1} \frac{i}2 = \frac{n(n+1)}4$.
	- ==Average-case time complexity is $O(n^2)$.==

> [!time|red]- Worst Case: Reverse-Sorted Array
> In the worst case, each iteration of the outer loop does the maximum possible number of comparisons (max number of inner loop checks).
>
> ==That is, for each item, we have to compare it with every item to the left.==
>
> The worst case occurs when all values are in descending order: from highest to lowest. That is, for every value, the one on the left is bigger:
>
> | 6   | 5   | 4   | 3   | 2   | 1   |
> | --- | --- | --- | --- | --- | --- |
> | 0   | 1   | 2   | 3   | 4   | 5   |
>
> At position 1, we have 1 record on the left. At position 2, we have 2 records on the left.
> Therefore, inserting the $i$-th record requires $i$ comparisons:
> - At $i = 1,$ one comparison is required.
> - At $i = 2$, two comparisons are required.
> - At $i = 3$, three comparisons are required.
> - ...
> - At $i = n - 1$, $n-1$ comparisons are required.
>
> The total number of comparisons are the sum of integers from $1$ to $n-1$.
> This is the sum or arithmetic series: $1 + 2 + 3 + \ldots + n-1 = n(n-1)/2.$
> Therefore, the worst case time complexity of insertion sort is $O(n^2)$.
>
> > [!maths|yellow] Another Analysis
> > Draw a box for each comparison.
> > The total number of comparisons will be:
> >
> > <center>area of the big triangle + area of (n-1) small triangles</center>
> >
> > So the total area is $\frac{(n-1)(n-1)}{2} + \frac{n-1}{2} = \frac{n(n-1)}2$.
> > Therefore, the worst-case running time is $O(n^2)$.
> >
> > ![[insertion-sort-analysis.png|Draw a box for each comparison made from i = 1 to i = n-1. The total number of comparisons made is then the sum of areas of the big triangle + the series of (n-1) small triangles.]]
> >

> [!time|teal]- Best Case: Sorted Array
> The best case occurs when the values are already in ascending order, from lowest to highest. For every $i$-th item, every item on the left from index $0$ to $i-1$ is already smaller, resulting in only 1 comparison need for items from $1$ to $n-1$.
>
> | 1   | 2   | 3   | 4   | 5   | 6   |
> | --- | --- | --- | --- | --- | --- |
> | 0   | 1   | 2   | 3   | 4   | 5   |
>
> **Inserting each element requires one comparison** (one inner loop condition check).
> Every test on the inner loop will fail immediately and no values will be moved.
>
> **The total number of comparisons will be $n-1$**, which is the number of times the outer loop executes to step through the array one item at a time, starting from index 1.
>
> Therefore, the best-case time complexity of insertion sort is $O(n)$.
>
> ```info:2
> void insertionSort(int[] A) {
>   for (int i=1; i<A.length; i++) // Insert i'th record
>     for (int j=i; (j>0) && (A[j] < A[j-1]); j--)
>       swap(A, j, j-1);
> }
> ```

> [!time|gray]- Average Case: Randomly-Sorted Array
> When record $i$ is processed, the number of times through the inner loop depends on how far out of order the record is. The inner loop is executed once for each value that is out of order.
>
> To calculate the average cost, we want to determine what is the average number of inversions will be for the record at position $i$.
>
> This could be 0, 1, or anything up to $i$. On average, it is $i/2$ positions out of order.
>
> | *0* | *1* | *...* | *$i - 1$* | ==$i$== | ... | $n-1$ |
> | --- | --- | ----- | --------- | ------- | --- | ----- |
>
> So for records from $1$ to $n-1$, we perform $i/2$ comparisons on average.
> Therefore, the total cost is
> $$
> \sum_{i=1}^{n-1} \frac{i}2 = \frac{n(n+1)}4 \approx O(n^2).
> $$ 

> [!NOTE|outlined] Why do we only count comparisons and not swaps?
> Counting comparisons or swaps yields similar results. Each inner loop iteration yields both a comparison and a swap, except for the last (i.e. the comparison that fails the inner loop test), which has no swap. Therefore, the number of swaps is $n-1$ less than the number of comparisons. This is $0$ in the best case, and $O(n^2)$ in the average and worst cases.
## Algorithm

```c
void insertionSort(int[] A) {
  for (int i = 1; i < A.length; i++) // Insert i'th record...
    for (int j = i; (j>0) && (A[j] < A[j-1]); j--) // in the correct position behind (left)
      swap(A, j, j-1); 
}
```

```python
def insertionSort(A):
	for i in range(1, len(A)): # Take the i'th record
		j = i;
		while (j != 0) and (A[j] < A[j-1]): # compare to the (i-1)'th record
			swap(j, j-1)     # swap if smaller A[i] < A[i-1]
			j -= 1           
```

- The outer loop steps throughs all elements except the first one, starting from `A[1]`.
- The inner loop compares `A[i]` to the left-most item, moving it down if `A[i] < A[i-1].
- After the inner loop, we insert `A[i]` in the correct place.
- After k iterations, the first k + 1 entries are sorted (+1 because the first entry is skipped).
## Step-by-Step Example
On each pass, we are building/growing the sorted list *behind* us (in green).

<u>First Pass</u>

**Step 1:** We start with the record in position 1.

| 20  | ==10== | <span style="color:rgb(204, 204, 204)">5</span> | <span style="color:rgb(204, 204, 204)">30</span> |
| --- | ------ | ----------------------------------------------- | ------------------------------------------------ |
| 0   | **1**  | 2                                               | 3                                                |

**Step 2:** Compare it to the record to its left.

| <u>20</u> | ==10== | <span style="color:rgb(204, 204, 204)">5</span> | <span style="color:rgb(204, 204, 204)">30</span> |
| --------- | ------ | ----------------------------------------------- | ------------------------------------------------ |
| 0         | **1**  | 2                                               | 3                                                |

**Step 3:** Since this is smaller than the value to its left, swap them.

| ==10== | *20* | <span style="color:rgb(204, 204, 204)">5</span> | <span style="color:rgb(204, 204, 204)">30</span> |
| ------ | ---- | ----------------------------------------------- | ------------------------------------------------ |
| **0**  | 1    | 2                                               | 3                                                |

**Step 4:** Now we are done with this record since we can't move further left.

| *10*  | *20* | <span style="color:rgb(204, 204, 204)">5</span> | <span style="color:rgb(204, 204, 204)">30</span> |
| ----- | ---- | ----------------------------------------------- | ------------------------------------------------ |
| **0** | 1    | 2                                               | 3                                                |

<u>Second Pass</u>

**Step 5:** Consider the next record in position 2.

| *10* | *20* | ==5== | <span style="color:rgb(204, 204, 204)">30</span> |
| ---- | ---- | ----- | ------------------------------------------------ |
| 0    | 1    | **2** | 3                                                |

**Step 6:** Compare it to the value to its left.

| *10* | <u>20</u> | ==5== | <span style="color:rgb(204, 204, 204)">30</span> |
| ---- | --------- | ----- | ------------------------------------------------ |
| 0    | 1         | **2** | 3                                                |

**Step 7:** Since it is smaller, swap them.

| *10* | ==5== | *20* | <span style="color:rgb(204, 204, 204)">30</span> |
| ---- | ----- | ---- | ------------------------------------------------ |
| 0    | **1** | 2    | 3                                                |

**Step 8:** Now compare against the record to its left.

| <u>10</u> | ==5== | *20* | <span style="color:rgb(204, 204, 204)">30</span> |
| --------- | ----- | ---- | ------------------------------------------------ |
| 0         | **1** | 2    | 3                                                |

**Step 9:** Since it is smaller, swap them.

| ==5== | *10* | *20* | <span style="color:rgb(204, 204, 204)">30</span> |
| ----- | ---- | ---- | ------------------------------------------------ |
| **0** | 1    | 2    | 3                                                |

**Step 10:** Now we are done with this record since we can't move further down.

| *5*   | *10* | *20* | <span style="color:rgb(204, 204, 204)">30</span> |
| ----- | ---- | ---- | ------------------------------------------------ |
| **0** | 1    | 2    | 3                                                |

<u>Third Pass</u>

**Step 11:** Consider the next record in position 3.

| *5* | *10* | *20* | ==30== |
| --- | ---- | ---- | ------ |
| 0   | 1    | 2    | **3**  |

**Step 12:** Compare it to the record in position 2.

| *5* | *10* | <u>20</u> | ==30== |
| --- | ---- | --------- | ------ |
| 0   | 1    | 2         | **3**  |

**Step 13:** Since it is NOT smaller than the record in position 2, nothing changes and we are done with this record.

| *5* | *10* | *20* | *30*  |
| --- | ---- | ---- | ----- |
| 0   | 1    | 2    | **3** |
## Implementation

```python
def insertion_sort(array):
    for i in range(1, len(array)):
        key = array[i]  # key to insert
        j = i - 1       # start at the previous element (to the left)
        
        while j >= 0 and key < array[j]:  # while we are LARGER than key
            array[j + 1] = array[j]       # ... move it to the right
            j -= 1                        # ... continue down the list

        array[j + 1] = key                # now we are SMALLER OR EQUAL to key
                                          # ... insert the key
    return array

```

- The outer `for` loop iterates up the array starting from index 1. The ==key== is where we are currently at in the array.
- With each outer iteration, we are comparing the ==key== with elements to its left. The inner `while` loop compares ==key== against the value to the left, and shifts all larger values up (to the right) while going down the list. This makes space behind us, so when we exit the loop, we insert the key in the space made behind (to the right).
