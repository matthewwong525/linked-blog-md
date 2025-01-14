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
links: https://www.baeldung.com/cs/insertion-vs-bubble-sort#:~:text=On%20average%2C%20the%20bubble%20sort,twice%20as%20many%20cache%20misses
cssclasses:
  - table-array
method: exchange
---
## Bubble Sort
> **Best Time**: $O(n)$ comparisons and $O(1)$ swaps
> **Average & Worst Time**: $O(n^2)$ comparisons and swaps

#adaptive #stable #in-place

Step through the array, comparing pairs of adjacent elements, and swapping their values if [[data structures & algorithms/appendix/glossary#inversions|inverted]]. Repeat for all $n$ values, looking at one less item toward the end than the previous pass, or until no swaps have been performed during a pass. 

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1.5
===
<b><u>First Pass</u></b>
- Start from the first element.
- Compare every adjacent element up to the *last*. Swap if inverted.
- The largest value `23` “bubbles” up to the end of the array, in its final position.

<b><u>Second Pass</u></b>
- Start from the first element.
- Compare every adjacent element up to the *second-last* element.
- The second largest value `10` "bubbles" up to the 2nd last position.

<b><u>Final Pass</u></b>
- Start from the first element.
- Compare the last two unsorted elements.
- No more elements to compare. Done.
```
void bubblesort(int[] A) {
  n = A.length
  for (int i=0; i<n-1; i++) 
	swapped = false
    for (int j=1; j<n-i; j++) 
      if (A[j-1] > A[j])   
        swap(A, j-1, j);  
        swapped = true
        
	if (swapped = false) break   
}
```



`````

`````col-md
flexGrow=1
textAlign=end
===
![[bubble-sort.png|Each pass bubbles up the i-th largest value to the end.]]
`````
``````


- On the $i$-th pass the $i$-th largest element is guaranteed to be in its final position. 
- After a total of $n-1$ passes, all $n$ elements are guaranteed to be sorted.
- On each pass, we grow the sorted array by 1 element from the end. Therefore, on each pass, we can look at 1 less element (1 less comparison) than the previous one.
- On each pass, there are *always* $n-1-i$ comparisons made => $O(n^2)$ comparisons.
- However, the number of swaps varies depending on the number of inversions in the array. There will be $O(k)$ total swaps for $k$ inversions in the array.

## Notes

Bubble sort is slow, even compared to the other $O(n^2)$ sorts.
- Both algorithms compare elements to find their correct position. For each iteration, insertion sort finds the correct place for the $i$-th element amongst the already sorted $i-1$ elements. Conversely, bubble sort compares and swaps all adjacent elements in each iteration.
- Bubble sort always takes one more pass over array to determine if it's sorted (i.e. if no swaps have been made during a pass, it terminates). On the other hand, insertion sort does not need this — in a single pass once the last element is inserted, the array is guaranteed to be sorted.
- As a result, insertion sort performs fewer comparisons on average because it only compares elements until the correct position for the current item is found. Whereas bubble sort performs **more comparisons** since it always compares all $n-i$ elements (up until the last $i$ items).
- Also, this means bubble sort performs **more swaps** than insertion sort, which is a computationally expensive operation since it writes to memory.


> [!example]
> Take an array of numbers "5 1 4 2 8", and sort the array from lowest number to greatest number using bubble sort. In each step, elements ==highlighted== are being compared. Three passes will be required:
> 
> **First Pass**
> - ( ==5 1== 4 2 8 ) → ( ==1 5== 4 2 8 ), Swap since 5 > 1
> - ( 1 ==5 4== 2 8 ) → ( 1 ==4 5== 2 8 ), Swap since 5 > 4
> - ( 1 4 ==5 2== 8 ) → ( 1 4 ==2 5== 8 ), Swap since 5 > 2
> - ( 1 4 2 ==5 8== ) → ( 1 4 2 ==5 8== ), No swaps since 5 < 8 (already in order)
> 
> **Second Pass**
> - ( ==1 4== 2 5 8 ) → ( ==1 4 ==2 5 8 )
> - ( 1 ==4 2== 5 8 ) → ( 1 ==2 4== 5 8 ), Swap since 4 > 2
> - ( 1 2 ==4 5== 8 ) → ( 1 2 ==4 5== 8 )
> - ( 1 2 4 ==5 8== ) → ( 1 2 4 ==5 8== )
> 
> Now, the array is already sorted, but the algorithm doesn't know that. The algorithm needs one additional **whole** pass without **any** swap to know it is sorted.
> 
> **Third Pass**
> - ( ==1 2== 4 5 8 ) → ( ==1 2== 4 5 8 )
> - ( 1 ==2 4== 5 8 ) → ( 1 ==2 4== 5 8 )
> - ( 1 2 ==4 5== 8 ) → ( 1 2 ==4 5== 8 )
> - ( 1 2 4 ==5 8== ) → ( 1 2 4 ==5 8== )

## Properties
- [x] **Stable**: Comparisons are made between adjacent elements only. Elements are only swapped if out of order.
- [x] **Adaptive** : Bubble sort is $O(n^2)$ on average, but $O(n)$ if input is sorted.
- [x] **In-place**: Sorting is done within original array, through swaps.
## Analysis
1. The outer loop controls how many times the inner loop must run. For an array with $n$ values, the outer loop runs $n-1$ times, skipping the last value.
2. The inner loop goes through the array and swaps adjacent values. It goes through one less value each time it runs.

```
void bubblesort(int[] A) {
  for (int i=0; i<A.length-1; i++) 
	swapped = false
    for (int j=1; j<A.length-i; j++) 
      if (A[j-1] > A[j])   
        swap(A, j-1, j);  
        swapped = true
        
	if (swapped = false) break   
}
```

> [!summary]- Algorithm Steps
> - The outer loop executes $n-1$ times, processing records $0$ to $n-2$.
> - For each iteration $i$, the inner loop compares adjacent elements in the unsorted portion of the array (up to and including $n-1-i$).
> - On the $i$-th iteration, the number of comparisons is *always* $n-i$.
> - After the $i$-th iteration, the $i$-th largest element is in its final correct position.

<br/>

- **Worst Case: Reverse-Sorted Array**
	- <mark class="grey">$n-1$ passes required</mark> (max number of outer loop iterations).
	- Each pass requires $n-i$ comparisons (where $i=1$ to $n-1$).
	- <mark class="grey">Total comparisons: $n-1 + n-2 + ... + 1 = \frac{n(n-1)}2$</mark>.
	- Every comparison leads to a swap: <mark class="grey">$\frac{n(n-1)}2$ swaps</mark>.
	- ==Worst-case time complexity is $O(n^2)$==.
- **Best Case: Sorted Array**
	- <mark class="grey">$1$ pass required</mark>, with no swaps so we break early.
	- <mark class="grey">$n-1$ comparisons, $0$ swaps</mark>.
	- ==Best-case time complexity is $O(n)$==.


> [!time|red]- Worst Case: Reverse-Sorted Array
> In the worst case, every pass performs the max number of comparisons, and each comparison leads to a swap.
>
> This means that for every pair of adjacent elements, the left one is always greater than the right one, so the array will look like this:
>
> | 6   | 5   | 4   | 3   | 2   | 1   |
> | --- | --- | --- | --- | --- | --- |
>
>
> ``` hlt:2,3
> void bubblesort(int[] A) {
>   for (int i=0; i<A.length-1; i++) // i'th record
>     for (int j=1; j<A.length-i; j++) 
>       if (A[j-1] > A[j])   
>         swap(A, j-1, j);  
> }
> ```
>
> - The number of comparisons made by the inner loop on the $i$-th pass is always $n-i$.
> - The outer loop makes $n-1$ passes, from records $0$ to $n-2$:
> 	- First pass : $n-1$ comparisons
> 	- Second pass: $n-2$ comparisons
> 	- ...
> 	- Final pass ($n-1$): 1 comparison
>
> Total number of comparisons: $n-1 + n-2 + ... + 1 = \frac{n(n-1)}2$.
> Every comparison leads to a swap so total number of swaps: $\frac{n(n-1)}2$.
>
> Therefore, the worst-case time for bubble sort is $O(n^2)$.

> [!time|teal]- Best Case: Sorted Array
> The best case occurs when **no swaps are made in the first pass**, meaning the **array is already sorted** and the algorithm terminates immediately.
>
> | 1   | 2   | 3   | 4   | 5   | 6   |
> | --- | --- | --- | --- | --- | --- |
>
> The total number of comparisons is $n-1$, which is the number of outer loop iterations.
> ```hl:2
> void bubblesort(int[] A) {
>   for (int i=0; i<A.length-1; i++) 
>     for (int j=1; j<A.length-i; j++)
>       if (A[j-1] > A[j])
>         swap(A, j-1, j);
> }
> ```
> Therefore, the best-case running time of bubble sort is $O(n)$.

> [!time|gray]- Average Case: Random Array
> The number of swaps required depends on how often a record's value is less than the one to its left. We can expect this to occur for about half the comparisons in the average case, leading to $O(n^2)$ for the expected number of swaps.

## Algorithm
```
void bubblesort(int[] A) {

  for (int i=0; i<A.length-1; i++) 
	swapped = false
	
    for (int j=1; j<A.length-i; j++) 
      if (A[j-1] > A[j])   // if this pair is out of order
        swap(A, j-1, j);   // swap them and remember something changed
        swapped = true
        
	if (swapped = false) break   
}
```

- Consists of a double loop:
	- The outer loop runs from $0$ up to $n-1$ (the last element). 
	- The inner loop moves through the array from left to right, comparing adjacent keys. If a key is greater than the key to its right, then the two are swapped. Once the largest key is found, this is "bubbled" up to the right end of the array.
- The $i$-th pass finds the $i$-th largest value and puts it into its final place. Therefore, on the $i$-th pass, we can skip looking at the last $i$ items.
- If no swaps occur during a pass, the algorithm exits early.

```python
def bubble_sort(array):
    n = len(array)

    for i in range(n):
        swapped = False
        for j in range(n - i - 1): 
            if array[j] > array[j + 1]:
                array[j], array[j + 1] = array[j + 1], array[j] # swap
                swapped = True

        if not swapped:
            break

    return array
```
The outer loop iterates from the positions $0$ to $n-1$.
The inner loop iterates from the start to the second-last element $n-1$ because 

The range of the inner loop decreases with each pass (`n - i - 1`) as the sorted portion at the right-end grows (since on the $i$-th pass, the last $i$ items are sorted).