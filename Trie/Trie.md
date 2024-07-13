## [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/description/)

A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

`Trie()` Initializes the trie object.
void `insert(String word)` Inserts the string `word` into the trie.
boolean `search(String word)` Returns true if the string `word` is in the trie (i.e., was inserted before), and `false` otherwise.
boolean `startsWith(String prefix)` Returns `true` if there is a previously inserted string word that has the prefix prefix, and `false` otherwise.

```cpp
class Trie {
private: 
    unordered_map<char, Trie*> children; 
    bool isword;
    
public:
    Trie() {
        children = {};
        isword = 0;
    }
    
    void insert(string word) {
        Trie* node = this;
        for (char ch : word) {
            if (!node->children.count(ch)) { node->children[ch] = new Trie(); }
            node = node->children[ch];
        }
        node->isword = true;
    }
    
    bool search(string word) {
        Trie* node = this;
        for (char ch : word) {
            if (!node->children.count(ch)) { return false; }
            node = node->children[ch];
        }
        return node->isword;
    }
    
    bool startsWith(string prefix) {
        Trie* node = this;
        for (char ch : prefix) {
            if (!node->children.count(ch)) { return false; }
            node = node->children[ch];
        }
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```

## [Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/description/)

**Problem Statement:**
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:

- `WordDictionary()` Initializes the object.
- `void addWord(word)` Adds word to the data structure, it can be matched later.
- `bool search(word)` Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

**Examples:**
```
Input
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]

Output
[null,null,null,null,false,true,true,true]

Explanation
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True
```

**Constraints:**
- `1 <= word.length <= 25`
- `word` in `addWord` consists of lowercase English letters.
- `word` in search consist of `'.'` or lowercase English letters.
- There will be at most `2` dots in word for search queries.
- At most `10^4` calls will be made to addWord and search.

**Solution:**

```cpp
class WordDictionary {
private: 
    unordered_map<char, WordDictionary*> children; 
    bool isword;
public:
    // Initialize your data structure here. 
    WordDictionary() {
        isword = 0;
        children = {};
    }
    
    // Adds a word into the data structure. 
    void addWord(string word) {
        WordDictionary* node = this;
        for (char ch : word) {
            if (!node->children[ch])
            { 
                node->children[ch] = new WordDictionary(); 
            }                
            node = node->children[ch];
        }
        node->isword = true;
    }
    
    // Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. 
    bool search(string word) {
        WordDictionary *node = this;
        for(int i = 0; i < word.length(); ++i){
            char c = word[i];
            if(c == '.'){
                for(auto ch: node->children)
                    if(ch.second && ch.second->search(word.substr(i+1))) return true;
                return false;
            }
            if(node->children[c] == nullptr) return false;
            node = node->children[c];
        }
        return node && node->isword;
    }
};

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary* obj = new WordDictionary();
 * obj->addWord(word);
 * bool param_2 = obj->search(word);
 */
```

## [Map Sum Pairs](https://leetcode.com/problems/map-sum-pairs/description/)

**Map:**

Maps a string key to a given value.

Returns the sum of the values that have a key with a prefix equal to a given string.


**MapSum class:**

MapSum() Initializes the MapSum object.

void insert(String key, int val) Inserts the key-val pair into the map. If the key already existed, the original key-value pair will be overridden to the new one.

int sum(string prefix) Returns the sum of all the pairs' value whose key starts with the prefix.

**Examples**
```
Input
["MapSum", "insert", "sum", "insert", "sum"]
[[], ["apple", 3], ["ap"], ["app", 2], ["ap"]]
Output
[null, null, 3, null, 5]

Explanation
MapSum mapSum = new MapSum();
mapSum.insert("apple", 3);  
mapSum.sum("ap");           // return 3 (apple = 3)
mapSum.insert("app", 2);    
mapSum.sum("ap");           // return 5 (apple + app = 3 + 2 = 5)
```

**Constraints:**

- `1 <= key.length, prefix.length <= 50`
- `key` and `prefix` consist of only lowercase English letters.
- `1 <= val <= 1000`
- At most `50` calls will be made to `insert` and `sum`.


