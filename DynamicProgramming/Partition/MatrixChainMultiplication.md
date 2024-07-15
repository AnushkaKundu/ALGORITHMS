## Matrix Chain Multiplication 
### Top-Down - More Space
```cpp
 #include <bits/stdc++.h>
using namespace std;

int f(vector<int>& arr, int i, int j, vector<vector<int>>& dp){
    
    // base condition
    if(i == j)
        return 0;
        
    if(dp[i][j]!=-1)
        return dp[i][j];
    
    int mini = INT_MAX;
    
    // partioning loop
    for(int k = i; k<= j-1; k++){
        
        int ans = f(arr,i,k,dp) + f(arr, k+1,j,dp) + arr[i-1]*arr[k]*arr[j];
        
        mini = min(mini,ans);
        
    }
    
    return mini;
}


int matrixMultiplication(vector<int>& arr, int N){
    
    vector<vector<int>> dp(N,vector<int>(N,-1));
    
    int i =1;
    int j = N-1;
    
    
    return f(arr,i,j,dp);
    
    
}

int main() {
	
	vector<int> arr = {10, 20, 30, 40, 50};
	
	int n = arr.size();
	
	cout<<"The minimum number of operations is "<<matrixMultiplication(arr,n);
	
	return 0;
}
```

### Bottom-up - less space
```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of operations for matrix multiplication
int matrixMultiplication(vector<int>& arr, int N) {
    // Create a DP table to store the minimum number of operations
    vector<vector<int>> dp(N, vector<int>(N, -1));

    // Initialize the diagonal elements of the DP table to 0
    for (int i = 0; i < N; i++) {
        dp[i][i] = 0;
    }

    // Loop for the length of the chain
    for (int len = 2; len < N; len++) {
        for (int i = 1; i < N - len + 1; i++) {
            int j = i + len - 1;
            dp[i][j] = INT_MAX;

            // Try different partition points to find the minimum
            for (int k = i; k < j; k++) {
                int cost = dp[i][k] + dp[k + 1][j] + arr[i - 1] * arr[k] * arr[j];
                dp[i][j] = min(dp[i][j], cost);
            }
        }
    }

    // The result is stored in dp[1][N-1]
    return dp[1][N - 1];
}

int main() {
    vector<int> arr = {10, 20, 30, 40, 50};
    int n = arr.size();

    cout << "The minimum number of operations for matrix multiplication is " << matrixMultiplication(arr, n) << endl;

    return 0;
}
```

## [Minimum cost to cut the stick](https://leetcode.com/problems/minimum-cost-to-cut-a-stick/)
```cpp
class Solution {
public:
    int util(int start, int end, vector<int>& cuts, vector<vector<int>>& dp) {
        if (start > end)
            return 0;
        if (dp[start][end] != -1)
            return dp[start][end];
        int ans = INT_MAX;
        for (int i=start; i<=end; i++) {
            ans = min(
                ans,
                cuts[end+1] - cuts[start-1]
                + util(start, i-1, cuts, dp)
                + util(i+1, end, cuts, dp)
            );
        }
        return dp[start][end] = ans;
    }
    int minCost(int n, vector<int>& cuts) {
        sort(cuts.begin(), cuts.end());
        cuts.insert(cuts.begin(), 0);
        cuts.push_back(n);
        int c = cuts.size()-2;
        vector<vector<int>>dp(c+1, vector<int>(c+1, -1));
        return util(1, c, cuts, dp);
    }
};
```
