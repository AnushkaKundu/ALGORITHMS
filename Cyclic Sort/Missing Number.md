##  Missing Number

Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

```
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size(), i = 0;
        while(i < n) {                                           // don't use for loop, increment only when nums[i] == nums[nums[i]].
            if (nums[i] < n and nums[i] != nums[nums[i]]) {
                swap(nums[i], nums[nums[i]]);
            } else {
                i++;
            }
        }
        for (int i=0; i<n; i++) {
            if (nums[i] != i)
                return i;
        }
        return n;
    }
};
```
