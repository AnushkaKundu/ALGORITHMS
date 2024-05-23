## Inversion Count

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
