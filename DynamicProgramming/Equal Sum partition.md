Iterative:
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
