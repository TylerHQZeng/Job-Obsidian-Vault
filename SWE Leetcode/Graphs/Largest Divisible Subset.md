## Problem statement

Given a set of **distinct** positive integers `nums`, return the largest subset `answer` such that every pair `(answer[i], answer[j])` of elements in this subset satisfies:

- `answer[i] % answer[j] == 0`, or
- `answer[j] % answer[i] == 0`

If there are multiple solutions, return any of them.

**Example 1:**

**Input:** nums = `[1,2,3]`
**Output:** `[1,2]`
**Explanation:** `[1,3]` is also accepted.

**Example 2:**

**Input:** nums = `[1,2,4,8]`
**Output:** `[1,2,4,8]`

**Constraints:**

- `1 <= nums.length <= 1000`
- `1 <= nums[i] <= 2 * 109`
- All the integers in `nums` are **unique**.
## Notes

- Could use DP
- I prefer setting up an adjacency list with edges being modulo == 0 between numbers
- Perform DFS on the adjacency list and keep track of longest list
## Complexity

- Time: $O(n^2)$
- Space: $O(n)$
## Code

```python
from functools import lru_cache

class Solution:

    def largestDivisibleSubset(self, nums: List[int]) -> List[int]:

        nums.sort()

        adj = {num: [] for num in nums}

        res = []

  

        for i in range(len(nums)):

            for j in range(i + 1, len(nums)):

                if nums[j] % nums[i] == 0:

                    adj[nums[i]].append(nums[j])

        @lru_cache(None)

        def longest_path(num):

            max_path = [num]

            for neighbor in adj[num]:

                next_path = list(longest_path(neighbor))  

                path = [num] + next_path

                if len(path) > len(max_path):

                    max_path = path

            return tuple(max_path)

  

        for num in nums:

            path = list(longest_path(num))

            if len(path) > len(res):

                res = path

  

        return res
```

#medium
#graphs 
#dp 
#dfs