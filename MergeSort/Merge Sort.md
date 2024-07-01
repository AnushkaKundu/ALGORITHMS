## Inversion Count
For a given integer array/list 'ARR' of size 'N' containing all distinct values, find the total number of 'Inversions' that may exist.

An inversion is defined for a pair of integers in the array/list when the following two conditions are met.

A pair ('ARR[i]', 'ARR[j]') is said to be an inversion when:

1. 'ARR[i] > 'ARR[j]' 
2. 'i' < 'j'

Where 'i' and 'j' denote the indices ranging from [0, 'N').

```cpp
#include <bits/stdc++.h>
using namespace std;

int mergesort_inv(int a[], int tmp[], int l, int r);

int merge_inv(int a[], int tmp[], int l, int half, int r);

// sorts and returns the inversions
int mergeSort(int a[], int n)	
{
	int tmp[n];
	return mergesort_inv(a, tmp, 0, n - 1);
}

int mergesort_inv(int a[], int tmp[], int l, int r)	// merges and returns the inversions
{
	int half, inv_cnt = 0;
	if (r > l)
	{
		half = (r + l) / 2;
		/*divide and call mergesort_inv function for both the parts*/
		inv_cnt = inv_cnt + mergesort_inv(a, tmp, l, half);
		inv_cnt = inv_cnt + mergesort_inv(a, tmp, half + 1, r);

        // merge the two parts
		inv_cnt += merge_inv(a, tmp, l, half + 1, r);	
	}
	return inv_cnt;
}

// merge and return the inversions
int merge_inv(int a[], int tmp[], int l, int half, int r)
{
	int i, j, k;
	int inv_cnt = 0;

	i = l;	// index for left subarray
	j = half;	// index for right subarray
	k = l;	// index for resultant merged subarray

	while ((i <= half - 1) && (j <= r))
	{
		if (a[i] <= a[j])
		{
			tmp[k] = a[i];
			i++;
			k++;
		}
		else
		{
			tmp[k] = a[j];
			k++;
			j++;
			inv_cnt = inv_cnt + (half - i);	// merge inversion count
		}
	}

	/*Copy the remaining elements of the left
	subarray (if there are any) to temp*/
	while (i <= half - 1)
	{
		tmp[k] = a[i];
		k++;
		i++;
	}

	/*Copy the remaining elements of the right
	subarray (if there are any) to temp*/
	while (j <= r)
	{
		tmp[k] = a[j];
		k++;
		j++;
	}

	/*Copy back the merged elements to the
	original array*/
	for (i = l; i <= r; i++)
		a[i] = tmp[i];

	return inv_cnt;
}

int main()
{
	int a[] = { 7, 5, 9, 3, 4 };
	int n = sizeof(a) / sizeof(a[0]);
	int res = mergeSort(a, n);
	cout << "Inversions: " << res;
	return 0;
}
```

## Reverse Pairs
Given an integer array nums, return the number of reverse pairs in the array.

A reverse pair is a pair (i, j) where:

0 <= i < j < nums.length and
nums[i] > 2 * nums[j].

```cpp
#include <bits/stdc++.h>
using namespace std;

void merge(vector<int> &arr, int low, int mid, int high) {
    vector<int> temp; // temporary array
    int left = low;      // starting index of left half of arr
    int right = mid + 1;   // starting index of right half of arr

    //storing elements in the temporary array in a sorted manner//

    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp.push_back(arr[left]);
            left++;
        }
        else {
            temp.push_back(arr[right]);
            right++;
        }
    }

    // if elements on the left half are still left //

    while (left <= mid) {
        temp.push_back(arr[left]);
        left++;
    }

    //  if elements on the right half are still left //
    while (right <= high) {
        temp.push_back(arr[right]);
        right++;
    }

    // transfering all elements from temporary to arr //
    for (int i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }
}

int countPairs(vector<int> &arr, int low, int mid, int high) {
    int right = mid + 1;
    int cnt = 0;
    for (int i = low; i <= mid; i++) {
        while (right <= high && arr[i] > 2 * arr[right]) right++;
        cnt += (right - (mid + 1));
    }
    return cnt;
}

int mergeSort(vector<int> &arr, int low, int high) {
    int cnt = 0;
    if (low >= high) return cnt;
    int mid = (low + high) / 2 ;
    cnt += mergeSort(arr, low, mid);  // left half
    cnt += mergeSort(arr, mid + 1, high); // right half
    cnt += countPairs(arr, low, mid, high); //Modification
    merge(arr, low, mid, high);  // merging sorted halves
    return cnt;
}

int team(vector <int> & skill, int n)
{
    return mergeSort(skill, 0, n - 1);
}

int main()
{
    vector<int> a = {4, 1, 2, 3, 1};
    int n = 5;
    int cnt = team(a, n);
    cout << "The number of reverse pair is: "
         << cnt << endl;
    return 0;
}
```

## Count of Range Sum
Given an integer array nums and two integers lower and upper, return the number of range sums that lie in [lower, upper] inclusive.

Range sum S(i, j) is defined as the sum of the elements in nums between indices i and j inclusive, where i <= j.

```java
/*
    Time complexity : O(N * logN)
    Space complexity: O(N)

    where N is the size of the array

*/

int mergeSort(vector<long> &sum, int L, int R, int start, int end)
{
    // Corner case
    if (end - start <= 1)
    {
        return 0;
    }

    int mid = (start + end) / 2, m = mid, n = mid, count = 0;

    count = mergeSort(sum, L, R, start, mid) + mergeSort(sum, L, R, mid, end);

    // Count the valid ranges
    for (int i = start; i < mid; i++)
    {
        while (m < end && sum[m] - sum[i] < L)
        {
            m++;
        }

        while (n < end && sum[n] - sum[i] <= R)
        {
            n++;
        }

        count += n - m;
    } 
    
    // Merge the two sorted half and copy the sorted result back to sum
    inplace_merge(sum.begin() + start, sum.begin() + mid, sum.begin() + end);

    return count;
}

int countRangeSum(vector<int> &nums, int N, int L, int R)
{
    vector<long> sum(N + 1, 0);

    // Storing the prefix sum
    for (int i = 0; i < N; i++)
    {
        sum[i + 1] = sum[i] + nums[i];
    }

    return mergeSort(sum, L, R, 0, N + 1);
}```