**Solution:**
```cpp
class TrieNode {
    public:
        TrieNode *children[26];
        bool isEnd;
        int val;
        TrieNode()
        {
            isEnd = 0;
            val = 0;
            for (int i=0; i<26; i++)
            {
                children[i] = NULL;
            }
        }
};
class MapSum {
public:
    TrieNode *root;
    MapSum() {
        root = new TrieNode();
    }
    
    void insert(string key, int val) {
        TrieNode *iterator = root;
        for (auto x : key)
        {
            if (!iterator->children[x-'a'])
                iterator->children[x-'a'] = new TrieNode();
            iterator = iterator->children[x-'a'];
        }
        iterator->isEnd = 1;
        iterator->val = val;
    }
    
    int tempSum(TrieNode* iterator)
    {
        int sum = 0;
        if (iterator->isEnd)
            sum += iterator->val;
        for (int i=0; i<26; i++)
        {
            if (!iterator->children[i])
                continue;
            sum += tempSum(iterator->children[i]);
        }
        return sum;
    }
    
    int sum(string prefix) {
        int sum = 0;
        TrieNode *iterator = root;
        for (auto x : prefix)
        {
            if (!iterator->children[x-'a'])
                return 0;
            iterator = iterator->children[x-'a'];
        }
        return tempSum(iterator);
    }
};

/**
 * Your MapSum object will be instantiated and called as such:
 * MapSum* obj = new MapSum();
 * obj->insert(key,val);
 * int param_2 = obj->sum(prefix);
 */
```

## [Replace Words](https://leetcode.com/problems/replace-words/description/)

In English, we have a concept called `root`, which can be followed by some other word to form another longer word - let's call this word `successor`. For example, when the `root` "help" is followed by the `successor` word "ful", we can form a new word "helpful".

Given a dictionary consisting of many roots and a `sentence` consisting of words separated by spaces, replace all the successors in the sentence with the root forming it. If a successor can be replaced by more than one `root`, replace it with the root that has the shortest length.

Return the `sentence` after the replacement.

**Examples:**
```
Input: dictionary = ["cat","bat","rat"], sentence = "the cattle was rattled by the battery"
Output: "the cat was rat by the bat"
```
```
Input: dictionary = ["a","b","c"], sentence = "aadsfasf absbs bbab cadsfafs"
Output: "a a b c"
```

**Constraints:**
- `1 <= dictionary.length <= 1000`
- `1 <= dictionary[i].length <= 100`
- `dictionary[i]` consists of only lower-case letters.
- `1 <= sentence.length <= 10^6`
- `sentence` consists of only lower-case letters and spaces.
- The number of words in `sentence` is in the range `[1, 1000]`
- The length of each word in `sentence` is in the range `[1, 1000]`
- Every two consecutive words in `sentence` will be separated by exactly one space.
- `sentence` does not have leading or trailing spaces.

**Solution:**
```cpp
  class TrieNode {
public:
    TrieNode *children[26];
    bool isEnd;
    TrieNode () {
        isEnd = 0;
        for (int i=0; i<26; i++)
        {
            children[i] = NULL;
        }
    }
};
class Trie {
public:
    TrieNode* root;
    Trie() {
        root = new TrieNode();
    }
    void insert(string key)
    {
        TrieNode *iterator = root;
        for (auto x : key)
        {
            if (!iterator->children[x-'a'])
                iterator->children[x-'a'] = new TrieNode();
            iterator = iterator->children[x-'a'];
        }
        iterator->isEnd = 1;
    }
    string replace(string word)
    {
        TrieNode *iterator = root;
        for (int i=0; i<word.length(); i++)
        {
            char x  = word[i];
            if (!iterator->children[x-'a'])
                return word;
            if (iterator->children[x-'a']->isEnd == 1) 
                return word.substr(0, i+1);
            iterator = iterator->children[x-'a'];
        }
        return word;
    }
};
class Solution {
public: 
    string replaceWords(vector<string>& dictionary, string sentence) {
        istringstream iss(sentence);
        Trie *trie = new Trie();
        for (auto ele : dictionary)
        {
            trie->insert(ele);
        }
        bool first = 1;
        string out = "";
        while (iss >> sentence) {
            if (first)
                first = 0;
            else
                out += " ";
            out += trie->replace(sentence);
        }
        return out;
    }
};
```

## [Longest Word in Dictionary](https://leetcode.com/problems/longest-word-in-dictionary/description/)

**Problem Statement:**

Given an array of strings words representing an English Dictionary, return the longest word in words that can be built one character at a time by other words in words.

If there is more than one possible answer, return the longest word with the smallest lexicographical order. If there is no answer, return the empty string.

Note that the word should be built from left to right with each additional character being added to the end of a previous word. 

