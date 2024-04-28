## Remove Duplicates from Sorted Array II
Given an integer array nums sorted in non-decreasing order, remove some duplicates in-place such that each unique element appears at most twice. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

```
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int n = nums.size();
        if (n <= 2)
            return n;
        int replaceIdx = 2, curIdx = 2;
        while(curIdx < n) {
            nums[replaceIdx] = nums[curIdx];
            if (nums[replaceIdx-2] != nums[replaceIdx])
            {
                replaceIdx++;
            }
            curIdx++;
        }
        return replaceIdx;
    }
};
```

## Dutch national flag sorting problem
For this problem, your goal is to sort an array of 0, 1 and 2's but you must do this in place, in linear time and without any extra space (such as creating an extra array). This is called the Dutch national flag sorting problem. For example, if the input array is [2,0,0,1,2,1] then your program should output [0,0,1,1,2,2] and the algorithm should run in O(n) time.

```
void sort012(int arr[], int n)
{
    // Initialisation
    int l=0;
    int r=n-1;
     
    for(int i=0;i<n && i<=r;){
        // current element is 0
        if(arr[i]==0){
            swap(arr[l],arr[i]);
            l++;
            i++;
        }
        // current element is 2
        else if(arr[i]==2){
            swap(arr[i],arr[r]);
            r--;
        }
        // current element is 1
        else{
            i++;
        }
    }
}
```
