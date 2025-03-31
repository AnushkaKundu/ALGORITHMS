## Merge Intervals

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

 
Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]

Output: [[1,6],[8,10],[15,18]]

Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].


Example 2:

Input: intervals = [[1,4],[4,5]]

Output: [[1,5]]

Explanation: Intervals [1,4] and [4,5] are considered overlapping.
 

Constraints:

1 <= intervals.length <= 104

intervals[i].length == 2

0 <= starti <= endi <= 104


```
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        int n = intervals.size();
        vector<vector<int>>ans;
        sort(intervals.begin() , intervals.end());
        int start = intervals[0][0];
        int end = intervals[0][1];

        for (int i=1; i<n; i++)
        {
            if (intervals[i][0] <= end)
                end = max(end, intervals[i][1]);
            else
            {
                ans.push_back({start, end});
                start = intervals[i][0];
                end = intervals[i][1];
            }
        }
        ans.push_back({start, end});
        return ans;
    }
};
```

## Maximum CPU Load from the given list of jobs
Given an array of jobs with different time requirements, where each job consists of start time, end time and CPU load. 

The task is to find the maximum CPU load at any time if all jobs are running on the same machine.

Examples: 

Input: jobs[] = {{1, 4, 3}, {2, 5, 4}, {7, 9, 6}} 

Output: 7 

Explanation: 

In the above-given jobs, there are two jobs which overlaps. 

That is, Job [1, 4, 3] and [2, 5, 4] overlaps for the time period in [2, 4] 

Hence, the maximum CPU Load at this instant will be maximum (3 + 4 = 7).



Input: jobs[] = {{6, 7, 10}, {2, 4, 11}, {8, 12, 15}} 

Output: 15 

Explanation: 

Since, There are no jobs that overlaps. 

Maximum CPU Load will be – max(10, 11, 15) = 15

```
// C++ implementation to find the
// maximum CPU Load from the given array of jobs

#include <bits/stdc++.h>
using namespace std;

// the job struct will have s(starting time) , e(ending time) , load(cpu load)
struct Job {
	int s, e, load;
};

// endpoint struct will have val(the time associated with the endpoint),
// load(cpu load associated with the endpoint),
// a flag isStart which will tell if the endpoint is starting or ending point of
// an interval
struct Endpoint {
	int val, load;
	bool isStart;
};

// custom comparator function which is used by the c++ sort stl
bool comp(const Endpoint& a, const Endpoint& b) {
	if (a.val != b.val)
		return a.val < b.val;
	return a.isStart == true && b.isStart == false;
}
//function to find maximum cpu load
int maxCpuLoad(vector<Job> v)
{
	int count = 0; // count will contain the count of current loads
	int result = 0; // result will contain maximum of all counts

	// this data array will contain all the endpoints combined with their load values
	// and flags telling whether they are starting or ending point
	vector<Endpoint> data;

	for (int i = 0; i < v.size(); i++) {
		data.emplace_back(Endpoint{ v[i].s, v[i].load, true});
		data.emplace_back(Endpoint{ v[i].e, v[i].load, false});
	}

	sort(data.begin(), data.end(), comp);

	for (int i = 0; i < data.size(); i++) {
		if (data[i].isStart == true) {
			count += data[i].load;
			result = max(result, count);
		}
		else
			count -= data[i].load;

	}

	return result;
}
//Driver code to test maxCpuLoad function
int main() {
	vector<Job> v = {
		{6, 7, 10},
		{2, 4, 11}, 
		{8, 12, 15}
	};
	cout << maxCpuLoad(v);
	return 0;
}
// this code is contributed by Mohit Puri

```

Similar: 
Car Pooling 
https://leetcode.com/problems/car-pooling/

## [Merge Overlapping Intervals: ](https://leetcode.com/problems/non-overlapping-intervals/description/)
Minimum of intervals needed to remove to make all the intervals non overlapping. 

## [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)
There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array points where points[i] = [xstart, xend] denotes a balloon whose horizontal diameter stretches between xstart and xend. You do not know the exact y-coordinates of the balloons.


Arrows can be shot up directly vertically (in the positive y-direction) from different points along the x-axis. A balloon with xstart and xend is burst by an arrow shot at x if xstart <= x <= xend. There is no limit to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.


Given the array points, return the minimum number of arrows that must be shot to burst all balloons.

### Approach: 
Sort intervals by end time. Always burst 1st ballon. Maintain index of last arrow, which is end of 1st interval for now. run a loop to detect that if the next intervals start before index of last arrow, if yes means they are burst ignore that interval. Otherwise, burst the baloon by putting next arrow on end of that interval. And update last arrow index.

```cpp
class Solution {
public:
    static bool endSorter(vector<int>&a, vector<int>&b)
    {
        return a[1] == b[1] ? a[0] < b[0] : a[1] < b[1];
    }
    int findMinArrowShots(vector<vector<int>>& points) {
        int size = points.size();
        sort(points.begin(), points.end(), endSorter);
        int arrow = points[0][1];
        int count = 1;
        for (int i = 1; i < size; i++)
        {
            if (arrow >= points[i][0] && arrow <= points[i][1])
                continue;
            count++;
            arrow = points[i][1];
        }
        return count;
    }
};
```

