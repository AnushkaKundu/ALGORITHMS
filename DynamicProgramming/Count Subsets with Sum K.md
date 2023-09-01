
Botton - Up:
```
int findWays(vector<int>nums, int target){
	if (target == 0) return 1;  
	
	int size = nums.size();
	int dp[size + 1][target + 1];

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
				dp[i][j] = dp[i - 1][j - nums[i - 1]] + dp[i - 1][j];
		}
	}
	return dp[size][target];
}
```
