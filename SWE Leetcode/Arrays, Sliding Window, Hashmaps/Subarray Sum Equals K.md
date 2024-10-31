## Problem statement

Given an array of integers `nums` and an integer `k`, return _the total number of subarrays whose sum equals to_ `k`.

A subarray is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**

**Input:** nums = `[1,1,1]`, k = 2
**Output:** 2

**Example 2:**

**Input:** nums = `[1,2,3`], k = 3
**Output:** 2

**Constraints:**

- `1 <= nums.length <= 2 * 104`
- `-1000 <= nums[i] <= 1000`
- `-107 <= k <= 107`
## Notes

- My initial thoughts is that we can a dfs/dp approach on the array where we either choose to continue the subarray or start a new one. We memoize each index where the value is the number of subarrays that start at that index which hits the target. 
- Compute prefix sum of the array, store it in a hashmap and check if prefix - target is already been computed before (very similar to two sum)
## Complexity

- Time: $O(n)$
- Space: $O(n)$

## Code

```python
class Solution:

    def subarraySum(self, nums: List[int], k: int) -> int:

        # Dictionary to store the count of prefix sums

        prefix_count = {0: 1}

        prefix = 0

        count = 0

  

        for num in nums:

            # Update the prefix sum

            prefix += num

            # Calculate the target prefix sum needed to form a subarray summing to k

            target = prefix - k

            # If target is in the dictionary, it means there are subarrays that sum to k

            if target in prefix_count:

                count += prefix_count[target]

            # Update the count of the current prefix sum in the dictionary

            prefix_count[prefix] = prefix_count.get(prefix, 0) + 1

  

        return count
```

#prefixsum
#hashmap 
#medium 