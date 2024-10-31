## Problem statement

You are given an integer array `nums`. You want to maximize the number of points you get by performing the following operation any number of times:

- Pick any `nums[i]` and delete it to earn `nums[i]` points. Afterwards, you must delete **every** element equal to `nums[i] - 1` and **every** element equal to `nums[i] + 1`.

Return _the **maximum number of points** you can earn by applying the above operation some number of times_.

**Example 1:**

**Input:** nums = `[3,4,2]`
**Output:** 6
**Explanation:** You can perform the following operations:
- Delete 4 to earn 4 points. Consequently, 3 is also deleted. nums = `[2]`.
- Delete 2 to earn 2 points. nums = [].
You earn a total of 6 points.

**Example 2:**

**Input:** nums = `[2,2,3,3,3,4]`
**Output:** 9
**Explanation:** You can perform the following operations:
- Delete a 3 to earn 3 points. All 2's and 4's are also deleted. nums = `[3,3]`.
- Delete a 3 again to earn 3 points. nums = `[3]`.
- Delete a 3 once more to earn 3 points. nums = [].
You earn a total of 9 points.

**Constraints:**

- `1 <= nums.length <= 2 * 104`
- `1 <= nums[i] <= 104`
## Notes

- Similar to House Robber where we get to choose if we take the current index or not, if we do we skip over the next element if the next element is in the array
## Complexity

- Time: $O(n)$ where $n$ is the number of unique elements
- Space: $O(n)$ where $n$ is the number of unique elements
## Code

```python
class Solution:

    def deleteAndEarn(self, nums: List[int]) -> int:

        points = {}

        for num in nums:

            points[num] = points.get(num, 0) + num

        sorted_keys = sorted(points.keys())

        @cache

        def dfs(i):

            if i >= len(sorted_keys):

                return 0

  

            curr_key = sorted_keys[i]

            take = points[curr_key]

            if i + 1 < len(sorted_keys) and sorted_keys[i + 1] == curr_key + 1:

                take += dfs(i + 2)

            else:

                take += dfs(i + 1)

  

            skip = dfs(i + 1)

            return max(take, skip)

  

        return dfs(0)
```

#dp 
#medium