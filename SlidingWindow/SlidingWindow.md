[List](https://leetcode.com/list/?selectedList=mxhm4ulv)

## Minimum Size Subarray Sum
Given an array of positive integers nums and a positive integer target, return the minimal length of a subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.
Example 1:

Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
Example 2:

Input: target = 4, nums = [1,4,4]
Output: 1
Example 3:

Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
 

Constraints:

1 <= target <= 109
1 <= nums.length <= 105
1 <= nums[i] <= 104
 

```
int minSubArrayLen(int s, vector<int>& A) {
    int i = 0, n = A.size(), res = n + 1;
    for (int j = 0; j < n; ++j) {
        s -= A[j];
        while (s <= 0) {
            res = min(res, j - i + 1);
            s += A[i++];
        }
    }
    return res == (n + 1) ? 0 : res;
}
```

## Minimum Size Subarray Sum with negative numbers allowed 

[Explanation](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/solutions/143726/C++JavaPython-O(N)-Using-Deque/)

Given an integer array nums and an integer k, return the length of the shortest non-empty subarray of nums with a sum of at least k. If there is no such subarray, return -1.
A subarray is a contiguous part of an array.

Example 1:

Input: nums = [1], k = 1
Output: 1
Example 2:

Input: nums = [1,2], k = 4
Output: -1
Example 3:

Input: nums = [2,-1,2], k = 3
Output: 3
 

Constraints:

1 <= nums.length <= 105
-105 <= nums[i] <= 105
1 <= k <= 109

```
int shortestSubarray(vector<int> A, int K) {
    int N = A.size(), res = N + 1;
    deque<long> d;
    for (int i = 0; i < N; i++) {
        if (i > 0)
            A[i] += A[i - 1];
        if (A[i] >= K)
            res = min(res, i + 1);
        while (d.size() > 0 && A[i] - A[d.front()] >= K)
            res = min(res, i - d.front()), d.pop_front();
        while (d.size() > 0 && A[i] <= A[d.back()])
            d.pop_back();
        d.push_back(i);
    }
    return res <= N ? res : -1;
}
```

## Count Number of Nice Subarrays
Count SA with k odd numbers.
Example 1:

Input: nums = [1,1,2,1,1], k = 3
Output: 2
Explanation: The only sub-arrays with 3 odd numbers are [1,1,2,1] and [1,2,1,1].
Example 2:

Input: nums = [2,4,6], k = 1
Output: 0
Explanation: There is no odd numbers in the array.
Example 3:

Input: nums = [2,2,2,1,2,2,1,2,2,2], k = 2
Output: 16
 

Constraints:

1 <= nums.length <= 50000
1 <= nums[i] <= 10^5
1 <= k <= nums.length

```
int numberOfSubarrays(vector<int>& A, int k) {
    return atMost(A, k) - atMost(A, k - 1);
}

int atMost(vector<int>& A, int k) {
    int res = 0, i = 0, n = A.size();
    for (int j = 0; j < n; j++) {
        k -= A[j] % 2;
        while (k < 0)
            k += A[i++] % 2;
        res += j - i + 1;
    }
    return res;
}
```
## Get Equal Substrings Within Budget
Try yourself.

## Subarrays with K Different Integers
Find Number of Subarrays with K Different Integers.

Example 1:

Input: nums = [1,2,1,2,3], k = 2
Output: 7
Explanation: Subarrays formed with exactly 2 different integers: [1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,1,2]
Example 2:

Input: nums = [1,2,1,3,4], k = 3
Output: 3
Explanation: Subarrays formed with exactly 3 different integers: [1,2,1,3], [2,1,3], [1,3,4].
 

Constraints:

1 <= nums.length <= 2 * 104
1 <= nums[i], k <= nums.length

```
int subarraysWithKDistinct(vector<int>& A, int K) {
    return atMostK(A, K) - atMostK(A, K - 1);
}
int atMostK(vector<int>& A, int K) {
    int i = 0, res = 0;
    unordered_map<int, int> count;
    for (int j = 0; j < A.size(); ++j) {
        if (!count[A[j]]++) K--;
        while (K < 0) {
            if (!--count[A[i]]) K++;
            i++;
        }
        res += j - i + 1;
    }
    return res;
}
```
## Fruit Into Baskets
Similar to prev 2.

## Frequency of the Most Frequent Element
The frequency of an element is the number of times it occurs in an array.

You are given an integer array nums and an integer k. In one operation, you can choose an index of nums and increment the element at that index by 1.

Return the maximum possible frequency of an element after performing at most k operations.

Example 1:

Input: nums = [1,2,4], k = 5
Output: 3
Explanation: Increment the first element three times and the second element two times to make nums = [4,4,4].
4 has a frequency of 3.
Example 2:

Input: nums = [1,4,8,13], k = 5
Output: 2
Explanation: There are multiple optimal solutions:
- Increment the first element three times to make nums = [4,4,8,13]. 4 has a frequency of 2.
- Increment the second element four times to make nums = [1,8,8,13]. 8 has a frequency of 2.
- Increment the third element five times to make nums = [1,4,13,13]. 13 has a frequency of 2.
Example 3:

Input: nums = [3,9,6], k = 2
Output: 1
 

Constraints:

1 <= nums.length <= 105
1 <= nums[i] <= 105
1 <= k <= 105

```
class Solution {
public:
    int maxFrequency(vector<int>& nums, int k) {
        sort(nums.begin(), nums.end());
        int left = 0;
        int ans = 0;
        long curr = 0;
        
        for (int right = 0; right < nums.size(); right++) {
            long target = nums[right];
            curr += target;
            
            while ((right - left + 1) * target - curr > k) {
                curr -= nums[left];
                left++;
            }
            
            ans = max(ans, right - left + 1);
        }
        
        return ans;
    }
};
```
## Find the Longest Equal Subarray
You are given a 0-indexed integer array nums and an integer k.

A subarray is called equal if all of its elements are equal. Note that the empty subarray is an equal subarray.

Return the length of the longest possible equal subarray after deleting at most k elements from nums.

A subarray is a contiguous, possibly empty sequence of elements within an array.

Example 1:

Input: nums = [1,3,2,3,1,3], k = 3
Output: 3
Explanation: It's optimal to delete the elements at index 2 and index 4.
After deleting them, nums becomes equal to [1, 3, 3, 3].
The longest equal subarray starts at i = 1 and ends at j = 3 with length equal to 3.
It can be proven that no longer equal subarrays can be created.
Example 2:

Input: nums = [1,1,2,2,1,1], k = 2
Output: 4
Explanation: It's optimal to delete the elements at index 2 and index 3.
After deleting them, nums becomes equal to [1, 1, 1, 1].
The array itself is an equal subarray, so the answer is 4.
It can be proven that no longer equal subarrays can be created.
 

Constraints:

1 <= nums.length <= 105
1 <= nums[i] <= nums.length
0 <= k <= nums.length

```
int longestEqualSubarray(vector<int>& nums, int k) {
    unordered_map<int,int>mp;
    int n = nums.size(), i = 0, maxf = 0;
    for (int j=0; j<n; j++) {
        mp[nums[j]]++;
        maxf = max(maxf, mp[nums[j]]);
        while(j - i + 1 - k > maxf) {
            mp[nums[i]]--;
            i++;
        }
    }
    return maxf;
}
```

## Longest Nice Subarray
You are given an array nums consisting of positive integers.

We call a subarray of nums nice if the bitwise AND of every pair of elements that are in different positions in the subarray is equal to 0.

Return the length of the longest nice subarray.

A subarray is a contiguous part of an array.

Note that subarrays of length 1 are always considered nice.

Example 1:

Input: nums = [1,3,8,48,10]
Output: 3
Explanation: The longest nice subarray is [3,8,48]. This subarray satisfies the conditions:
- 3 AND 8 = 0.
- 3 AND 48 = 0.
- 8 AND 48 = 0.
It can be proven that no longer nice subarray can be obtained, so we return 3.
Example 2:

Input: nums = [3,1,5,11,13]
Output: 1
Explanation: The length of the longest nice subarray is 1. Any subarray of length 1 can be chosen.
 

Constraints:

1 <= nums.length <= 105
1 <= nums[i] <= 109
```
int longestNiceSubarray(vector<int>& nums) {
    int used = 0, j = 0, res = 0;
    for (int i = 0; i < nums.size(); ++i) {
        while ((used & nums[i]) != 0)
            used -= nums[j++];
        used += nums[i];
        res = max(res, i - j + 1);
    }
    return res;
}
```
