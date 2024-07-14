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

## [Strongly Connected Components in Directed Graph (Kosaraju's Algo)](https://www.geeksforgeeks.org/problems/strongly-connected-components-kosarajus-algo/1)
```cpp
#include <bits/stdc++.h>
using namespace std;




class Solution
{
private:
    void dfs(int node, vector<int> &vis, vector<int> adj[],
             stack<int> &st) {
        vis[node] = 1;
        for (auto it : adj[node]) {
            if (!vis[it]) {
                dfs(it, vis, adj, st);
            }
        }

        st.push(node);
    }
private:
    void dfs3(int node, vector<int> &vis, vector<int> adjT[]) {
        vis[node] = 1;
        for (auto it : adjT[node]) {
            if (!vis[it]) {
                dfs3(it, vis, adjT);
            }
        }
    }
public:
    //Function to find number of strongly connected components in the graph.
    int kosaraju(int V, vector<int> adj[])
    {
        vector<int> vis(V, 0);
        stack<int> st;
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                dfs(i, vis, adj, st);
            }
        }

        vector<int> adjT[V];
        for (int i = 0; i < V; i++) {
            vis[i] = 0;
            for (auto it : adj[i]) {
                // i -> it
                // it -> i
                adjT[it].push_back(i);
            }
        }
        int scc = 0;
        while (!st.empty()) {
            int node = st.top();
            st.pop();
            if (!vis[node]) {
                scc++;
                dfs3(node, vis, adjT);
            }
        }
        return scc;
    }
};

int main() {

    int n = 5;
    int edges[5][2] = {
        {1, 0}, {0, 2},
        {2, 1}, {0, 3},
        {3, 4}
    };
    vector<int> adj[n];
    for (int i = 0; i < n; i++) {
        adj[edges[i][0]].push_back(edges[i][1]);
    }
    Solution obj;
    int ans = obj.kosaraju(n, adj);
    cout << "The number of strongly connected components is: " << ans << endl;
    return 0;
}
```
