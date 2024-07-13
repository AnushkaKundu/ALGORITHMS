## [No of connected components in a matrix](https://leetcode.com/problems/number-of-islands/description/)
```cpp
class Solution {
public:
    void dfs(int i, int j, int m, int n, vector<vector<bool>>& visited, vector<vector<char>>& grid)
    {
        if (i < 0 || j < 0 || i >= m || j >= n || visited[i][j] || grid[i][j] == '0')  
            return;
        visited[i][j] = 1;
        dfs(i-1, j, m, n, visited, grid);
        dfs(i+1, j, m, n, visited, grid);
        dfs(i, j-1, m, n, visited, grid);
        dfs(i, j+1, m, n, visited, grid);
    }
    int numIslands(vector<vector<char>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        vector<vector<bool>>visited(m, vector<bool>(n, 0));
        int islands = 0;
        for (int i=0; i<m; i++)
        {
            for (int j=0; j<n; j++)
            {
                if (visited[i][j] || grid[i][j] == '0')
                    continue;
                dfs(i, j, m, n, visited, grid);
                islands++;
            }
        }
        return islands;
    }
};
```

## [No of connnected components in undirected graph](https://leetcode.com/problems/number-of-provinces/description/)

```cpp
class Solution {
public:
    void dfs(vector<vector<int>>& isConnected, int i, vector<bool>& visited, int n) {
        if (visited[i])
            return;
        visited[i] = 1;
        for (int j=0; j<n; j++) {
            if (!isConnected[i][j])
                continue;
            if (visited[j])
                continue;
            dfs(isConnected, j, visited, n);
        }
    }
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        vector<bool>visited(n, 0);
        int ans = 0;
        for (int i=0; i<n; i++) {
            if (!visited[i]) {
                ans++;
                dfs(isConnected, i, visited, n);
            }
        }
        return ans;
    }
};
```

