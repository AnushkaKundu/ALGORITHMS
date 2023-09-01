Input: Array of numbers, a target number.

Output: All subsets that add up to target.

To find if such a solution exists or not (bool output) refer [Subset Sum or Target Sum (With repeating elements)](https://github.com/AnushkaKundu/ALGORITHMS/blob/7e920c7ba91cfe37ed0862caf90750ba8b17a875/DynamicProgramming/Subset%20Sum%20or%20Target%20Sum%20(With%20repeating%20elements).md) - Dynamic Programming

```
class Solution {
public:
    void util(vector<vector<int>>&out, vector<int>present, vector<int>&candidates, int idx, int target, int presentsum)
    {
        if (presentsum>target) return;
        if (presentsum==target)
        {
            out.push_back(present);
            return;
        }
        if (idx >= candidates.size()) return;
        int times = (target - presentsum)/candidates[idx]+1;
        for (int i=0; i<=times; i++)
        {
            util(out, present, candidates, idx+1, target, presentsum + i*candidates[idx]);
            present.push_back(candidates[idx]);
        }

    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>>out;
        vector<int>present;
        int sum = 0;
        util(out, present, candidates, 0, target, 0);
        return out;
    }
};
```
[View in leetcode](https://leetcode.com/problems/combination-sum/)
