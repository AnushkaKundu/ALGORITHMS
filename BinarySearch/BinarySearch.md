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

3. Design the condition function. This is the most difficult and most beautiful part. Needs lots of practice.

   
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

### [Sqrt(x)](https://leetcode.com/problems/sqrtx/)

```
def mySqrt(x: int) -> int:
    left, right = 0, x
    while left < right:
        mid = left + (right - left) // 2
        if mid * mid <= x:
            left = mid + 1
        else:
            right = mid
    return left - 1
```
### [Search Insert Position](https://leetcode.com/problems/search-insert-position/)
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order. You may assume no duplicates in the array.

CPP
```
class Solution {
public:
    int searchInsert(vector<int>& num, int target) {
        int lo=0, high=num.size()-1;
        int mid=high/2;
        while (lo<=high)
        {
            if (num[mid]==target) return mid;
            else if (num[mid]<target) lo=mid+1;
            else high=mid-1;
            
            mid=lo+(high-lo)/2;
        }
        return mid;
    }
};
```

Python
```
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)
        while left < right:
            mid = left + (right - left) // 2
            if nums[mid] >= target:
                right = mid
            else:
                left = mid + 1
        return left
```

## Array of weights + max-weight given. Find min splits/ cuts in the array so that elements in each cut add up to weight less than max-weight
### [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)

Input: Array of weights, max-weight a partition of array can sum up to.
Output: No of partitions in array.

Python
```
def shipWithinDays(weights: List[int], D: int) -> int:
    def feasible(capacity) -> bool:
        days = 1
        total = 0
        for weight in weights:
            total += weight
            if total > capacity:  # too heavy, wait for the next day
                total = weight
                days += 1
                if days > D:  # cannot ship within D days
                    return False
        return True

    left, right = max(weights), sum(weights)
    while left < right:
        mid = left + (right - left) // 2
        if feasible(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

### [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)
Input: Array of weights, no. of paritions
Output: max-weight

Python:
```
def splitArray(nums: List[int], m: int) -> int:        
    def feasible(threshold) -> bool:
        count = 1
        total = 0
        for num in nums:
            total += num
            if total > threshold:
                total = num
                count += 1
                if count > m:
                    return False
        return True

    left, right = max(nums), sum(nums)
    while left < right:
        mid = left + (right - left) // 2
        if feasible(mid):
            right = mid     
        else:
            left = mid + 1
    return left
```

### [Koko Eating Bananas](875. Koko Eating Bananas)

Python
```
def minEatingSpeed(piles: List[int], H: int) -> int:
    def feasible(speed) -> bool:
        # return sum(math.ceil(pile / speed) for pile in piles) <= H  # slower        
        return sum((pile - 1) / speed + 1 for pile in piles) <= H  # faster

    left, right = 1, max(piles)
    while left < right:
        mid = left  + (right - left) // 2
        if feasible(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

### [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/)

Python
```
def minDays(bloomDay: List[int], m: int, k: int) -> int:
    def feasible(days) -> bool:
        bonquets, flowers = 0, 0
        for bloom in bloomDay:
            if bloom > days:
                flowers = 0
            else:
                bonquets += (flowers + 1) // k
                flowers = (flowers + 1) % k
        return bonquets >= m

    if len(bloomDay) < m * k:
        return -1
    left, right = 1, max(bloomDay)
    while left < right:
        mid = left + (right - left) // 2
        if feasible(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

### [Kth Smallest Number in Multiplication Table](https://leetcode.com/problems/kth-smallest-number-in-multiplication-table/description/)
Python
```
def findKthNumber(m: int, n: int, k: int) -> int:
    def enough(num) -> bool:
        count = 0
        for val in range(1, m + 1):  # count row by row
            add = min(num // val, n)
            if add == 0:  # early exit
                break
            count += add
        return count >= k                

    left, right = 1, n * m
    while left < right:
        mid = left + (right - left) // 2
        if enough(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

### [Find K-th Smallest Pair Distance](https://leetcode.com/problems/find-k-th-smallest-pair-distance/)

Python
```
def enough(distance) -> bool:  # two pointers
    count, i, j = 0, 0, 0
    while i < n or j < n:
        while j < n and nums[j] - nums[i] <= distance:  # move fast pointer
            j += 1
        count += j - i - 1  # count pairs
        i += 1  # move slow pointer
    return count >= k

def smallestDistancePair(nums: List[int], k: int) -> int:
    nums.sort()
    n = len(nums)
    left, right = 0, nums[-1] - nums[0]
    while left < right:
        mid = left + (right - left) // 2
        if enough(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

### [Ugly Number III [Medium]](https://leetcode.com/problems/ugly-number-iii/)

Python
```
def nthUglyNumber(n: int, a: int, b: int, c: int) -> int:
    def enough(num) -> bool:
        total = mid//a + mid//b + mid//c - mid//ab - mid//ac - mid//bc + mid//abc
        return total >= n

    ab = a * b // math.gcd(a, b)
    ac = a * c // math.gcd(a, c)
    bc = b * c // math.gcd(b, c)
    abc = a * bc // math.gcd(a, bc)
    left, right = 1, 10 ** 10
    while left < right:
        mid = left + (right - left) // 2
        if enough(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

### [Find the Smallest Divisor Given a Threshold](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/)

Python
```
def smallestDivisor(nums: List[int], threshold: int) -> int:
    def condition(divisor) -> bool:
        return sum((num - 1) // divisor + 1 for num in nums) <= threshold

    left, right = 1, max(nums)
    while left < right:
        mid = left + (right - left) // 2
        if condition(mid):
            right = mid
        else:
            left = mid + 1
    return left
```
