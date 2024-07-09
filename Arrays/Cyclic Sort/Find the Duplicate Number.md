## Find the Duplicate Number

Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

You must solve the problem without modifying the array nums and uses only constant extra space.

O(n)
```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int np1 = nums.size();
        int i = 0;
        while (i < np1 - 1) {
            if (nums[i] != i+1) {
                if (nums[i] != nums[nums[i]-1])
                    swap(nums[i], nums[nums[i]-1]);
                else 
                    return nums[i];
            } else {
                i++;
            }
        }
        return nums[np1-1];
    }
};
```
