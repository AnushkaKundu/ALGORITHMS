## Number Complement

The complement of an integer is the integer you get when you flip all the 0's to 1's and all the 1's to 0's in its binary representation.

For example, The integer 5 is "101" in binary and its complement is "010" which is the integer 2.

Given an integer num, return its complement.
```cpp
class Solution {
public:
    int findComplement(int n) {
        int nn = n;
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;
        return (((n - (n >> 1)) - 1) << 1) + 1 - nn;
    }
};
```
