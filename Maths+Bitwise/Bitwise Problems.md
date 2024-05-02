## Number Complement

**Problem Statement:**  
The complement of an integer is the integer you get when you flip all the 0's to 1's and all the 1's to 0's in its binary representation.

For example, The integer 5 is "101" in binary and its complement is "010" which is the integer 2.

Given an integer num, return its complement.
```cpp
class Solution {
public:
    int findComplement(int n) {
        int nn = n;
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;
        return (((n - (n >> 1)) - 1) << 1) + 1 - nn;
    }
};
```
## Single Number

**Problem Statement:**  
Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int x=0;
        for (auto ele:nums) x^=ele;
        return x;
    }
};
```

## Single Number II
**Problem Statement:**  
Given an integer array nums where every element appears three times except for one, which appears exactly once. Find the single element and return it.

You must implement a solution with a linear runtime complexity and use only constant extra space.

**Examples:**
```
Example 1:

Input: nums = [2,2,3,2]
Output: 3
Example 2:

Input: nums = [0,1,0,1,0,1,99]
Output: 99
```

**Constraints:**
```
1 <= nums.length <= 3 * 104
-231 <= nums[i] <= 231 - 1
Each element in nums appears exactly three times except for one element which appears once.
```

**Solution:**
```java
class Solution {
    public int singleNumber(int[] nums) {
        int x1 = 0, x2 = 0, mask = 0;
         
        for (int i : nums) {
            x2 ^= x1 & i;
            x1 ^= i;
            mask = ~(x1 & x2);
            x2 &= mask;
            x1 &= mask;
        }

        return x1;  // Since p = 1, in binary form p = '01', then p1 = 1, so we should return x1. 
                    // If p = 2, in binary form p = '10', then p2 = 1, and we should return x2.
                    // Or alternatively we can simply return (x1 | x2).
    }
}
```

[Explanation](https://leetcode.com/problems/single-number-ii/solutions/43295/detailed-explanation-and-generalization-of-the-bitwise-operation-method-for-single-numbers)
