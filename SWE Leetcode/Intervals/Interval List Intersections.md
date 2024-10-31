## Problem statement

You are given two lists of closed intervals, `firstList` and `secondList`, where `firstList[i] = [starti, endi]` and `secondList[j] = [startj, endj]`. Each list of intervals is pairwise **disjoint** and in **sorted order**.

Return _the intersection of these two interval lists_.

A **closed interval** `[a, b]` (with `a <= b`) denotes the set of real numbers `x` with `a <= x <= b`.

The **intersection** of two closed intervals is a set of real numbers that are either empty or represented as a closed interval. For example, the intersection of `[1, 3]` and `[2, 4]` is `[2, 3]`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)

**Input:** firstList = `[[0,2],[5,10],[13,23],[24,25]]`, secondList = `[[1,5],[8,12],[15,24],[25,26]]`
**Output:** `[[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]`

**Example 2:**

**Input:** firstList = `[[1,3],[5,9]]`, secondList = []
**Output:** []

**Constraints:**

- `0 <= firstList.length, secondList.length <= 1000`
- `firstList.length + secondList.length >= 1`
- `0 <= starti < endi <= 109`
- `endi < starti+1`
- `0 <= startj < endj <= 109`
- `endj < startj+1`
## Notes

- Use a two pointer approach where we keep track of the start and end intervals and append if there is an overlap 
## Complexity

- Time: $O(n)$
- Space: $O(1)$
## Code

```python
class Solution:

    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:

        a, b = 0, 0

        res = []

  

        while a < len(firstList) and b < len(secondList):

            aStart, aEnd = firstList[a]

            bStart, bEnd = secondList[b]

  

            start = max(aStart, bStart)

            end = min(aEnd, bEnd)

  

            if aStart <= bEnd and bStart <= aEnd:

                res.append([start,end])

  

            if aEnd <= bEnd:

                a += 1

            else:

                b += 1

  

  

        return res
```

#medium 
#intervals 
#twopointer