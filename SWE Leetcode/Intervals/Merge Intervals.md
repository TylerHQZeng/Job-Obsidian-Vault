## Problem statement

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = `[[1,3],[2,6],[8,10],[15,18]]`
**Output:** `[[1,6],[8,10],[15,18]]`
**Explanation:** Since intervals `[1,3]` and `[2,6]` overlap, merge them into `[1,6]`.

**Example 2:**

**Input:** intervals = `[[1,4],[4,5]]`
**Output:** `[[1,5]]`
**Explanation:** Intervals `[1,4]` and `[4,5]` are considered overlapping.

**Constraints:**

- `1 <= intervals.length <= 104`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 104`
## Notes

- We can sort the intervals by start time and then keep track of overlapping intervals by iterating over all intervals. When we hit an interval which does not overlap, append everything from before to result

## Complexity

- Time: $O(n\log{n})$ to sort $n$ intervals
- Space: $O(n)$ space for the sorting
## Code

```python
from typing import List

class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        if len(intervals) == 0 or len(intervals) == 1:
            return intervals
        
        sorted_list = sorted(intervals, key=lambda x: x[0])
        result = []
        
        l = 0
        r = 1
        
        while r < len(sorted_list):
            if sorted_list[l][1] >= sorted_list[r][0]:
                sorted_list[l][1] = max(sorted_list[l][1], sorted_list[r][1])
                r += 1
            else:
                result.append([sorted_list[l][0], sorted_list[l][1]])
                l = r
                r += 1
        
        result.append([sorted_list[l][0], sorted_list[l][1]])
        
        return result
```

#intervals 
#medium 
#sorting