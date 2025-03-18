## Problem statement

You are given an array `nums` consisting of **positive** integers.

We call a subarray of `nums` **nice** if the bitwise **AND** of every pair of elements that are in **different** positions in the subarray is equal to `0`.

Return _the length of the **longest** nice subarray_.

A **subarray** is a **contiguous** part of an array.

**Note** that subarrays of length `1` are always considered nice.

**Example 1:**

**Input:** nums = `[1,3,8,48,10]`
**Output:** 3
**Explanation:** The longest nice subarray is `[3,8,48]`. This subarray satisfies the conditions:
- 3 AND 8 = 0.
- 3 AND 48 = 0.
- 8 AND 48 = 0.
It can be proven that no longer nice subarray can be obtained, so we return 3.

**Example 2:**

**Input:** nums = `[3,1,5,11,13]`
**Output:** 1
**Explanation:** The length of the longest nice subarray is 1. Any subarray of length 1 can be chosen.

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 109`
## Notes

- Use regular sliding window with left and right pointer
- Use XOR to get rid of any numbers on the left that doesn't keep it 0
- Use OR to add any numbers on the right 
## Complexity

- Time: $O(n)$
- Space: $O(1)$
## Code

```python
class Solution:

    def longestNiceSubarray(self, nums: List[int]) -> int:

        l = 0

        res = 0

        curr = 0

        for r in range(len(nums)):

            while (curr & nums[r]) != 0:

                curr ^= nums[l]

                l += 1

  

            curr |= nums[r]

            res = max(res, r - l + 1)

        return res
```

#medium 
#arrays 
#slidingwindow 
#bitmanipulation