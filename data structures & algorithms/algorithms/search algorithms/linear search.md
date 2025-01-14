The linear (or sequential) search algorithm accepts as its input an array of $n$ keys and the target key $K$ to search for.

There are 3 input cases that affect the running time of linear search:
1. When the target key $K$ is located at the first position in the input array
2. When the target key $K$is located at the last position in the input array
3. The average cost over all possible positions for $K$, which comes out to about $n/2$. 


In the best case, only one element is visited. T(n) = 1.
The upper bound time complexity in the best case is O(1).
Even when $n$ increases, the cost for the best case does not grow.

In the worst case, $n$ elements must be visited. T(n) = n.
The upper bound time complexity in the worst case is O(n).

In the average case, about $n/2$ elements are visited. T(n) = $n/2$.
The upper bound time complexity in the average case also O(n).

What is the upper bound of linear search in the best/average/worst case?


