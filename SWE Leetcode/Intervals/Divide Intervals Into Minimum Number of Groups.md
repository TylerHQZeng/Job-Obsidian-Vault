## Problem statement

You are given a 2D integer array `intervals` where `intervals[i] = [lefti, righti]` represents the **inclusive** interval `[lefti, righti]`.

You have to divide the intervals into one or more **groups** such that each interval is in **exactly** one group, and no two intervals that are in the same group **intersect** each other.

Return _the **minimum** number of groups you need to make_.

Two intervals **intersect** if there is at least one common number between them. For example, the intervals `[1, 5]` and `[5, 8]` intersect.

**Example 1:**

**Input:** intervals = `[[5,10],[6,8],[1,5],[2,3],[1,10]]`
**Output:** 3
**Explanation:** We can divide the intervals into the following groups:
- Group 1: `[1, 5], [6, 8]`
- Group 2: `[2, 3], [5, 10]`
- Group 3: `[1, 10]`
It can be proven that it is not possible to divide the intervals into fewer than 3 groups.

**Example 2:**

**Input:** intervals = `[[1,3],[5,6],[8,10],[11,13]]`
**Output:** 1
**Explanation:** None of the intervals overlap, so we can put all of them in one group.

**Constraints:**

- `1 <= intervals.length <= 105`
- `intervals[i].length == 2`
- `1 <= lefti <= righti <= 106`

## Notes

- Notice that the minimum number of groups that we need is the maximum number of overlapping intervals at a certain time period
- We can keep track of this by using a line sweep algorithm
	- Whenever we enter an interval, increment counter by 1
	- Whenever we leave an interval, decrement counter by 1

## Complexity

- Time: $O(N + K)$ where $N$ is the number of intervals and $K$ is the range between start and end
- Space: $O(K$)

## Code

```python
class Solution:
    def minGroups(self, intervals: List[List[int]]) -> int:
        # Find the minimum and maximum value in the intervals
        range_start = float("inf")
        range_end = float("-inf")
        for interval in intervals:
            range_start = min(range_start, interval[0])
            range_end = max(range_end, interval[1])

        # Initialize the list with all zeroes
        point_to_count = [0] * (range_end + 2)
        for interval in intervals:
            point_to_count[
                interval[0]
            ] += 1  # Increment at the start of the interval
            point_to_count[
                interval[1] + 1
            ] -= 1  # Decrement right after the end of the interval

        concurrent_intervals = 0
        max_concurrent_intervals = 0
        for i in range(range_start, range_end + 1):
            # Update currently active intervals
            concurrent_intervals += point_to_count[i]
            max_concurrent_intervals = max(
                max_concurrent_intervals, concurrent_intervals
            )

        return max_concurrent_intervals
```

#intervals
#linesweep
#medium