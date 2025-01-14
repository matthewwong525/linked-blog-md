## Adaptability
>**Adaptive sorting algorithms take advantage of *pre-sorted* input and sorts faster.**

A sorting algorithm is **adaptive** if performs more efficiently (i.e. requires fewer operations) when dealing with already- or partially- sorted data.

The time complexity of an adaptive sorting algorithm will be better for sorted or nearly-sorted inputs. ==The more pre-sorted the input is, the faster it should be sorted.==

This can be a useful property, depending on whether nearly sorted inputs are common.

[[Insertion sort]] is an example of an adaptive sorting algorithm. Otherwise, adaptive sorting is usually achieved by modifying existing sorting algorithms e.g. adaptive heap sort.

