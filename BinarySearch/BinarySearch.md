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
