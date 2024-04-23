## Meeting rooms I
Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

Example 1:

Input: [[0,30],[5,10],[15,20]]

Output: false

Example 2:

Input: [[7,10],[2,4]]

Output: true

```
bool Solution::canAttend(vector<vector<int> > &A) {
    sort(A.begin(), A.end());
    for (int i=1; i<N; i++) {
      if (A[i].first > A[i-1].second) {
        return 0;
      } 
    }
    return 1;
}
```

## Meeting rooms II
Given an 2D integer array A of size N x 2 denoting time intervals of different meetings.

Where:

A[i][0] = start time of the ith meeting.

A[i][1] = end time of the ith meeting.

Find the minimum number of conference rooms required so that all meetings can be done.

Note :- If a meeting ends at time t, another meeting starting at time t can use the same conference room

Problem Constraints

1 <= N <= 105

0 <= A[i][0] < A[i][1] <= 2 * 109

Input Format

The only argument given is the matrix A.

Output Format

Return the minimum number of conference rooms required so that all meetings can be done.


```
int Solution::rooms(vector<vector<int> > &A) {
    int maxinc = INT_MIN, count = 0, N = A.size();
    vector<pair<int, int>>V;
    for (auto ele : A) {
        V.push_back({ele[0], 1});
        V.push_back({ele[1], -1});
    }
    auto comp = [](pair<int, int> &a, pair<int, int> &b) {
        return a.first == b.first ? a.second < b.second : a.first < b.first;
    };
    sort(V.begin(), V.end(), comp);
    for (int i=0; i<2*N; i++) {
        if (V[i].second == 1)
            count++;
        else 
            count--;
        maxinc = max(maxinc, count);
    }
    // for (auto ele : V) {
    //     cout << ele.first << " " << ele.second << "\t";
    // }
    return maxinc;
}
```

## Meeting Rooms III

Problem: You are given an integer n. There are n rooms numbered from 0 to n - 1.

You are given a 2D integer array meetings where meetings[i] = [starti, endi] means that a meeting will be held during the half-closed time interval [starti, endi). All the values of starti are unique.

Meetings are allocated to rooms in the following manner:

Each meeting will take place in the unused room with the lowest number.

If there are no available rooms, the meeting will be delayed until a room becomes free. The delayed meeting should have the same duration as the original meeting.

When a room becomes unused, meetings that have an earlier original start time should be given the room.

Return** the number of the room that held the most meetings. If there are multiple rooms, return the room with the lowest number.**

A half-closed interval [a, b) is the interval between a and b including a and not including b.

Example 1:

Input: n = 2, meetings = [[0,10],[1,5],[2,7],[3,4]]

Output: 0

Explanation:
- At time 0, both rooms are not being used. The first meeting starts in room 0.
- At time 1, only room 1 is not being used. The second meeting starts in room 1.
- At time 2, both rooms are being used. The third meeting is delayed.
- At time 3, both rooms are being used. The fourth meeting is delayed.
- At time 5, the meeting in room 1 finishes. The third meeting starts in room 1 for the time period [5,10).
- At time 10, the meetings in both rooms finish. The fourth meeting starts in room 0 for the time period [10,11).
Both rooms 0 and 1 held 2 meetings, so we return 0. 

Example 2:

Input: n = 3, meetings = [[1,20],[2,10],[3,5],[4,9],[6,8]]

Output: 1

Explanation:
- At time 1, all three rooms are not being used. The first meeting starts in room 0.
- At time 2, rooms 1 and 2 are not being used. The second meeting starts in room 1.
- At time 3, only room 2 is not being used. The third meeting starts in room 2.
- At time 4, all three rooms are being used. The fourth meeting is delayed.
- At time 5, the meeting in room 2 finishes. The fourth meeting starts in room 2 for the time period [5,10).
- At time 6, all three rooms are being used. The fifth meeting is delayed.
- At time 10, the meetings in rooms 1 and 2 finish. The fifth meeting starts in room 1 for the time period [10,12).
Room 0 held 1 meeting while rooms 1 and 2 each held 2 meetings, so we return 1. 

Constraints:
- 1 <= n <= 100
- 1 <= meetings.length <= 105
- meetings[i].length == 2
- 0 <= starti < endi <= 5 * 105
- All the values of starti are unique.

```

```
