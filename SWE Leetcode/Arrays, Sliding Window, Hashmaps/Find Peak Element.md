## Problem statement

A peak element is an element that is strictly greater than its neighbors.

Given a **0-indexed** integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in `O(log n)` time.

**Example 1:**

**Input:** nums = `[1,2,3,1]`
**Output:** 2
**Explanation:** 3 is a peak element and your function should return the index number 2.

**Example 2:**

**Input:** nums = `[1,2,1,3,5,6,4]`
**Output:** 5
**Explanation:** Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.

**Constraints:**

- `1 <= nums.length <= 1000`
- `-231 <= nums[i] <= 231 - 1`
- `nums[i] != nums[i + 1]` for all valid `i`.
## Notes

- We know `num[l] > num[l-1]` and `num[r] > num[r+1]`, we want to keep this property, so we check if the midpoint is bigger or smaller than midpoint + 1.
## Complexity

- Time: $O(\log{n})$
- Space: $O(1)$
## Code

```python
class Solution:

    def findPeakElement(self, nums: List[int]) -> int:

        l, r = 0 , len(nums) - 1

        if len(nums) == 1:

            return 0

        while l <= r:

            m = (l + r) // 2

            if nums[m-1] < nums[m] and nums[m+1] < nums[m]:

                return m

  

            if l + 1 < len(nums) and nums[l] > nums[l+1]:

                return l

            if r-1 > -1 and nums[r] > nums[r-1]:

                return r

            if m + 1 < len(nums) and nums[m] < nums[m+1]:

                l = m + 1

            elif m - 1 > -1:

                r = m - 1
```

#arrays
#binarysearch
#medium