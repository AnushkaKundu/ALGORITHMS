```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the longest increasing subsequence
int longestIncreasingSubsequence(int arr[], int n) {
    // Create a temporary vector to store the increasing subsequence
    vector<int> temp;
    temp.push_back(arr[0]);

    int len = 1;

    for (int i = 1; i < n; i++) {
        if (arr[i] > temp.back()) {
            // If arr[i] is greater than the last element of temp, extend the subsequence
            temp.push_back(arr[i]);
            len++;
        } else {
            // If arr[i] is not greater, replace the element in temp with arr[i]
            int ind = lower_bound(temp.begin(), temp.end(), arr[i]) - temp.begin();
            temp[ind] = arr[i];
        }
    }

    return len;
}

int main() {
    int arr[] = {10, 9, 2, 5, 3, 7, 101, 18};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "The length of the longest increasing subsequence is " << longestIncreasingSubsequence(arr, n);

    return 0;
}
```
