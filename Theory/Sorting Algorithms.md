# Time Complexities of Sorting Algorithms

| Sorting Algorithm | Best Case Time Complexity | Average Case Time Complexity | Worst Case Time Complexity | Stable | In-Place |
|-------------------|---------------------------|------------------------------|----------------------------|--------|----------|
| **Bubble Sort**   | O(n)                      | O(n^2)                       | O(n^2)                     | Yes    | Yes      |
| **Selection Sort**| O(n^2)                    | O(n^2)                       | O(n^2)                     | No     | Yes      |
| **Insertion Sort**| O(n)                      | O(n^2)                       | O(n^2)                     | Yes    | Yes      |
| **Merge Sort**    | O(n log n)                | O(n log n)                   | O(n log n)                 | Yes    | No       |
| **Quick Sort**    | O(n log n)                | O(n log n)                   | O(n^2)                     | No     | Yes      |
| **Heap Sort**     | O(n log n)                | O(n log n)                   | O(n log n)                 | No     | Yes      |
| **Counting Sort** | O(n + k)                  | O(n + k)                     | O(n + k)                   | Yes    | No       |
| **Radix Sort**    | O(nk)                     | O(nk)                        | O(nk)                      | Yes    | No       |
| **Bucket Sort**   | O(n + k)                  | O(n + k)                     | O(n^2)                     | Yes    | No       |
| **Shell Sort**    | O(n log n)                | O(n^(3/2))                   | O(n^2)                     | No     | Yes      |

* n: number of elements
* k: range of the input values (for Counting Sort and Radix Sort)

## Definitions

- **Stable Sorting Algorithm**: A sorting algorithm is said to be stable if it preserves the relative order of records with equal keys (i.e., values). For example, if two elements with equal keys appear in the same order in the sorted output as they appear in the input, the sorting algorithm is stable.

- **In-Place Sorting Algorithm**: A sorting algorithm is considered in-place if it requires only a constant amount (O(1)) of additional memory space to perform the sorting. In other words, it doesn't require extra space for another array or a significant amount of additional space.
