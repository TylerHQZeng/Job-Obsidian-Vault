## Problem statement

Given a binary array `nums` and an integer `k`, return _the maximum number of consecutive_ `1`_'s in the array if you can flip at most_ `k` `0`'s.

**Example 1:**

**Input:** nums = `[1,1,1,0,0,0,1,1,1,1,0]`, k = 2
**Output:** 6
**Explanation:** `[1,1,1,0,0,**1**,1,1,1,1,**1**]`
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.

**Example 2:**

**Input:** nums = `[0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1]`, k = 3
**Output:** 10
**Explanation:** `[0,0,1,1,**1**,**1**,1,1,1,**1**,1,1,0,0,0,1,1,1,1]`
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.

**Constraints:**

- `1 <= nums.length <= 105`
- `nums[i]` is either `0` or `1`.
- `0 <= k <= nums.length`
## Notes

- Sliding window where we keep track of the number of current flips, if the flips exceed k, we increment the left pointer until we are in the limit
## Complexity

- Time: $O(n)$
- Space: $O(1)$
## Code

```python
class Solution:

    def longestOnes(self, nums: List[int], k: int) -> int:

        l, r = 0, 0

        max_len = 0

        curr_flips = 0

        while r < len(nums):

            if nums[r] == 0:

                curr_flips += 1

  

            while curr_flips > k:

                if nums[l] == 0:

                    curr_flips -= 1

                l += 1

            max_len = max(max_len, r - l + 1)

            r += 1

        return max_len
```


#medium 
#slidingwindow
#arrays