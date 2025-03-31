## Longest Common Subsequence: 
![WhatsApp Image 2025-03-31 at 4 30 03 PM](https://github.com/user-attachments/assets/5df4e117-b891-453d-8881-00161c29cb4d)

## Longest Common Substring: 
### Recursive 
(diff from subsequence is introduction of count variable, count resets to zero if a particular letter doesn't match unlike subsequences hwere it remains same)
![WhatsApp Image 2025-03-31 at 4 30 16 PM (1)](https://github.com/user-attachments/assets/33d3aa9e-b341-4849-b1ce-ea6604915e0b)

### Iterative
![WhatsApp Image 2025-03-31 at 4 30 29 PM](https://github.com/user-attachments/assets/316ebc91-7bf9-4cd9-9d06-292fc63b7e47)

## Shortest Common Supersequence: 

Idea: len(SCS) = len(str1) + len(str2) - LCSubsequence(str1, str2) 
- substract LCS since, it is counted twice, since it appears in both strings.

![WhatsApp Image 2025-03-31 at 4 30 46 PM (1)](https://github.com/user-attachments/assets/b59aecad-05bc-4770-a5fc-fc622e73b5f2)

## Minimum number of insertions and deletions to convert string a to string b
= LCS(a, b)

![WhatsApp Image 2025-03-31 at 4 31 26 PM](https://github.com/user-attachments/assets/8e769980-58fc-4a2e-9c2a-da19a3e97501)

## Longest Palindromic Subsequence:
LPS(str) = LCS(str, reverse(str))

![WhatsApp Image 2025-03-31 at 4 31 36 PM](https://github.com/user-attachments/assets/e0ef7068-c828-498b-9595-e8340888fc10)

## Minumum deletions from string to make a palindrome: 
= len(str) - len(LPS(str))

![image](https://github.com/user-attachments/assets/64d154e3-b317-4d4e-9412-20acab7565bb)

## Minimum insertions to make a palindrome: 
Idea: The letters that dont participate in the LPS need to be added.
Ans = len(str) - LPS(str) 

## Longest repeating Subsequence: 
Idea: It works same as LCS with an extra condition. That is in the `if` condition, i.e.: `str1[i-1] == str2[j-1]` we add an extra constraint, `i != j`

![image](https://github.com/user-attachments/assets/6affd6a7-1959-41c7-ad08-9f4aa1deb313)

## Longest repeating and non-overlapping substring
[link](https://www.geeksforgeeks.org/longest-repeating-and-non-overlapping-substring/)

## Find if `a` is a subsequence of `b`
Idea: if a == LCS(a, b), return `true`

![image](https://github.com/user-attachments/assets/2d1b86d6-0dc1-4075-af1a-9a340384154a)

