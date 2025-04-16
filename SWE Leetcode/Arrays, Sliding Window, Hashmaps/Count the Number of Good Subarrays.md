## Problem statement

Given an integer array `nums` and an integer `k`, return _the number of **good** subarrays of_ `nums`.

A subarray `arr` is **good** if there are **at least** `k` pairs of indices `(i, j)` such that `i < j` and `arr[i] == arr[j]`.

A **subarray** is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**

**Input:** nums = `[1,1,1,1,1]`, k = 10
**Output:** 1
**Explanation:** The only good subarray is the array nums itself.

**Example 2:**

**Input:** nums = `[3,1,4,3,2,2,4]`, k = 2
**Output:** 4
**Explanation:** There are 4 different good subarrays:
- `[3,1,4,3,2,2]` that has 2 pairs.
- `[3,1,4,3,2,2,4]` that has 3 pairs.
- `[1,4,3,2,2,4]` that has 2 pairs.
- `[4,3,2,2,4]` that has 2 pairs.

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i], k <= 109`
## Notes

- We keep track of a sliding window of the number of pairs within the subarray. If the number of pairs exceeds or equals k, then we know if we add anything to this subarray, it is still a good array (hence we add len(nums) - r to the total count)
- When the pairs exceed or equals to k, we shrink from the left until we go under k again
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
class Solution:

    def countGood(self, nums: List[int], k: int) -> int:

        count = defaultdict(int)

        total_pairs = 0

        res = 0

        l = 0

  

        for r in range(len(nums)):

            total_pairs += count[nums[r]]

            count[nums[r]] += 1

            while total_pairs >= k:

                res += len(nums) - r

                count[nums[l]] -= 1

                total_pairs -= count[nums[l]]

                l += 1

  

        return res
```

#medium 
#slidingwindow 
#arrays