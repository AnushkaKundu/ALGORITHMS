## Set Mismatch

You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

You are given an integer array nums representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return them in the form of an array.

```
class Solution {
public:
    vector<int> findErrorNums(vector<int>& nums) {
        int n = nums.size(), i = 0;
        while(i<n) {
            if (nums[i] == i+1 || nums[i] == nums[nums[i]-1]) {
                i++;
            } else {
                swap(nums[i], nums[nums[i]-1]);
            }
        }
        for (int i=0; i<n; i++) {
            if (nums[i] != i+1)
                return {nums[i], i+1};
        }
        return {-1, -1};
    }
};
```
