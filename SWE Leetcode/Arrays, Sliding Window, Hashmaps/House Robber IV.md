## Problem statement

There are several consecutive houses along a street, each of which has some money inside. There is also a robber, who wants to steal money from the homes, but he **refuses to steal from adjacent homes**.

The **capability** of the robber is the maximum amount of money he steals from one house of all the houses he robbed.

You are given an integer array `nums` representing how much money is stashed in each house. More formally, the `ith` house from the left has `nums[i]` dollars.

You are also given an integer `k`, representing the **minimum** number of houses the robber will steal from. It is always possible to steal at least `k` houses.

Return _the **minimum** capability of the robber out of all the possible ways to steal at least_ `k` _houses_.

**Example 1:**

**Input:** nums = `[2,3,5,9]`, k = 2
**Output:** 5
**Explanation:** 
There are three ways to rob at least 2 houses:
- Rob the houses at indices 0 and 2. Capability is max(nums`[0]`, nums`[2]`) = 5.
- Rob the houses at indices 0 and 3. Capability is max(nums`[0]`, nums`[3]`) = 9.
- Rob the houses at indices 1 and 3. Capability is max(nums`[1]`, nums`[3]`) = 9.
Therefore, we return min(5, 9, 9) = 5.

**Example 2:**

**Input:** nums = `[2,7,9,3,1]`, k = 2
**Output:** 2
**Explanation:** There are 7 ways to rob the houses. The way which leads to minimum capability is to rob the house at index 0 and 4. Return max(nums`[0]`, nums`[4]`) = 2.

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 109`
- `1 <= k <= (nums.length + 1)/2`
## Notes

- Perform binary search on the max element
- For every iteration of binary search, we check the number of thefts we can make, if we can make more thefts than k, then that means the minimum is lower, else the minimum is higher

```
We define the search space based on the possible values for this **maximum** reward. The smallest possible value for this maximum reward is `min(nums)` (the lowest value in the house list), and the largest possible value is `max(nums)` (the highest value in the house list). This gives us a range of `[minReward, maxReward]`, where `minReward = min(nums)` or more specifically `1` and `maxReward = max(nums)`.

We use binary search to determine the **minimum possible capability** that still allows robbing at least `k` houses. At each step, we take the middle value in our range (`midReward = (minReward + maxReward) / 2`) and check whether it's possible to rob at least `k` houses while ensuring that no single robbed house has a value greater than `midReward`.

To determine whether a particular `midReward` is feasible, we use a greedy approach. We iterate through the list of house values and greedily select houses that have at most `midReward`. Since we cannot rob consecutive houses, we skip the next house each time we choose one. We keep a count of how many houses have been robbed, and if we reach at least `k` houses, it means the current `midReward` is achievable.

- If it is **possible** to rob at least `k` houses while keeping the "maximum stolen amount ≤ midReward", then we try lowering it by moving the binary search range to the left (`maxReward = midReward`).
- If it is **not possible**, it means `midReward` is too low, so we increase it by moving the search range to the right (`minReward = midReward + 1`).
```
## Complexity

- Time: $O(n\log m)$
- Space: $O(1)$
## Code

```python
class Solution:

    def minCapability(self, nums: List[int], k: int) -> int:

        # binary search from min to high

        l, r = 1, max(nums)

        while l < r:

            m = (l + r) // 2

            pt = 0

            index = 0

            while index < len(nums):

                if nums[index] <= m:

                    pt += 1

                    index += 2

                else:

                    index += 1

            if pt >= k:

                r = m

            else:

                l = m + 1

  

        return l
```

#binarysearch 
#medium 
#arrays