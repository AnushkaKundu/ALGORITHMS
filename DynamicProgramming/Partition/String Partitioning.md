# Evaluating or Partitioning a string as per given rules
## [Palindrome Partitioning]()

Given a string, a partitioning of the string is a palindrome partitioning if every substring of the partition is a palindrome. 
Example:
  “aba|b|bbabb|a|b|aba” is a palindrome partitioning of “ababbbabbababa”.

### Problem Statement: 
Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.

**Example 1:**

Input: s = "aab"

Output: [["a","a","b"],["aa","b"]]

**Example 2:**

Input: s = "a"

Output: [["a"]]

### Solution: 
[video link](https://youtu.be/szKVpQtBHh8?si=ihykjmLN7-tLqWYt)

```python3
class Solution(object):
    @cache  # the memory trick can save some time
    def partition(self, s):
        if not s: return [[]]
        ans = []
        for i in range(1, len(s) + 1):
            if s[:i] == s[:i][::-1]:  # prefix is a palindrome
                for suf in self.partition(s[i:]):  # process suffix recursively
                    ans.append([s[:i]] + suf)
        return ans
```

## [Boolean Parenthesization - Evaluate Expression to True](https://www.geeksforgeeks.org/boolean-parenthesization-problem-dp-37/)

Given a boolean expression with the following symbols:

### Symbols:
- `'T'` — true  
- `'F'` — false  

And the following operators placed between symbols:

### Operators:
- `&` — Boolean AND  
- `|` — Boolean OR  
- `^` — Boolean XOR  

Count the number of ways we can parenthesize the expression so that the value of the expression evaluates to `true`.

## Example

**Input:**  
```plaintext
symbol[]    = {T, F, T}  
operator[]  = {^, &}
```

### Solution: 
#### [Naive Approach] – Using Recursion – O(2^n) Time and O(n^2) Space
```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to evaluate a
// boolean condition.
bool evaluate(bool b1, bool b2, char op)
{
    if (op == '&')
    {
        return b1 & b2;
    }
    else if (op == '|')
    {
        return b1 | b2;
    }
    return b1 ^ b2;
}

// Function which returns the number of ways
// s[i:j] evaluates to req.
int countRecur(int i, int j, bool req, string &s)
{

    // Base case:
    if (i == j)
    {
        return (req == (s[i] == 'T')) ? 1 : 0;
    }

    int ans = 0;
    for (int k = i + 1; k < j; k += 1)
    {

        // Count Ways in which left substring
        // evaluates to true and false.
        int leftTrue = countRecur(i, k - 1, 1, s);
        int leftFalse = countRecur(i, k - 1, 0, s);

        // Count Ways in which right substring
        // evaluates to true and false.
        int rightTrue = countRecur(k + 1, j, 1, s);
        int rightFalse = countRecur(k + 1, j, 0, s);

        // Check if the combinations results
        // to req.
        if (evaluate(true, true, s[k]) == req)
        {
            ans += leftTrue * rightTrue;
        }
        if (evaluate(true, false, s[k]) == req)
        {
            ans += leftTrue * rightFalse;
        }
        if (evaluate(false, true, s[k]) == req)
        {
            ans += leftFalse * rightTrue;
        }
        if (evaluate(false, false, s[k]) == req)
        {
            ans += leftFalse * rightFalse;
        }
    }

    return ans;
}
int countWays(string s)
{
    int n = s.length();
    return countRecur(0, n - 1, 1, s);
}

int main()
{
    string s = "T|T&F^T";
    cout << countWays(s);
    return 0;
}
```

Why use DP? 
1. Optimal Substructure: Number of ways to make expression s[i, j] evaluate to req depends on the optimal solutions of countWays(i, k-1, 0), countWays(i, k-1, 1), countWays(k+1, j, 0) and countWays(k+1, j, 1) where k lies between i and j.


2. Overlapping Subproblems: While applying a recursive approach in this problem, we notice that certain subproblems are computed multiple times. For example, countWays(0, 4, 1) and countWays(0, 7, 1) will call the same subproblem countWays(0, 2, 0) twice.

#### [Expected Approach 1]- Using Top-Down DP – O(n^3) Time and O(n^2) Space
[link to video - recursive](https://www.youtube.com/watch?v=pGVguAcWX4g&list=PL_z_8CaSLPWekqhdCPmFohncHwz8TY2Go&index=39)

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to evaluate a
// boolean condition.
bool evaluate(int b1, int b2, char op)
{
    if (op == '&')
    {
        return b1 & b2;
    }
    else if (op == '|')
    {
        return b1 | b2;
    }
    return b1 ^ b2;
}

// Function which returns the number of ways
// s[i:j] evaluates to req.
int countRecur(int i, int j, int req, string &s, vector<vector<vector<int>>> &memo)
{

    // Base case:
    if (i == j)
    {
        return (req == (s[i] == 'T')) ? 1 : 0;
    }

    // If value is memoized
    if (memo[i][j][req] != -1)
        return memo[i][j][req];

    int ans = 0;
    for (int k = i + 1; k < j; k += 1)
    {

        // Count Ways in which left substring
        // evaluates to true and false.
        int leftTrue = countRecur(i, k - 1, 1, s, memo);
        int leftFalse = countRecur(i, k - 1, 0, s, memo);

        // Count Ways in which right substring
        // evaluates to true and false.
        int rightTrue = countRecur(k + 1, j, 1, s, memo);
        int rightFalse = countRecur(k + 1, j, 0, s, memo);

        // Check if the combinations results
        // to req.
        if (evaluate(1, 1, s[k]) == req)
        {
            ans += leftTrue * rightTrue;
        }
        if (evaluate(1, 0, s[k]) == req)
        {
            ans += leftTrue * rightFalse;
        }
        if (evaluate(0, 1, s[k]) == req)
        {
            ans += leftFalse * rightTrue;
        }
        if (evaluate(0, 0, s[k]) == req)
        {
            ans += leftFalse * rightFalse;
        }
    }

    return memo[i][j][req] = ans;
}
int countWays(string s)
{
    int n = s.length();
    vector<vector<vector<int>>> memo(n, vector<vector<int>>(n, vector<int>(2, -1)));
    return countRecur(0, n - 1, 1, s, memo);
}

int main()
{

    string s = "T|T&F^T";
    cout << countWays(s);
    return 0;
}
```

#### [Expected Approach 2]- Using Bottom-Up DP – O(n^3) Time and O(n^2) Space

[link to video - iterative](https://youtu.be/bzXM1Zond9U?si=tztIjLNCtxaVfT_y)

This problem is solved using tabulation (bottom-up DP). We define a 3D DP table where:

dp[i][j][1] stores the number of ways the subexpression s[i:j] evaluates to True.

dp[i][j][0] stores the number of ways the subexpression s[i:j] evaluates to False.

To fill the DP table, we iterate over all possible substrings s[i:j] and break them into two parts at every operator s[k]. The left part is s[i:k-1], and the right part is s[k+1:j]. Based on the operator (&, |, ^), we compute the number of ways to get True and False.

The final result is stored in dp[0][n-1][1], which gives the total ways to evaluate the full expression to True. 
```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to evaluate a boolean condition.
bool evaluate(int b1, int b2, char op)
{
    if (op == '&')
        return b1 & b2;
    if (op == '|')
        return b1 | b2;
    return b1 ^ b2;
}

// Function to count ways to parenthesize the expression to get 'True'
int countWays(string s)
{
    int n = s.length();
    vector<vector<vector<int>>> dp(n, vector<vector<int>>(n, vector<int>(2, 0)));

    // Base case: Single operands (T or F)
    for (int i = 0; i < n; i += 2)
    {
        dp[i][i][1] = (s[i] == 'T');
        dp[i][i][0] = (s[i] == 'F');
    }

    // Iterate over different substring lengths
    for (int len = 2; len < n; len += 2)
    {    
        // len increases by 2 (odd indices are operators)
        for (int i = 0; i < n - len; i += 2)
        {
            int j = i + len;
            
            // Reset values for the current subproblem
            dp[i][j][0] = dp[i][j][1] = 0; 

            for (int k = i + 1; k < j; k += 2)
            { // Iterate over operators
                char op = s[k];
                int leftTrue = dp[i][k - 1][1], leftFalse = dp[i][k - 1][0];
                int rightTrue = dp[k + 1][j][1], rightFalse = dp[k + 1][j][0];

                // Count ways to get True or False
                if (evaluate(1, 1, op))
                    dp[i][j][1] += leftTrue * rightTrue;
                if (evaluate(1, 0, op))
                    dp[i][j][1] += leftTrue * rightFalse;
                if (evaluate(0, 1, op))
                    dp[i][j][1] += leftFalse * rightTrue;
                if (evaluate(0, 0, op))
                    dp[i][j][1] += leftFalse * rightFalse;

                if (!evaluate(1, 1, op))
                    dp[i][j][0] += leftTrue * rightTrue;
                if (!evaluate(1, 0, op))
                    dp[i][j][0] += leftTrue * rightFalse;
                if (!evaluate(0, 1, op))
                    dp[i][j][0] += leftFalse * rightTrue;
                if (!evaluate(0, 0, op))
                    dp[i][j][0] += leftFalse * rightFalse;
            }
        }
    }
    
    // Return ways to make entire expression True
    return dp[0][n - 1][1]; 
}

int main()
{
    string s = "T|T&F^T";
    cout << countWays(s) << endl;
    return 0;
}
```

## [Scramble String](https://www.interviewbit.com/problems/scramble-string/)
Given a string `s1`, we may represent it as a binary tree by partitioning it into two non-empty substrings recursively.

### Example Representation

Below is one possible representation of `A = "great"`:

```plaintext
    great
   /    \
  gr    eat
 / \    /  \
g   r  e   at
           / \
          a   t
```

To scramble the string, we may choose any non-leaf node and swap its two children.

For example, if we choose the node “gr” and swap its two children, it produces a scrambled string “rgeat”.

```plaintext
    rgeat
   /    \
  rg    eat
 / \    /  \
r   g  e   at
           / \
          a   t
```

We say that “rgeat” is a scrambled string of “great”.

Similarly, if we continue to swap the children of nodes “eat” and “at”, it produces a scrambled string “rgtae”.

```plaintext
    rgtae
   /    \
  rg    tae
 / \    /  \
r   g  ta  e
       / \
      t   a
```

We say that “rgtae” is a scrambled string of “great”.


### Problem Statement: 
Given two strings A and B of the same length, determine if B is a scrambled string of S.

Evaluate if one string is a scrambled version of another using recursion.

Input Format:

The first argument of input contains a string A.  
The second argument of input contains a string B.  

Output Format:

Return an integer, 0 or 1:  
    => 0 : False  
    => 1 : True  

Constraints:

1 <= len(A), len(B) <= 50  

Examples:

Input 1:  
    A = "we"  
    B = "we"  

Output 1:  
    1  

Input 2:  
    A = "phqtrnilf"  
    B = "ilthnqrpf"  

Output 2:  
    0  

### Solution - Recursive (memoized)
```cpp
unordered_map<string, bool> memo;

bool solveMemo(const string& a, const string& b) {
    int n = a.length();
    if (a == b) return true;
    if (n <= 1) return false;

    string key = a + " " + b;
    if (memo.find(key) != memo.end()) {
        return memo[key];
    }

    bool flag = false;
    for (int k = 1; k <= n - 1; k++) {
        bool test1 = (solveMemo(a.substr(0, k), b.substr(n - k, k)) &&
                      solveMemo(a.substr(k, n - k), b.substr(0, n - k)));
        bool test2 = (solveMemo(a.substr(0, k), b.substr(0, k)) &&
                      solveMemo(a.substr(k, n - k), b.substr(k, n - k)));
        
        if (test1 || test2) {
            flag = true;
            break;
        }
    }

    return memo[key] = flag;
}

int Solution::isScramble(const string A, const string B) {
    memo.clear();
    if (A.length() != B.length()) return 0;
    return solveMemo(A, B) ? 1 : 0;
}
```

### Solution - Iter
```cpp
int Solution::isScramble(const string A, const string B) {
    int la = A.length(), lb = B.length();
    
    if (la != lb)
        return 0;

    int len = la;
    int dp[len + 1][len][len];
    memset(dp, 0, sizeof(dp));

    // Base case: single character comparison
    for (int i = 0; i < len; i++) {
        for (int j = 0; j < len; j++) {
            dp[0][i][j] = 1;
            if (A[i] == B[j])
                dp[1][i][j] = 1;
        }
    }

    // Building up the solution for longer substrings
    for (int k = 2; k <= len; k++) {
        for (int i = 0; i <= len - k; i++) {
            for (int j = 0; j <= len - k; j++) {
                bool flag = false;
                for (int l = 1; l < k; l++) {
                    if ((dp[l][i][j] && dp[k - l][i + l][j + l]) || 
                        (dp[l][i][j + k - l] && dp[k - l][i + l][j])) {
                        flag = true;
                        break;
                    }
                }
                dp[k][i][j] = flag;
            }
        }
    }
    return dp[len][0][0];
}
```

## [Egg dropping problem](geeksforgeeks.org/egg-dropping-puzzle-dp-11/)

You are given n identical eggs and you have access to a k-floored building from 1 to k.

There exists a floor f where 0 <= f <= k such that any egg dropped from a floor higher than f will break, and any egg dropped from or below floor f will not break. There are a few rules given below:

- An egg that survives a fall can be used again.
- A broken egg must be discarded.
- The effect of a fall is the same for all eggs.
- If the egg doesn’t break at a certain floor, it will not break at any floor below.
- If the egg breaks on a certain floor, it will break on any floor above.
- Your task is to find the minimum number of moves you need to determine the value of f with certainty.

[Refer for soln](https://www.geeksforgeeks.org/egg-dropping-puzzle-dp-11/)

