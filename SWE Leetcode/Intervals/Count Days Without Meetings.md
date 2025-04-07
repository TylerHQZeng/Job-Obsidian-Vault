## Problem statement

You are given a positive integer `days` representing the total number of days an employee is available for work (starting from day 1). You are also given a 2D array `meetings` of size `n` where, `meetings[i] = [start_i, end_i]` represents the starting and ending days of meeting `i` (inclusive).

Return the count of days when the employee is available for work but no meetings are scheduled.

**Note:** The meetings may overlap.

**Example 1:**

**Input:** days = 10, meetings = `[[5,7],[1,3],[9,10]]`

**Output:** 2

**Explanation:**

There is no meeting scheduled on the 4th and 8th days.

**Example 2:**

**Input:** days = 5, meetings = `[[2,4],[1,3]]`

**Output:** 1

**Explanation:**

There is no meeting scheduled on the 5th day.

**Example 3:**

**Input:** days = 6, meetings = `[[1,6]]`

**Output:** 0

**Explanation:**

Meetings are scheduled for all working days.

**Constraints:**

- `1 <= days <= 109`
- `1 <= meetings.length <= 105`
- `meetings[i].length == 2`
- `1 <= meetings[i][0] <= meetings[i][1] <= days`
## Notes

- Merge all overlapping intervals and then count the gap in between and the beginning and the end
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
class Solution:

    def countDays(self, days: int, meetings: List[List[int]]) -> int:

        meetings.sort()

        res = 0

  

        def merge(sorted_list):

            l = 0

            r = 1

            result = []

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

        merged_interval = merge(meetings)

  

        for i in range(len(merged_interval) - 1):

            curr_int, next_int = merged_interval[i], merged_interval[i + 1]

            res += next_int[0] - curr_int[1] - 1

        if merged_interval[0][0] > 1:

            res += merged_interval[0][0] - 1

  

        if merged_interval[-1][1] < days:

            res += days - merged_interval[-1][1]

  

        return res
```

#medium 
#intervals 
#sorting 
#arrays