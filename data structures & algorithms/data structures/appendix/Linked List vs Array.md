|                                                                 | Array                              | Linked List                                                   |
| --------------------------------------------------------------- | ---------------------------------- | ------------------------------------------------------------- |
| Fixed size in memory                                            | Yes                                | No                                                            |
| Elements stored right after each other in memory (contiguously) | Yes                                | No                                                            |
| Random access (direct element access)                           | Yes                                | No                                                            |
| O(1) insertion and deletion                                     | No                                 | Yes                                                           |
| Memory Overhead                                                 | Low (each node only contains data) | High (each node contains both data + pointers)                |
| Memory Efficiency                                               | May contain unused memory          | Can change dynamically in size, resulting in no wasted memory |


| Operation       | Array                                   | Linked List                             |
| --------------- | --------------------------------------- | --------------------------------------- |
| **Access**      | Best: O(1) <br>Avg: O(1)<br>Worst: O(1) | Best: O(1)<br>Avg: O(n)<br>Worst: O(n)  |
| **Insertion**   | Best: O(1)<br>Avg: O(n)<br>Worst: O(n)  | Best: O(1)<br>Avg: O(n)<br>Worst: O(n)  |
| **Deletion**    | Best: O(1)<br>Avg: O(n)<br>Worst: O(n)  | Best: O(1)<br>Avg: O(n)<br>Worst: O(n)  |
| **Memory**      | Efficient if size is optimised          | Higher overhead (pointers in each node) |
| **Flexibility** | Fixed size, possible unused memory      | Dynamically adjusts, no wasted memory   |
## Arrays
Arrays stores elements in **contiguous memory locations**, resulting in easily calculable addresses for the elements stored. This allows faster access to an element at a specific index. Also, the size of an array is fixed and must be declared beforehand, making it unchangeable.
### Access
Accessing an element takes constant time O(1).

Elements are stored in contiguous memory locations, resulting in easily calculable memory addresses for the element stored.

For example, if we want to retrieve the element at index 4, we can calculate the memory address of the index with simple arithmetic:

```
Base address of array (the memory address of the first element) + index
```

![[arrays-sequential-memory.webp|Sequential memory allows for highly efficient element access in arrays.]]

### Insertion
Insertion at the end is O(1) but inserting at the beginning or middle requires shifting elements to the right to make one space, making it O(n).

- **Best Case**: $O(1)$ – inserting an element at the end of the array means no elements need to be shifted.
- **Average Case**: $O(n)$ – elements can be inserted anywhere, the mean index being **0.5n**. So the number of shifts is proportional to the size of the array **n**.
- **Worst Case**: $O(n)$ – inserting at the beginning requires shifting all **n-1** elements one space to the right.

![[array-insertion.webp|If an element is inserted at the beginning of an array, the whole array must shift to the right one space resulting in a worst time complexity of O(n).]]

### Deletion
Deletion at the end is O(1) but deleting from the beginning or middle requires shifting elements to the left to remove one space, making it O(n).

- **Best Case**: O(1) – deleting the last element requires no shifting.
- **Average Case**: O(n) – deleting an element at a random position requires shifting the remaining elements.
- **Worst Case**: O(n) – deleting the first element necessitates shifting all subsequent elements.
### Memory
Arrays are memory-efficient for data storage, but require pre-declaration of size, which can lead to over-sizing or under-sizing.


![[array-size.webp|In this array of size 6, only 5 memory addresses are being usefully used, the last memory address 105 serves as a waste of space.]]

> [!calculator] Calculation
> An integer is 4 bytes. The total memory usage is therefore:
> - 5-index array (with unused space): `4 bytes × 5 = 20 bytes`
> - 4-index array (no useless space): `4 bytes × 4 = 16 bytes`


## Linked Lists
Linked lists are a linear collection of elements connected via **pointers**, with each node pointing to the memory address of the next node. Elements are **not stored in contiguous memory** and are dynamically allocated.
### Access
> Accessing an element requires traversal starting from the head node.

Elements are randomly stored in the memory so we cannot calculate the memory address of a given index.

In order to access an element, we must follow the pointer at each node starting from the head until we reach the desired index.

Hence, access is directly proportional to the size of the linked list.

- Best Case: O(1) – accessing the head node (first node).
- Average Case: O(n) – traversing $\sim n/2$ nodes (average index being accessed is ***n/2***)
- Worst Case: O(n) – accessing the last node.
### Insertion
Inserting an element into a linked list is more efficient than arrays because it requires no shifts. Instead, the pointer of the previous node must change to the address of the newly added node.

However, to get to that position, you must first traverse the linked list until the desired index of insertion, therefore, taking an O(n) average time.

Similarly, if a new node is inserted at the beginning of the linked list, then the head pointer will be replaced in order to point to the memory address of the new starting node. This results in a best time complexity of O(1).

- **Best Case**: O(1) – inserting at the beginning by updating the head pointer.
- **Average Case**: O(n) – traversing the list to the desired position before updating pointers.
- **Worst Case**: O(n) – inserting at the end requires traversing to the last node and updating its pointer.

### Deletion
Deletion at the head is O(1), but for other positions, traversal is required, making it O(n).

- **Best Case**: O(1) – deleting the first node involves updating the head pointer.
- **Average Case**: O(n) – traversing to find the node to delete, followed by updating pointers.
- **Worst Case**: O(n) – deleting the last node requires traversal of the entire list.

### Memory
Linked lists need memory to store data AND a memory address in each node, whereas arrays only need to store data values. This increases overall memory usage.

However, unlike arrays, nodes are dynamically allocated when needed so all memory is useful. There is never unused memory.

> [!calculator] Calculation
> An integer is 4 bytes. A pointer is 8 bytes. The total memory usage is therefore:
> - 4-node linked list: `4 bytes × 4 + 8 bytes = 56 bytes`


