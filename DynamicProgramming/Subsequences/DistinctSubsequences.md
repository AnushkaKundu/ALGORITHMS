Given two strings s and t, return the number of distinct subsequences of s which equals t.

The test cases are generated so that the answer fits on a 32-bit signed integer.

```cpp
class Solution {
public:
    int util(vector<vector<int>>& dp, string& s, string& t, int si, int ti, int sn, int tn, bool b = 1)
    {
        if (!b)
            return 0;
        if (ti == tn)
            return 1;
        if (si == sn)
            return 0;
        if (dp[si][ti] != -1)
            return dp[si][ti];
        if (sn - si < tn - ti)
            return dp[si][ti] = 0;
        return dp[si][ti] = util(dp, s, t, si+1, ti, sn, tn) + util(dp, s, t, si+1, ti+1, sn, tn, s[si] == t[ti]);
    }
    int numDistinct(string s, string t) {
        int si = 0, ti = 0;
        int sn = s.length(), tn = t.length();
        vector<vector<int>>dp(sn, vector<int>(tn, -1));
        return util(dp, s, t, si, ti, sn, tn);
    }
};
```
