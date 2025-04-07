## Problem statement

Given an integer array `nums`, return `true` _if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or_ `false` _otherwise_.

**Example 1:**

**Input:** nums = `[1,5,11,5]`
**Output:** true
**Explanation:** The array can be partitioned as `[1, 5, 5]` and `[11]`.

**Example 2:**

**Input:** nums = `[1,2,3,5]`
**Output:** false
**Explanation:** The array cannot be partitioned into equal sum subsets.

**Constraints:**

- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 100`
## Notes

```
a + b = sum => a = sum - b
a - b = 0 => sum - b - b = 0 => 2b = sum => b = sum/2
Therefore if sum is odd then we immediately return false
Each subset must equal to half the total sum
```
## Complexity

- Time: $O(2^{n})$ optimized with cache
- Space: $O(n^2)$
## Code

```python
class Solution:

    def canPartition(self, nums: List[int]) -> bool:

        target = 0

        for num in nums:

            target += num

        if target % 2 == 1:

            return False

        target = target // 2

  

        @lru_cache(None)

        def dp(a, b, i):

            if i >= len(nums):

                return a == b  

            if a > target or b > target:

                return False

            return dp(a + nums[i], b, i + 1) or dp(a, b + nums[i], i + 1)

  
  

        return dp(0, 0, 0)
```

#medium 
#dp 