**Examples:**
```
Input: words = ["w","wo","wor","worl","world"]
Output: "world"
Explanation: The word "world" can be built one character at a time by "w", "wo", "wor", and "worl".
```
```
Input: words = ["a","banana","app","appl","ap","apply","apple"]
Output: "apple"
Explanation: Both "apply" and "apple" can be built from other words in the dictionary. However, "apple" is lexicographically smaller than "apply".
```

**Constraints:**
- `1 <= words.length <= 1000`
- `1 <= words[i].length <= 30`
- `words[i]` consists of lowercase English letters.

**Solution:**
```cpp
class Trie {
private: 
    unordered_map<char, Trie*> children; 
    bool isword;
    
public:
    Trie() {
        children = {};
        isword = 0;
    }
    
    void insert(string word) {
        Trie* node = this;
        for (char ch : word) {
            if (!node->children.count(ch)) { node->children[ch] = new Trie(); }
            node = node->children[ch];
        }
        node->isword = true;
    }
    
    bool search(string word) {
        Trie* node = this;
        for (char ch : word) {
            if (!node->children.count(ch)) { return false; }
            node = node->children[ch];
        }
        return node->isword;
    }
    
    bool check (string& word) {
        Trie* node = this;
        for (char ch : word) {
            if (!node->children.count(ch)) { return false; }
            node = node->children[ch];
            if (!node->isword)
                return false;
        }
        return node->isword;
    }
};
class Solution {
private:
    bool larger(string& a, string& b) {
        int l = a.length();
        for (int i=0; i<l; i++) {
            if (a[i] == b[i])
                continue;
            return a[i] > b[i];
        }
        return 0;
    }
public:
    string longestWord(vector<string>& words) {
        Trie *trie = new Trie();
        // sort(words.begin(), words.end(), greater<>);
        for (auto word : words) {
            trie->insert(word);
        }
        int ml = 0;
        string ans = "";
        for (auto word : words) {
            int w = word.length();
            if (w < ml || (w == ml && larger(word, ans)))
                continue;
            if (trie->check(word)) {
                ml = w;
                ans = word;
            }
        }
        return ans;
    }
};
```

## [Maximum XOR of Two Numbers in an Array](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/description/)

**Problem Statement:**

Given an integer array nums, return the maximum result of `nums[i]` XOR `nums[j]`, where `0 <= i <= j < n`.

**Example:**
```
Input: nums = [3,10,5,25,2,8]
Output: 28
Explanation: The maximum result is 5 XOR 25 = 28.
```
```
Input: nums = [14,70,53,83,49,91,36,80,92,51,66,70]
Output: 127
```

**Constraints:**

- `1 <= nums.length <= 2 * 10^5`
- `0 <= nums[i] <= 2^31 - 1`

**Solution:**
```cpp
class TrieNode{
public:
    TrieNode *child[2];
    
    TrieNode(){
        this->child[0] = NULL; //for 0 bit 
        this->child[1] = NULL; //for 1 bit
    }

    void insert(int x){
        TrieNode *t = this;
        bitset<32> bs(x);
        
        for(int j=31; j>=0; j--){
            if(!t->child[bs[j]]) 
                t->child[bs[j]] = new TrieNode();
            t = t->child[bs[j]];
        }    
    }

    int maxXOR(int n){
        TrieNode *t = this;
        bitset<32> bs(n);
        int ans=0; 
        for(int j=31; j>=0; j--){
            if(t->child[!bs[j]]) {
                ans += (1<<j);
                t = t->child[!bs[j]];
            }
            else t = t->child[bs[j]];
        }
        return ans;
    }
};
class Solution {
public:
    int findMaximumXOR(vector<int>& nums) {
        TrieNode trie;
        for(auto &n : nums) 
            trie.insert(n); 
        
        int ans=0;
        for(auto n : nums){
            ans = max(ans, trie.maxXOR(n)); 
        }
        return ans;
    }
};
```

## [Word Search II](https://leetcode.com/problems/word-search-ii/description/)

**Problem Statement:**
Given an `m x n` board of characters and a list of strings `words`, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

**Examples:**

