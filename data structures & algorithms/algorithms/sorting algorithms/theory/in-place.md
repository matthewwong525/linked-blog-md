## In-place
> **In-place sorting algorithms sorts and modifies the input *in place* (directly), without requiring extra space (i.e. creating temporary arrays).**

A sorting algorithm is **in-place** it sorts the data within the original structure, without requiring extra space or creating a separate copy of the data structure.

Examples of sorting algorithms that re-arrange arrays into sorted order in-place include [[bubble sort]], [[selection sort]], [[insertion sort]], [[heap sort]] and [[shell sort]]. These algorithms require only a few pointers, so their space complexity is O(log n).

In contrast, [[quick sort]] operates in-place on the data to be sorted. However, it requires O(log n) stack space pointers to keep track of the subarrays in its divide and conquer strategy. Therefore, it needs O(log^2 n) additional space.
