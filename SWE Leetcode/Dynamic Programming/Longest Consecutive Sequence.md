## Problem statement

Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

**Input:** nums = `[100,4,200,1,3,2]`
**Output:** 4
**Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4.

**Example 2:**

**Input:** nums = `[0,3,7,2,5,8,4,6,0,1]`
**Output:** 9

**Constraints:**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
## Notes

- My idea is that we perform dfs on all numbers in the array. We can check left and right by 1 and add the currently visited node to a set so we do not traverse over the same element twice
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
class Solution:

    def longestConsecutive(self, nums: List[int]) -> int:

        visited = set()

        all_nums = set()

        max_consec = 0        

        for num in nums:

            all_nums.add(num)

        def dfs(num):

            if num in visited:

                return 0

            if num not in all_nums:

                return 0

            visited.add(num)

            return 1 + dfs(num + 1) + dfs(num - 1)

  

        for num in nums:

            if num not in visited:

                max_consec = max(max_consec, dfs(num))

  

        return max_consec
```

#medium 
#dp
#dfs