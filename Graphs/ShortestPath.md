## Djikstra Algorithm
```cpp
class Solution
{
	public:
	  //Function to find the shortest distance of all the vertices
    //from the source vertex S.
    vector <int> dijkstra(int V, vector<vector<int>> adj[], int S)
    {
        // Create a set ds for storing the nodes as a pair {dist,node}
        // where dist is the distance from source to the node.
        // set stores the nodes in ascending order of the distances 
        set<pair<int,int>> st; 

        // Initialising dist list with a large number to
        // indicate the nodes are unvisited initially.
        // This list contains distance from source to the nodes.
        vector<int> dist(V, 1e9); 
        
        st.insert({0, S}); 

        // Source initialised with dist=0
        dist[S] = 0;
        
        // Now, erase the minimum distance node first from the set
        // and traverse for all its adjacent nodes.
        while(!st.empty()) {
            auto it = *(st.begin()); 
            int node = it.second; 
            int dis = it.first; 
            st.erase(it); 
            
            // Check for all adjacent nodes of the erased
            // element whether the prev dist is larger than current or not.
            for(auto it : adj[node]) {
                int adjNode = it[0]; 
                int edgW = it[1]; 
                
                if(dis + edgW < dist[adjNode]) {
                    // erase if it was visited previously at 
                    // a greater cost.
                    if(dist[adjNode] != 1e9) 
                        st.erase({dist[adjNode], adjNode}); 
                        
                    // If current distance is smaller,
                    // push it into the queue
                    dist[adjNode] = dis + edgW; 
                    st.insert({dist[adjNode], adjNode}); 
                 }
            }
        }
        // Return the list containing shortest distances
        // from source to all the nodes.
        return dist; 
    }
};
```

## [Count Shortest Paths](https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/)
```cpp
#define ll long long
#define pll pair<ll, ll>
class Solution {
public:
    int MOD = 1e9 + 7;
    int countPaths(int n, vector<vector<int>>& roads) {
        vector<vector<pll>> graph(n);
        for(auto& road: roads) {
            ll u = road[0], v = road[1], time = road[2];
            graph[u].push_back({v, time});
            graph[v].push_back({u, time});
        }
        return dijkstra(graph, n, 0);
    }
    int dijkstra(const vector<vector<pll>>& graph, int n, int src) {
        vector<ll> dist(n, LONG_MAX);
        vector<ll> ways(n);
        ways[src] = 1;
        dist[src] = 0;
        priority_queue<pll, vector<pll>, greater<>> minHeap;
        minHeap.push({0, 0}); // dist, src
        while (!minHeap.empty()) {
            auto[d, u] = minHeap.top(); minHeap.pop();
            if (d > dist[u]) continue; // Skip if `d` is not updated to latest version!
            for(auto [v, time] : graph[u]) {
                if (dist[v] > d + time) {
                    dist[v] = d + time;
                    ways[v] = ways[u];
                    minHeap.push({dist[v], v});
                } else if (dist[v] == d + time) {
                    ways[v] = (ways[v] + ways[u]) % MOD;
                }
            }
        }
        return ways[n-1];
    }
};
```

## [Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/description/)

## [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/description/)
pq can't be used, since stops condition is present, so if stops exceed we have to eliminate it even if dist is more.

then check queue for checking all conditions.
```cpp
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        vector<int>distances(n+1, INT_MAX);
        distances[src] = 0;
        map<int, set<pair<int, int>>>adjM;
        for (auto ele : flights)
        {
            adjM[ele[0]].insert({ele[2], ele[1]});
        }
        // auto comp = [](vector<int>& a, vector<int>& b) {
        //     if (a[0] == b[0])
        //         return a[2] > b[2];
        //     return a[0] > b[0];
        // };
        queue<vector<int>> pq;
        pq.push({0, src, 0}); // dist, node, stops
        while(!pq.empty())
        {
            auto p = pq.front();
            pq.pop();
            if (p[2] > k)
                continue;
            for (auto ele : adjM[p[1]])
            {
                if (p[0] + ele.first < distances[ele.second] and p[2] <= k)
                {
                    distances[ele.second] = p[0] + ele.first;
                    pq.push({distances[ele.second], ele.second, p[2] + 1});
                }
            }
        }
        return distances[dst] == INT_MAX ? -1 : distances[dst];
    }
};
```

## [Network Delay Time](https://leetcode.com/problems/network-delay-time/description/)
max of all distances from src to any vertice
```cpp
class Solution {
public:
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        vector<int>distances(n+1, INT_MAX);
        distances[k] = 0;
        map<int, set<pair<int, int>>>adjM;
        for (auto ele : times)
        {
            adjM[ele[0]].insert({ele[2], ele[1]});
        }

        priority_queue<pair<int, int>> pq;
        pq.push({0, k});
        while(!pq.empty())
        {
            auto p = pq.top();
            pq.pop();
            for (auto ele : adjM[p.second])
            {
                if (p.first + ele.first < distances[ele.second])
                {
                    distances[ele.second] = p.first + ele.first;
                    pq.push({distances[ele.second], ele.second});
                }
            }
        }
        int maxi = -1;
        for (int i=1; i<=n; i++)
        {
            maxi = max(maxi, distances[i]);
        }
        return maxi == INT_MAX ? -1 : maxi;
    }
};
```
