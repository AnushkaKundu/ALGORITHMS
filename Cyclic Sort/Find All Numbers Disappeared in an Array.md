## Find All Numbers Disappeared in an Array

Given an array nums of n integers where nums[i] is in the range [1, n], return an array of all the integers in the range [1, n] that do not appear in nums.

```
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        vector<int>ans;
        int n = nums.size(), i = 0;
        while(i < n) {
            if (nums[i] <= n and nums[i] != nums[nums[i]-1]) {
                swap(nums[i], nums[nums[i]-1]);
            } else {
                i++;
            }
        }
        for (int i=0; i<n; i++) {
            if (nums[i] != i+1)
                ans.push_back(i+1);
        }
        return ans;
    }
};
```
