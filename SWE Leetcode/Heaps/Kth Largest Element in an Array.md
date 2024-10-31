## Problem statement

Given an integer array `nums` and an integer `k`, return _the_ `kth` _largest element in the array_.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Can you solve it without sorting?

**Example 1:**

**Input:** nums = `[3,2,1,5,6,4]`, k = 2
**Output:** 5

**Example 2:**

**Input:** nums = `[3,2,3,1,2,4,5,5,6]`, k = 4
**Output:** 4

**Constraints:**

- `1 <= k <= nums.length <= 105`
- `-104 <= nums[i] <= 104`
## Notes

- Use a max heap and then pop k elements off
## Complexity

- Time: $O(k\log{n})$ heap pop takes $\log{n}$ time and we must pop $k$ times
- Space: $O(n)$
## Code

```python
class Solution:

    def findKthLargest(self, nums: List[int], k: int) -> int:

        heapq._heapify_max(nums)

  

        while k > 1:

            heapq._heappop_max(nums)

            k -= 1

  

        return heapq._heappop_max(nums)
```

#heaps
#medium