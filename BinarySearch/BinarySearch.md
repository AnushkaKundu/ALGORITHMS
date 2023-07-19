### Questions

When to exit the loop? Should we use `left < right` or `left <= right` as the while loop condition?

How to initialize the boundary variable `left` and `right`?

How to update the boundary? How to choose the appropriate combination from `left = mid` , `left = mid + 1` and `right = mid`, `right = mid - 1`?


### General Syntax
```
def binary_search(array) -> int:
    def condition(value) -> bool:
        pass

    left, right = 0, len(array)
    while left < right:
        mid = left + (right - left) // 2
        if condition(mid):
            right = mid
        else:
            left = mid + 1
    return left
```
1. Correctly initialize the boundary variables left and right. Only one rule: set up the boundary to **include all possible elements**.


2. Decide return value. Is it return left or return left - 1? Remember this: after exiting the while loop, left is the minimal k​ satisfying the condition function;

    If the array suffices ....TTTTTTTFFFFFF.... for the condition in the problem, so you want to find the last True value. So, Design a modifiedCondition that is !condition (complement). And return `left-1` in outer loop.

    If the array suffices ....FFFFFFFTTTTTT.... for the condition in the problem, so you want to find the first True value. Return `left` in outer loop.

## Questions

### [First Bad Version](https://leetcode.com/problems/first-bad-version/)
You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which returns whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.


```
class Solution:
    def firstBadVersion(self, n) -> int:
        left, right = 1, n
        while left < right:
            mid = left + (right - left) // 2
            if isBadVersion(mid):
                right = mid
            else:
                left = mid + 1
        return left
```

3. Design the condition function. This is the most difficult and most beautiful part. Needs lots of practice.
