# C++ Data Structures Time Complexities

## Vector

| Function         | Time Complexity |
|------------------|-----------------|
| operator[]     | O(1)            |
| at             | O(1)            |
| front          | O(1)            |
| back           | O(1)            |
| data           | O(1)            |
| begin          | O(1)            |
| end            | O(1)            |
| rbegin         | O(1)            |
| rend           | O(1)            |
| empty          | O(1)            |
| size           | O(1)            |
| capacity       | O(1)            |
| clear          | O(n)            |
| insert         | O(n)            |
| erase          | O(n)            |
| push_back      | Amortized O(1)  |
| pop_back       | O(1)            |
| resize         | O(n)            |
| swap           | O(1)            |

## Deque

| Function         | Time Complexity |
|------------------|-----------------|
| operator[]     | O(1)            |
| at             | O(1)            |
| front          | O(1)            |
| back           | O(1)            |
| begin          | O(1)            |
| end            | O(1)            |
| rbegin         | O(1)            |
| rend           | O(1)            |
| empty          | O(1)            |
| size           | O(1)            |
| clear          | O(n)            |
| insert         | O(n)            |
| erase          | O(n)            |
| push_back      | O(1)            |
| pop_back       | O(1)            |
| push_front     | O(1)            |
| pop_front      | O(1)            |
| resize         | O(n)            |
| swap           | O(1)            |

## List

| Function         | Time Complexity |
|------------------|-----------------|
| front          | O(1)            |
| back           | O(1)            |
| begin          | O(1)            |
| end            | O(1)            |
| rbegin         | O(1)            |
| rend           | O(1)            |
| empty          | O(1)            |
| size           | O(1)            |
| clear          | O(n)            |
| insert         | O(1)            |
| erase          | O(1)            |
| push_back      | O(1)            |
| pop_back       | O(1)            |
| push_front     | O(1)            |
| pop_front      | O(1)            |
| resize         | O(n)            |
| swap           | O(1)            |
| splice         | O(1)            |
| remove         | O(n)            |
| unique         | O(n)            |
| merge          | O(n + m)        |
| sort           | O(n log n)      |
| reverse        | O(n)            |

## Queue

| Function         | Time Complexity |
|------------------|-----------------|
| push           | O(1)            |
| pop            | O(1)            |
| front          | O(1)            |
| back           | O(1)            |
| empty          | O(1)            |
| size           | O(1)            |

## Priority Queue

| Function          | Time Complexity |
|-------------------|-----------------|
| push            | O(log n)        |
| pop             | O(log n)        |
| top             | O(1)            |
| empty           | O(1)            |
| size            | O(1)            |

## Heap

| Function          | Time Complexity |
|-------------------|-----------------|
| make_heap       | O(n)            |
| push_heap       | O(log n)        |
| pop_heap        | O(log n)        |
| sort_heap       | O(n log n)      |
| is_heap         | O(n)            |
| is_heap_until   | O(n)            |

## Stack

| Function         | Time Complexity |
|------------------|-----------------|
| push           | O(1)            |
| pop            | O(1)            |
| top            | O(1)            |
| empty          | O(1)            |
| size           | O(1)            |

## Set / Multiset

| Function         | Time Complexity |
|------------------|-----------------|
| insert         | O(log n)        |
| erase          | O(log n)        |
| find           | O(log n)        |
| count          | O(log n)        |
| lower_bound    | O(log n)        |
| upper_bound    | O(log n)        |
| begin          | O(1)            |
| end            | O(1)            |
| rbegin         | O(1)            |
| rend           | O(1)            |
| empty          | O(1)            |
| size           | O(1)            |
| clear          | O(n)            |
| swap           | O(1)            |

## Map / Multimap

| Function         | Time Complexity |
|------------------|-----------------|
| insert         | O(log n)        |
| erase          | O(log n)        |
| find           | O(log n)        |
| count          | O(log n)        |
| lower_bound    | O(log n)        |
| upper_bound    | O(log n)        |
| begin          | O(1)            |
| end            | O(1)            |
| rbegin         | O(1)            |
| rend           | O(1)            |
| empty          | O(1)            |
| size           | O(1)            |
| clear          | O(n)            |
| swap           | O(1)            |

## Unordered Set / Unordered Multiset

| Function         | Time Complexity |
|------------------|-----------------|
| insert         | O(1) average, O(n) worst |
| erase          | O(1) average, O(n) worst |
| find           | O(1) average, O(n) worst |
| count          | O(1) average, O(n) worst |
| begin          | O(1)            |
| end            | O(1)            |
| empty          | O(1)            |
| size           | O(1)            |
| clear          | O(n)            |
| swap           | O(1)            |

## Unordered Map / Unordered Multimap

| Function         | Time Complexity |
|------------------|-----------------|
| insert         | O(1) average, O(n) worst |
| erase          | O(1) average, O(n) worst |
| find           | O(1) average, O(n) worst |
| count          | O(1) average, O(n) worst |
| begin          | O(1)            |
| end            | O(1)            |
| empty          | O(1)            |
| size           | O(1)            |
| clear          | O(n)            |
| swap           | O(1)            |
