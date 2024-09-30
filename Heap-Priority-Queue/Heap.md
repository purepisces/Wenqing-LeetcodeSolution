### 1. **What is a Heap?**

A **heap** is a special binary tree data structure where:

-   **Min-Heap:** The parent node is always smaller than or equal to its children. This means the smallest element is always at the root.
-   **Max-Heap:** The parent node is always greater than or equal to its children, and the largest element is always at the root.

Python’s `heapq` module implements a **min-heap** by default. It provides methods to create and manipulate heaps efficiently.

-   **`heapq.heapify`**: Converts an unordered list into a min-heap.
-   **`heapq.heappop`**: Removes and returns the smallest element from the heap.
-   **`heapq.heappush`**: Adds a new element to the heap and maintains the heap property.

