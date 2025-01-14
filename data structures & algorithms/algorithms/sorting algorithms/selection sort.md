---
adaptive: 
stable: 
in-place: true
tags:
  - adaptive
  - stable
  - in-place
memory: $O(1)$
best: $O(n^2)$
average: $O(n^2)$
worst: $O(n^2)$
links: 
cssclasses: 
method: selection
---
## Selection Sort
> **Best Time**: $O(n^2)$ comparisons, $O(1)$ swap
> **Average & Worst Time**: $O(n^2)$ comparisons, $O(n)$ swaps

#adaptive #stable #in-place

Step through the array, looking through the entire unsorted portion of the array to find the **smallest (or largest)** item. Remember its location, and swap it in the correct position at the end of the pass. Repeat for all $n$ values. 

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1.75
===
<b><u>First Pass</u></b>
Find the smallest element in `a[0 .. n-1]`
Swap it with the first element `a[0]`

<b><u>Second Pass</u></b>
Find the second-smallest element in `a[1 .. n-1]`
Swap it with the second element `a[1]`

<b><u>Final Pass</u></b>
Find the second-largest element in `a[n-2 .. n-1]`,
Swap it with the second-last element `a[n-2]`
`````

`````col-md
flexGrow=1
===
![[selection-sort-1.png|Each pass builds up the sorted array by one. Similar to Insertion Sort, except Selection Sort scans forward (not backwards) and compares all unsorted items to find the minimum. It then "remembers" the location of this key, and performs a long-range swap at the end.]]
`````
``````

> [!pros] Advantages
> - Requires less number of swaps (or memory writes) compared to other algorithms. Total of $n-1$ swaps vs up to $\frac{n(n-1)}2$ swaps in [[insertion sort]] and [[bubble sort]].
> - Requires only a constant $O(1)$ extra memory space.

> [!cons] Disadvantages
> - **Not stable** — performs ==long-range swaps==, so it does not maintain the relative order of equal elements — making it not suitable for sorting input with duplicate keys.
> - **Not adaptive** — ==selection sort will perform identically, regardless of the order of the array==. In contrast, both bubble sort and insertion sort's running time can improve to $O(n)$ if the array is already sorted or "close to sorted."
> - **$O(n^2)$ time** — selection sort has a $O(n^2)$ time complexity, which makes it inefficient on large lists.
## Analysis
1. The outer loop that controls how many times the inner loop must run. For an array with $n$ values, the outer loops must run $n-1$ times , skipping the last value.
2. The inner loop goes through the unsorted part of array, finds the lowest value and remembers its location. After it looks at all $n-1-i$ values, it moves the found minimum to the front. This loop must loop through one less value each time it runs.

```c
void selectionSort(int arr[], int n) {

    // For each element in the array
    for (int i = 0; i < n - 1; i++) {
    
		// Assume the min is the first element
        int min = i;
        
        // Find the minimum in the unsorted a[i .. aLength-1]
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[min]) {
                min = j;
            }
        }
        
        // Move minimum element to its correct position
        swap(arr, a[i], a[min]);
    }
}
```

> [!maths|black|outlined] TOTAL COST
> - Total number of comparisons = $(n-1) + (n-2) + \ldots + 1 = \frac{n(n-1)}2 = O(n^2)$.
> - Total number of swaps = $n-1 = O(n)$.

- One loop to select an element (except for the last one): $O(n)$
- Another loop to compare that element with every other unsorted element: $O(n)$ 
- Overall time complexity = $O(n) \times O(n) = O(n^2)$

> [!warning|red] Best = Worst = Average Time = $O(n^2)$
> **The ==number of comparisons and swaps is always the same==, regardless of the sortedness of the input. Therefore, ==Selection Sort is not adaptive==.** 
> 
> The outer loop goes through the array of $n$ values $n-1$ times, and for each value, the inner loop scans all remaining unsorted values to find the minimum, taking  $n-1-i$ comparisons (compare one less item each pass) and performing exactly $1$ swap to insert it in the correct position.
> 
> Therefore, Selection Sort's cost is the same in all cases: worst, best and average-case.

> [!maths|gray]- Detailed Explanation
> **The outer loop goes through the array of $n$ values $n-1$ times.** This is because when the algorithm has sorted all values except the last, the last value must also be in the correct position.
> 
> **On each outer loop iteration, the inner loop executes $n-1-i$ times**. The $-i$ part is because on each pass, the array is sorted by one extra element,  so we can skip comparing the first $i$ items that have been sorted. 
> 
> On the first pass, selecting the minimum requires requires scanning $n$ elements, taking $n-1$ comparisons, and then swapping it into the first position. Finding the next lowest element requires scanning the remaining $n-1$ elements (taking $n-2$ comparisons) and so on. 
> 
> - First Pass: $n-1$ comparison, $1$ swap.
> - Second Pass: $n-2$ comparison, $1$ swap.
> - ...
> - Final Pass (only 2 items left): $1$ comparison, $1$ swap.
> 
> Therefore, the total number of comparisons is a sum of an arithmetic sequence:
> $${\displaystyle (n-1)+(n-2)+\dots +1=\sum _{i=1}^{n-1}i} = {\frac {(n-1)+1}{2}}(n-1)={\frac {1}{2}}n(n-1)={\frac {1}{2}}(n^{2}-n).$$
> which is of complexity $O(n^2)$ in terms of number of comparisons.
> 
> On each pass, we perform exactly $1$ swap operation. Therefore, the total number of swaps is $n-1$ which is of complexity $O(n)$.
## Properties
- [ ] ~~Stable~~: Selection Sort is *unstable* due to long-range swaps.
- [ ] ~~Adaptive~~:  Selection Sort is *not adaptive* because it performs a constant number of steps (same number of comparisons and swaps), regardless of sortedness of original array.
- [x] **In-place**: Sorting is done within original array, through swaps.
## Notes
Selection Sort is essentially a [[bubble sort]], except that the **next largest value is remembered** so that we can **delay the swap to the end of each pass** (whereas bubble sort repeatedly swaps it until it is at the end). 

Selection sort is also very similar to insertion sort in that after the $k$th iteration, the first $k$ elements in the array are in sorted order. 

The key difference is selection sort requires ==few swaps==. To find the next-largest key value requires searching through the entire unsorted portion of the array, but only one swap is required to put the record into place. Thus, the total number of swaps required will be $n−1$ (we get the last record in place “for free”).

However, the biggest disadvantage is that selection sort is not adaptive and requires more comparisons and swaps on average, when compared with bubble sort and insertion sort. Insertion sort only scans as many elements as it needs in order to place the $k+1$st element. Selection sort must scan all remaining elements to find the $k+1$st element.
## Walkthrough
![Selection Sort|500](https://miro.medium.com/v2/resize:fit:1400/1*5WXRN62ddiM_Gcf4GDdCZg.gif)

- @ Each iteration (pass) improves the “sortedness” of the array by one element.
- ! The $i$-th pass "selects" the $i$-th smallest (or largest) key.
- $ After the $n-1$ pass, the array is sorted.
- Swap the <u>min</u> element with the <u>current element</u> `a[i]` at index $i$.
- Swap the <u>max</u> element with the <u>i-th last element</u> `a[n-1-i]` at index $n-1-i$.

> [!example]- Explanation
> The input list is divided into 2 parts:
> 1. a sorted sublist which is built up from at the front (left) of the list
>    `a[0 .. i-1]`
> 1. an unsorted sublist which is the remaining part of the list
>    `a[i .. n-1]`
> 
> Initially, the sorted sublist is empty and the unsorted sublist is the entire input list.
> 
> The algorithm proceeds by repeatedly selecting the **smallest (or largest)** element from the unsorted portion and swapping it with the **first (or last)** unsorted element. This process continues until the entire array is sorted:
> 
> ```
> arr[] = 64 25 12 22 11
> 
> // Find the minimum element in arr[0...4]
> // and place it at beginning
> 11 25 12 22 64
> 
> // Find the minimum element in arr[1...4]
> // and place it at beginning of arr[1...4]
> 11 12 25 22 64
> 
> // Find the minimum element in arr[2...4]
> // and place it at beginning of arr[2...4]
> 11 12 22 25 64
> 
> // Find the minimum element in arr[3...4]
> // and place it at beginning of arr[3...4]
> 11 12 22 25 64
> ```
> 
> | Pass | Sorted sublist       | Unsorted sublist      | Least element in unsorted list |
> | ---- | -------------------- | --------------------- | ------------------------------ |
> | 0    | \[ \]                | \[ 23, 10, 1, 5, 2 \] | 1                              |
> | 1    | \[ 1 \]              | \[ 23, 10, 5, 2 \]    | 2                              |
> | 2    | \[ 1, 2 \]           | \[ 23, 10, 5 \]       | 5                              |
> | 3    | \[ 1, 2, 5 \]        | \[ 23, 10 \]          | 10                             |
> | 4    | \[ 1, 2, 5, 10 \]    | \[ 23 \]              | 23                             |
> | 5    | \[ 1, 2, 5, 10, 23\] | \[ \]                 |                                |
> As you can see, each pass improves the "sortedness" of the array by one element.
## Implementation
1. Find the min/max element in the unsorted portion: `a[i .. n-1]`.
2. Insert the found element:
	1. Place the **min** at the **beginning** of the unsorted portion `a[i]`. [^1]
	2. Place the **max** at the **end** of the unsorted portion `a[n-1-i]`. [^2]

> [!1|teal] Find the Minimum 
> ```python
> def selection_sort(array):
>     n = len(array)
> 
>     # advance the position through the entire array
>     for i in range(n - 1):
>         # find the min element in the unsorted a[i .. n-1]
>         
>         # assume the min is the first element
>         min_index = i
>         
>         # test against elements after i to find the smallest
>         for j in range(i + 1, n):
>         
>             # if this element is less, then it is the new minimum
>             if array[j] < array[min_index]:
>                 min_index = j
>                 
>         # swap the found minimum element with the first element
>         if min_index != i:
>             array[i], array[min_index] = array[min_index], array[i]
> 
>     return array
> ```
> 
> In each iteration (pass), we find the minimum element’s index in the <mark class="grey">unsorted portion of the array `A[i .. aLength-1]`</mark>, and swap it with the <mark class="grey">current index’s element (i.e. the beginning of the unsorted portion `A[i]`)</mark>. This gradually sorts the array from left to right.
> 
> Note that the outer loop runs $n-1$ times from `a[0]` to `a[n-2]` (the second last item) because by the time we have placed the `a[n-2]` element in the correct position, the last element is also guaranteed to be in the correct spot. 

> [!2|red]- Find the Maximum
> Another way to implement selection sort is to find the maximum element and swap it with the last unsorted element:
> 
> ```python
> def selection_sort(array):
>     n = len(array)
>     
>     for i in range(n - 1):
>         max_index = i
>         for j in range(1, n - i):
>             if array[j] > array[max_index]:
>                 max_index = j
> 
>         # swap with the last unsorted element at a[n - 1 - i]
>         array[max_index], array[n-i-1] = array[n-i-1], array[max_index]
> ```
> ```python
> def selection_sort_max(array):
>     n = len(array)
> 
>     # advance the position through the entire array, starting from the end
>     for i in range(n - 1, 0, -1):
>         # find the max element in the unsorted a[0 .. i]
> 
>         # assume the max is the first element
>         max_index = 0
> 
>         # test against elements after i to find the largest
>         for j in range(1, i + 1):
> 
>             # if this element is greater, then it is the new maximum
>             if array[j] > array[max_index]:
>                 max_index = j
> 
>         # swap the found maximum element with the last element
>         if max_index != i:
>             array[i], array[max_index] = array[max_index], array[i]
> 
>     return array
> ```

[^1]: The current index.
[^2]: We do not place the max element at `a[n-1]` because with each subsequent pass, we are finding the *next* largest element, which needs to be placed *before* the last element found. **Recall:** The $i$-th pass of Selection Sort "selects" the $i$-th largest/smallest key. Therefore, on the $i$-th pass, we want to place the key in the $i$-th last position which is `a[n-1-i]`.