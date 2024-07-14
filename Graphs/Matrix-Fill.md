
## Flood Fill

## [Number of Islands (Considering boundary to be water)](https://leetcode.com/problems/number-of-islands/description/)
Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

```
Input: grid = 
[
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]

Output: 1
```
Example 2:
```
Input: grid = 
[
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
```

Output: 3

## [Number of Distinct Islands](https://www.naukri.com/code360/problems/distinct-island_630460)

## [Number of Islands (Considering boundary to be land)](https://leetcode.com/problems/number-of-enclaves/description/)
TODO: Count '1' islands
1. Convert all Boundary '1' to be '#'
2. Flood fill '#'
3. Count number of '1' islands

## [Surrounded Regions](https://leetcode.com/problems/surrounded-regions)
[Picture representation](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

TODO: Count 'O' islands
1. Convert Boundary 'O' to '#'
2. Flood fill '#'
3. Convert remaining 'O' to 'X' (to return the changed matrix)
4. Convert '#' to 'O' (to return the changed matrix)
5. Count number of '#' islands
