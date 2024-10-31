## Problem statement

You are given an array of points in the **X-Y** plane `points` where `points[i] = [xi, yi]`.

Return _the minimum area of a rectangle formed from these points, with sides parallel to the X and Y axes_. If there is not any such rectangle, return `0`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/08/03/rec1.JPG)

**Input:** points = `[[1,1],[1,3],[3,1],[3,3],[2,2]]`
**Output:** 4

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/08/03/rec2.JPG)

**Input:** points = `[[1,1],[1,3],[3,1],[3,3],[4,1],[4,3]]`
**Output:** 2

**Constraints:**

- `1 <= points.length <= 500`
- `points[i].length == 2`
- `0 <= xi, yi <= 4 * 104`
- All the given points are **unique**.
## Notes

- Store all points in a hashmap, check every pair of points and see if the other two corners for the rectangle is in the set
## Complexity

- Time: $O(n^{2})$
- Space: $O(n)$
## Code

```python
class Solution:

    def minAreaRect(self, points: List[List[int]]) -> int:

        s = set((x,y) for x, y in points)

        res = float("inf")

  

        for idx1 in range(len(points)):

            for idx2 in range(idx1 + 1, len(points)):

                x1, y1 = points[idx1]

                x2, y2 = points[idx2]

                if x1 != x2 and y1 != y2 and (x1, y2) in s and (x2, y1) in s:

                    res = min(res, abs(x2 - x1) * abs(y2 - y1))

  

        return 0 if res == float("inf") else res
```

#hashmap 
#medium 
#math 