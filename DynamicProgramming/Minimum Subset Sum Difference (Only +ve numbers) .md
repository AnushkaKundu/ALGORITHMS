Problem Statement

Input: Array of numbers.
Output: Minimum possible absolute difference between the sum of elements of the 2 partitions of the array.

```
int minSubsetSumDifference(vector<int>& nums, int n)
{
	int sum = accumulate(nums.begin(), nums.end(), 0);
	int target = sum / 2;
	int size = n;

	bool dp[size + 1][target + 1];

	for (int i = 1; i <= target; i++)
	{
		dp[0][i] = 0;
	}

	for (int i = 0; i <= size; i++)
	{
		dp[i][0] = 1;
	}

	for (int i = 1; i <= size; i++)
	{
		for (int j=1; j<=target; j++)
		{
			if (j - nums[i - 1] < 0)
				dp[i][j] = dp[i-1][j];
			else
				dp[i][j] = dp[i - 1][j - nums[i - 1]] | dp[i-1][j];
		}
	}

	for (int i = target; i >=0 ; i--)
	{
		if (dp[size][i] == 1) return sum - 2 * i;
	}
	return sum;
}
```

[View in Coding Ninjas](https://www.codingninjas.com/studio/problems/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum_842494?leftPanelTab=0)
