Input: Array of numbers, a target number.
Output: Can a subset of the array sum up to the target ?

Top - Down:
```
class Solution{   
public:
    bool canAchieveTarget(vector<int>& nums, int target, int index, vector<vector<int>>& dp) {
        if (target == 0) return 1;
        if (index < 0 || target < 0) return 0;
        if (dp[index][target] != -1) return dp[index][target];
        
        bool include = canAchieveTarget(nums, target - nums[index], index - 1, dp);
        bool exclude = canAchieveTarget(nums, target, index - 1, dp);
        
        dp[index][target] = include || exclude;
        return dp[index][target];
    }
    
    bool isSubsetSum(vector<int>nums, int target){
        int size = nums.size();
        vector<vector<int>> dp(size, vector<int>(target + 1, -1));
        return canAchieveTarget(nums, target, size - 1, dp);
    }
};
```

Bottom - Up:
```
class Solution{   
public:
    bool isSubsetSum(vector<int>nums, int target){
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
};
```