![Example 1 image](https://assets.leetcode.com/uploads/2020/11/07/search1.jpg "Example 1")
```
Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]
```
![Example 2 image](https://assets.leetcode.com/uploads/2020/11/07/search2.jpg "Example 2")
```
Input: board = [["a","b"],["c","d"]], words = ["abcb"]
Output: []
```

**Constraints:**
- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 12`
- `board[i][j]` is a lowercase English letter.
- `1 <= words.length <= 3 * 10^4`
- `1 <= words[i].length <= 10`
- `words[i]` consists of lowercase English letters.
- All the strings of words are unique.

**Solution:**
```cpp
```

## [Palindrome Pairs](https://leetcode.com/problems/palindrome-pairs/description/)

**Problem Statement:**

You are given a 0-indexed array of unique strings words.

A palindrome pair is a pair of integers `(i, j)` such that:

`0 <= i, j < words.length`, `i != j`, and `words[i] + words[j]` (the concatenation of the two strings) is a  palindrome.

Return an array of all the palindrome pairs of words.

You must write an algorithm with **O(sum of words[i].length)** runtime complexity.

**Examples:**
```
Input: words = ["abcd","dcba","lls","s","sssll"]
Output: [[0,1],[1,0],[3,2],[2,4]]
Explanation: The palindromes are ["abcddcba","dcbaabcd","slls","llssssll"]
```
```
Input: words = ["bat","tab","cat"]
Output: [[0,1],[1,0]]
Explanation: The palindromes are ["battab","tabbat"]
```
```
Input: words = ["a",""]
Output: [[0,1],[1,0]]
Explanation: The palindromes are ["a","a"]
```

**Constraints:**

- `1 <= words.length <= 5000`
- `0 <= words[i].length <= 300`
- `words[i]` consists of lowercase English letters.

**Solution:**
```cpp
```

## [Design Search Autocomplete System](https://aaronice.gitbook.io/lintcode/data_structure/design-search-autocomplete-system)

**Problem Statement:**

Design a search autocomplete system for a search engine. Users may input a sentence (at least one word and end with a special character '#').

You are given a string array sentences and an integer array times both of length n where sentences[i] is a previously typed sentence and times[i] is the corresponding number of times the sentence was typed. For each input character except '#', return the top 3 historical hot sentences that have the same prefix as the part of the sentence already typed.

Here are the specific rules:

- The hot degree for a sentence is defined as the number of times a user typed the exactly same sentence before.
- The returned top `3` hot sentences should be sorted by hot degree (The first is the hottest one). If several sentences have the same hot degree, use ASCII-code order (smaller one appears first).
- If less than `3` hot sentences exist, return as many as you can.
- When the input is a special character, it means the sentence ends, and in this case, you need to return an empty list.

Implement the `AutocompleteSystem` class:

- `AutocompleteSystem(String[] sentences, int[] times)` Initializes the object with the sentences and times arrays.
- `List<String> input(char c)` This indicates that the user typed the character c.
- Returns an empty array `[]` if `c == '#'` and stores the inputted sentence in the system.
- Returns the top `3` historical hot sentences that have the same prefix as the part of the sentence already typed. If there are fewer than `3` matches, return them all.

**Examples:**
```
Input: 
["AutocompleteSystem", "input", "input", "input", "input"]
[[["i love you", "island", "iroman", "i love leetcode"], [5, 3, 2, 2]], ["i"], [" "], ["a"], ["#"]]

Output: 
[null, ["i love you", "island", "i love leetcode"], ["i love you", "i love leetcode"], [], []]

Explanation:

AutocompleteSystem obj = new AutocompleteSystem(["i love you", "island", "iroman", "i love leetcode"], [5, 3, 2, 2]);
obj.input("i");
// return ["i love you", "island", "i love leetcode"].
// There are four sentences that have prefix "i".
// Among them, "ironman" and "i love leetcode" have same hot degree.
// Since ' ' has ASCII code 32 and 'r' has ASCII code 114, "i love leetcode" should be in front of "ironman".
// Also we only need to output top 3 hot sentences, so "ironman" will be ignored.

obj.input(" ");
// return ["i love you", "i love leetcode"].
// There are only two sentences that have prefix "i ".

obj.input("a");
// return [].
// There are no sentences that have prefix "i a".

obj.input("#");
// return [].
// The user finished the input, the sentence "i a" should be saved as a historical sentence in system.
// And the following input will be counted as a new search.
```

**Constraints:**

- `n == sentences.length`
- `n == times.length`
- `1 <= n <= 100`
- `1 <= sentences[i].length <= 100`
- `1 <= times[i] <= 50`
- `c` is a lowercase English letter, a hash `'#'`, or space `' '`.
- Each tested sentence will be a sequence of characters c that end with the character '#'.
- Each tested sentence will have a length in the range `[1, 200]`.
- The words in each input sentence are separated by single spaces.
- At most `5000` calls will be made to `input`.

**Solution:**
```java
public class AutocompleteSystem {
    class Node {
        Node(String st, int t) {
            sentence = st;
            times = t;
        }
        String sentence;
        int times;
    }
    class Trie {
        int times;
        Trie[] branches = new Trie[27];
    }
    public int int_(char c) {
        return c == ' ' ? 26 : c - 'a';
    }
    public void insert(Trie t, String s, int times) {
        for (int i = 0; i < s.length(); i++) {
            if (t.branches[int_(s.charAt(i))] == null)
                t.branches[int_(s.charAt(i))] = new Trie();
            t = t.branches[int_(s.charAt(i))];
        }
        t.times += times;
    }
    public List < Node > lookup(Trie t, String s) {
        List < Node > list = new ArrayList < > ();
        for (int i = 0; i < s.length(); i++) {
            if (t.branches[int_(s.charAt(i))] == null)
                return new ArrayList < Node > ();
            t = t.branches[int_(s.charAt(i))];
        }
        traverse(s, t, list);
        return list;
    }
    public void traverse(String s, Trie t, List < Node > list) {
        if (t.times > 0)
            list.add(new Node(s, t.times));
        for (char i = 'a'; i <= 'z'; i++) {
            if (t.branches[i - 'a'] != null)
                traverse(s + i, t.branches[i - 'a'], list);
        }
        if (t.branches[26] != null)
            traverse(s + ' ', t.branches[26], list);
    }
    Trie root;
    public AutocompleteSystem(String[] sentences, int[] times) {
        root = new Trie();
        for (int i = 0; i < sentences.length; i++) {
            insert(root, sentences[i], times[i]);
        }
    }
    String cur_sent = "";
    public List < String > input(char c) {
        List < String > res = new ArrayList < > ();
        if (c == '#') { 
            insert(root, cur_sent, 1);
            cur_sent = "";
        } else {
            cur_sent += c;
            List < Node > list = lookup(root, cur_sent);
            Collections.sort(list, (a, b) -> a.times == b.times ? a.sentence.compareTo(b.sentence) : b.times - a.times);
            for (int i = 0; i < Math.min(3, list.size()); i++)
                res.add(list.get(i).sentence);
        }
        return res;
    }
}
```

## [Number of Distinct Substrings in a String](https://www.naukri.com/code360/problems/count-distinct-substrings_985292?utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_tries_videos)

Given a string 'S', you are supposed to return the number of distinct substrings(including empty substring) of the given string. You should implement the program using a trie.


Sample Input 1 :
2
sds
abc

Sample Output 1 :
6
7

Explanation of Sample Input 1 :

In the first test case, the 6 distinct substrings are { ‘s’,’ d’, ”sd”, ”ds”, ”sds”, “” }

In the second test case, the 7 distinct substrings are {‘a’, ‘b’, ‘c’, “ab”, “bc”, “abc”, “” }.

Sample Input 2 :
2
aa
abab

Sample Output 2 :
3
8

Explanation of Sample Input 2 :

In the first test case, the two distinct substrings are {‘a’, “aa”, “” }.

In the second test case, the seven distinct substrings are {‘a’, ‘b’, “ab”, “ba”, “aba”, “bab”, “abab”, “” }


```cpp
#include <bits/stdc++.h>
class Trie {
private: 
    vector<Trie*> children; 
    bool isword;
    int words;

public:
    Trie() {
        children = vector<Trie*>(26, nullptr);
        isword = false;
        words = 0;
    }
    
    void insert(string word) {
        Trie* node = this;
        for (char ch : word) {
            if (!node->children[ch - 'a']) {
                node->children[ch - 'a'] = new Trie();
            }
            node = node->children[ch - 'a'];
        }
        if (!node->isword) {
            words++;
        }
        node->isword = true;
    }

    bool search(string word) {
        Trie* node = this;
        for (char ch : word) {
            if (!node->children[ch - 'a']) {
                return false;
            }
            node = node->children[ch - 'a'];
        }
        return node->isword;
    }

    int getWords() {
        return words;
    }
};
int countDistinctSubstrings(string &s)
{
    int n = s.length();
    Trie trie;
    for (int i=0; i<n; i++)
        for (int j=i; j<n; j++) {
            string ss = s.substr(i, j-i+1);
            if (!trie.search(ss)) {
                trie.insert(ss);
            }
        }
            
    return trie.getWords() + 1;
}
```
