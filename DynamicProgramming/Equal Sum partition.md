Input: Array of numbers. 

Output: Is it possible to partition the numbers of the array in 2 parts such that the sum of the elements of both partitions are equal ?

## Recursive:
```
class Solution {
public:
    bool canAchieveTarget(vector<int>& nums, int target, int currentWeight, int index) {
        if (currentWeight > target) return 0;
        if (currentWeight == target) return 1;
        if (index < 0) return 0;
        return canAchieveTarget(nums, target, currentWeight + nums[index], index - 1)
|| canAchieveTarget(nums, target, currentWeight, index - 1);
    }

    bool canPartition(vector<int>& nums) {
        int sum = accumulate(nums.begin(), nums.end(), 0);
        if (sum%2) return 0;
        int target = sum/2;

        return canAchieveTarget(nums, target, 0, nums.size()-1);
    }
};
```


# DP
## Top - Down:
```
class Solution {
public:
    bool canAchieveTarget(vector<int>& nums, int target, int index, vector<vector<int>>& dp) {
        if (target == 0) return 1;
        if (index < 0 || target < 0) return 0;
        if (dp[index][target] != -1) return dp[index][target];
        
        bool include = canAchieveTarget(nums, target - nums[index], index - 1, dp);
        bool exclude = canAchieveTarget(nums, target, index - 1, dp);
        
        return dp[index][target] = include || exclude;
    }

    bool canPartition(vector<int>& nums) {
        int sum = accumulate(nums.begin(), nums.end(), 0);

        if (sum % 2) return 0;
        int target = sum / 2;
        
        int size = nums.size();
        vector<vector<int>> dp(size, vector<int>(target + 1, -1));
        
        return canAchieveTarget(nums, target, size - 1, dp);
    }
};
```

Stats:
`
208 ms

94.9 MB
`

## Bottom - Up:
```
class Solution {
public:
    bool canAchieveTarget(vector<int>& nums, int target) {
        if (target == 0) return 1;  
        
        int size = nums.size();
        bool dp[size + 1][target + 1];

        for (int i = 0; i <= target; i++)
            dp[0][i] = 0;

        for (int i = 0; i <= size; i++) 
            dp[i][0] = 1;

        for (int i = 1; i <= size; i++)        
        {
            for (int j = 1; j <= target; j++)
            {
                if (j - nums[i - 1] < 0)
                    dp[i][j] = dp[i-1][j];
                else 
                    dp[i][j] = dp[i - 1][j - nums[i - 1]] | dp[i - 1][j];
            }
        }

        return dp[size][target];
    }

    bool canPartition(vector<int>& nums) {
        int sum = accumulate(nums.begin(), nums.end(), 0);

        if (sum & 1) return 0;
        int target = sum / 2;
        
        return canAchieveTarget(nums, target);
    }
};
```

Stats:
`
147 ms

11.7 MB
`
