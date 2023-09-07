approach 1:
```
class Solution {
public:
    int indexOfRotation(vector<int>& nums) {
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
    int binarySearch(vector<int>& nums, int target, int low, int high) {
        while (low <= high)
        {
            int mid = (high - low)/2 + low;
            if (nums[mid] == target)
                return mid;
            else if (nums[mid] < target)
                low = mid + 1;
            else
                high = mid - 1;
        }
        return -1;
    }
    int search(vector<int>& nums, int target) {
        int size = nums.size();
        int rotation = indexOfRotation(nums);
        if (nums[rotation] <= target && nums[size-1] >= target)
            return binarySearch(nums, target, rotation, size-1);
        else
            return binarySearch(nums, target, 0, rotation - 1);
    }
};

```
approach 2:
```
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int size = nums.size();
        int low = 0, high = size - 1;
        while (low <= high)
        {
            int mid = (high - low) / 2 + low;
            if (nums[mid] == target)
                return mid;
            if (nums[low] <= nums[mid])
            {
                if (nums[low] <= target && target < nums[mid])
                    high = mid - 1;
                else
                    low = mid + 1;
            }
            else if (nums[mid] <= nums[high])
            {
                if (nums[mid] < target && target <= nums[high]) 
                    low = mid + 1;
                else
                    high = mid -1;
            }

        }
        return -1;
    }
};
```
