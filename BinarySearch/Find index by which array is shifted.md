Suppose an array of length n sorted in ascending order is rotated between 1 and n times. Find index by which array is shifted.
```
class Solution {
public:
    int findMin(vector<int>& nums) {
        int low = 0, high = nums.size() - 1;
        while(low < high)
        {
            int mid = (high - low)/2 + low;
            if (nums[mid] > nums[high])
                low = mid + 1;
            else
                high = mid;
        }
        return low;
    }
};
```
