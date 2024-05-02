# Pattern: Top 'K' Elements

The **Top 'K' Elements** pattern is a common coding pattern used to solve problems that involve finding the top, smallest, or most/least frequent **k** elements in an unsorted list. This pattern is particularly useful when dealing with large datasets, as it allows us to solve these problems efficiently without having to sort the entire list.

## Understanding the Pattern

The main idea behind this pattern is to maintain a heap of size **k** while iterating through the list of elements. The type of heap (min-heap or max-heap) depends on the problem at hand. For instance, if we want to find the top **k** largest elements, we use a min-heap; for the top **k** smallest elements, we use a max-heap.

## Heap Complexities

The time complexity of heap operations is as follows:
- **Make heap** (Make the entire vector a heap): **O(n)**
  > Often very useful. Instead of doing insertion of `n` elements in `0(n*log n)` time, we can achieve same in `O(n)` time.

- **Insertion**: **O(log n)**

- **Deletion**: **O(log n)**

- **Peek (or top operation)**: **O(1)**

These complexities make heaps an efficient data structure for the **Top 'K' Elements** pattern. They allow us to insert and delete elements in logarithmic time, which is significantly faster than linear time operations. This efficiency is crucial when dealing with large datasets or real-time data streams.

## Conclusion

The **Top 'K' Elements** pattern is a powerful tool for dealing with large datasets and finding the top **k** elements. By using a heap data structure, we can solve these problems efficiently and elegantly. Remember, practice is key to mastering this pattern, so try to solve as many problems as you can using this pattern. Happy coding!
