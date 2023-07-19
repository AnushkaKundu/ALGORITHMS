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
1. Correctly initialize the boundary variables left and right. Only one rule: set up the boundary to **include all possible elements**;


2. Decide return value. Is it return left or return left - 1? Remember this: after exiting the while loop, left is the minimal k​ satisfying the condition function;

If the array suffices ....TTTTTTTFFFFFF.... for the condition in the problem, so you want to find the last True value. So, Design a modifiedCondition that is !condition (complement). And return `left-1` in outer loop.

If the array suffices ....FFFFFFFTTTTTT.... for the condition in the problem, so you want to find the first True value. Return `left` in outer loop.


3. Design the condition function. This is the most difficult and most beautiful part. Needs lots of practice.
