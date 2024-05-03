## [Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters/description/)

**Problem Statement:**

Given a string `s`, remove duplicate letters so that every letter appears once and only once. You must make sure your result is  the smallest in lexicographical order among all possible results.

**Examples:**
```
Input: s = "bcabc"
Output: "abc"
```
```
Input: s = "cbacdcbc"
Output: "acdb"
```

**Constraints:**

- `1 <= s.length <= 10^4`
- `s` consists of lowercase English letters.

**Solution:**
```cpp
class Solution {
public:
    string printStack(stack<char>st) {
        string s = "";
        while(!st.empty()) {
            s = char(st.top()) + s;
            st.pop();
        }
        // cout << s << endl;
        return s;
    }
    string removeDuplicateLetters(string s) {
        vector<char>left(26, 0), inAns(26, 0);
        for (auto c : s) {
            left[c-'a']++;
        }
        string ans = "";
        stack<char>st;
        for (auto c : s) {
            // cout << "\t" << c << endl;
            if (inAns[c-'a']) {
                left[c-'a']--;
                continue;
            }
            while (!st.empty() and left[st.top()-'a']>0 and st.top() > c) {
                // cout << st.top() << endl;
                inAns[st.top()-'a'] = 0;
                // printStack(st);
                st.pop();                
            }
            st.push(c);
            // ans = printStack(st);
            left[c-'a']--;
            inAns[c-'a'] = 1;
        }
        while (!st.empty()) {
            char c = st.top();
            st.pop();
            ans = c + ans;
        }
        return ans;
    }
};
```
