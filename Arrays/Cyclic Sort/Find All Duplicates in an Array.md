## Find All Duplicates in an Array

Given an integer array nums of length n where all the integers of nums are in the range [1, n] and each integer appears once or twice, return an array of all the integers that appears twice.

You must write an algorithm that runs in O(n) time and uses only constant extra space.

```
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        vector<int>ans;
        int i=0, n = nums.size();
        while(i<n) {
            if (nums[i] == i+1 || nums[nums[i]-1] == nums[i])
                i++;
            else
                swap(nums[nums[i]-1], nums[i]);
        }
        for (int i=0; i<n; i++)
        {
            // cout << i+1 << " " << nums[i] << endl;
            if (nums[i] != i+1)
                ans.push_back(nums[i]);
        }
        return ans;
    }
};
```
