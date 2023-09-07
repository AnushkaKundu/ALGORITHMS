Find first occourance of a number:
```
int firstOccourance(vector<int>& arr, int target) {
int size = arr.size();
    int left = 0, right = size - 1;
    int result = -1; // Initialize result to -1, which will be used to track the first occurrence.

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {
            result = mid; // Update the result when we find a target element.
            right = mid - 1; // Continue searching in the left half to find the first occurrence.
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return result;
}
```

Find last occourance of a number:
```
int findLastOccurrence(const std::vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;
    int result = -1; // Initialize result to -1 (not found)

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {
            result = mid;  // Update result when we find the target
            left = mid + 1; // Continue searching in the right subarray
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return result;
}
```
