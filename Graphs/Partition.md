## Bipartite
```cpp
class Solution {
public:
    bool isBipartite(vector<vector<int>>& graph) {
        queue<int>q;
        int n = graph.size();
        vector<bool>coloured(n, 0), colour(n, 0), inQ(n, 0);
        for (int i=0; i<n; i++) {
            if (coloured[i])
                continue;
            coloured[i] = 1;
            colour[i] = 1;
            q.push(i);
            inQ[i] = 1;
            // cout << i << " "  << colour[i]  << endl;
            while(!q.empty()) {
                int top = q.front();
                q.pop();
                for (auto e : graph[top]) {
                    if (coloured[e] and colour[e] != 1 - colour[top]) {
                        return 0;
                    }
                    coloured[e] = 1;
                    colour[e] = 1 - colour[top];
                    if ( !inQ[e]) {
                        q.push(e);
                        inQ[e] = 1;
                        // cout << e << " "  << colour[e]  << endl;
                    }                     
                }
            }
        }
        return 1;
    }
};
```
