## Kth Largest Element in an Array
**Problem Statement:**
Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

Can you solve it without sorting?

**Examples:**
```
Example 1:
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5

Example 2:
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
 ```

**Constraints:**

```
1 <= k <= nums.length <= 105
-104 <= nums[i] <= 104
```

**Solution:**
```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        int size = nums.size();
        priority_queue<int, vector<int>, greater<int>>pq;
        for (int i = 0; i < size; i++)
        {
            if (i < k)
            {
                pq.push(nums[i]);
            }
            else
            {
                int temp = max(nums[i] , pq.top());
                pq.pop();
                pq.push(temp);
            }
        }
        return pq.top();
    }
};
```

## Kth Largest Element in a Stream
**Problem Statement:**

Design a class to find the kth largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Implement Kth Largest class:

`KthLargest(int k, int[] nums)` Initializes the object with the integer k and the stream of integers nums.
`int add(int val)` Appends the integer val to the stream and returns the element representing the kth largest element in the stream.

**Examples:**
```
Input
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
Output
[null, 4, 5, 5, 8, 8]

Explanation
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8
```

**Solution:**
```cpp
class KthLargest {
public:
    priority_queue<int, vector<int>, greater<int>> pq;
    int size;
    KthLargest(int k, vector<int> nums) {
        size=k;
        for(int i=0;i<nums.size();i++) {
            pq.push(nums[i]);
            if(pq.size()>k) pq.pop();
        }
    }
    
    int add(int val) {
        pq.push(val);
        if(pq.size()>size) pq.pop();
        return pq.top();
    }
};

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest* obj = new KthLargest(k, nums);
 * int param_1 = obj->add(val);
 */
```

## 'K' Closest Points to the Origin
**Problem Statement:**

Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0).

The distance between two points on the X-Y plane is the Euclidean distance (i.e., √(x1 - x2)2 + (y1 - y2)2).

You may return the answer in any order. The answer is guaranteed to be unique (except for the order that it is in).

**Examples:**

Example 1:
```
Input: points = [[1,3],[-2,2]], k = 1
Output: [[-2,2]]
Explanation:
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest k = 1 points from the origin, so the answer is just [[-2,2]].
```

Example 2:
```
Input: points = [[3,3],[5,-1],[-2,4]], k = 2
Output: [[3,3],[-2,4]]
Explanation: The answer [[-2,4],[3,3]] would also be accepted.
```

**Solution:**
```cpp
class Solution {
public:
    int sqDist(vector<int>& a) {
        return a[0]*a[0] + a[1]*a[1];
    }
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        auto comp = [](vector<int> a, vector<int> b) {
            return (a[0]*a[0] + a[1]*a[1] <b[0]*b[0] + b[1]*b[1]);
        };
        priority_queue<vector<int>, vector<vector<int>>, decltype(comp)> pq(comp);
        int n = points.size();
        for (int i=0; i<n; i++) {
            if (i<k) {
                pq.push(points[i]);
            } else {
                auto e = pq.top();
                if (sqDist(points[i]) < sqDist(e)) {
                    pq.pop();
                    pq.push(points[i]);
                }
            }
        }
        vector<vector<int>> ans;
        while(!pq.empty()) {
            ans.push_back(pq.top());
            pq.pop();
        }
        return ans;
    }
};
```

## Connect Ropes

Given an array of integers A representing the length of ropes.

You need to connect these ropes into one rope. The cost of connecting two ropes is equal to the sum of their lengths.

Find and return the minimum cost to connect these ropes into one rope.

**Examples:**

```
Example 1.
Input: A = [1, 2, 3, 4, 5]
Output: 33

Example 2.
Input: A = [5, 17, 100, 11]
Output: 182
```

```cpp
int solve(vector<int> &A) {
    priority_queue<int, vector<int>, greater<>>pq;
    int n = A.size(), sum = 0;
    for (int i=0; i<n; i++) {
        pq.push(A[i]);
    }    
    while(pq.size() != 1) {
        int a = pq.top();
        pq.pop();
        int b = pq.top();
        pq.pop();
        pq.push(a+b);
        sum += a + b;
    }
    return sum;
}
```

## Top K Frequent Elements

**Problem Statement:**

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

**Examples:**
```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```
```
Input: nums = [1], k = 1
Output: [1]
```

**Solution:**
```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        map<int, int>freq;
        for (auto ele : nums) {
            freq[ele]++;
        }
        auto comp = [](pair<int, int>& a, pair<int, int>& b) {
            return 1 - (a.second < b.second);
        };
        priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(comp)>pq(comp);
        int i = 0;
        for (auto ele : freq) {
            if (i<k) {
                pq.push({ele.first, ele.second});
            } else {
                auto t = pq.top();
                if (ele.second > t.second) {
                    pq.pop();
                    pq.push({ele.first, ele.second});
                }
            }
            i++;
        }
        vector<int> ans;
        while(!pq.empty()) {
            ans.push_back(pq.top().first);
            pq.pop();
        }
        return ans;
    }
};
```
## Frequency Sort

**Problem Statement:**

Given an array of integers nums, sort the array in increasing order based on the frequency of the values. If multiple values have the same frequency, sort them in decreasing order.

Return the sorted array.

**Examples:**
```
Input: nums = [1,1,2,2,2,3]
Output: [3,1,1,2,2,2]
Explanation: '3' has a frequency of 1, '1' has a frequency of 2, and '2' has a frequency of 3.
```
```
Input: nums = [2,3,1,3,2]
Output: [1,3,3,2,2]
Explanation: '2' and '3' both have a frequency of 2, so they are sorted in decreasing order.
```
```
Input: nums = [-1,1,-6,4,5,-6,1,4,1]
Output: [5,-1,4,4,-6,-6,1,1,1]
```

**Solution:**
```cpp
class Solution {
public:
    vector<int> frequencySort(vector<int>& A) {
        unordered_map<int, int> count;
        for (int a: A)
            count[a]++;
        sort(begin(A), end(A), [&](int a, int b) {
            return count[a] == count[b] ? a > b : count[a] < count[b];
        });
        return A;
    }
};
```

## Least Number of Unique Integers after K Removals

**Problem Statement:**

Given an array of integers arr and an integer k. Find the least number of unique integers after removing exactly k elements

**Examples:**
```
Input: arr = [5,5,4], k = 1
Output: 1
Explanation: Remove the single 4, only 5 is left.
```
```
Input: arr = [4,3,1,1,3,3,2], k = 3
Output: 2
Explanation: Remove 4, 2 and either one of the two 1s or three 3s. 1 and 3 will be left.
```

**Solution:**
```cpp
class Solution {
public:
    int findLeastNumOfUniqueInts(vector<int>& arr, int k) {
        unordered_map<int, int>count;
        vector<int>heap;
        for (auto ele : arr) {
            count[ele]++;
        }
        for (auto ele : count) {
            heap.push_back(ele.second);
        }
        make_heap(heap.begin(), heap.end(), greater<int>());
        while(k > 0) {
            k -= heap.front();
            pop_heap(begin(heap), end(heap), greater<int>()); 
            if (k >= 0)
                heap.pop_back();   
        }
        return heap.size();
    }
};
```
