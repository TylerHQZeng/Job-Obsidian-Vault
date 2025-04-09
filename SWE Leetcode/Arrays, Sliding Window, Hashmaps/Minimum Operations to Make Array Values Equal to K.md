## Problem statement

You are given an integer array `nums` and an integer `k`.

An integer `h` is called **valid** if all values in the array that are **strictly greater** than `h` are _identical_.

For example, if `nums = [10, 8, 10, 8]`, a **valid** integer is `h = 9` because all `nums[i] > 9` are equal to 10, but 5 is not a **valid** integer.

You are allowed to perform the following operation on `nums`:

- Select an integer `h` that is _valid_ for the **current** values in `nums`.
- For each index `i` where `nums[i] > h`, set `nums[i]` to `h`.

Return the **minimum** number of operations required to make every element in `nums` **equal** to `k`. If it is impossible to make all elements equal to `k`, return -1.

**Example 1:**

**Input:** nums = `[5,2,5,4,5]`, k = 2

**Output:** 2

**Explanation:**

The operations can be performed in order using valid integers 4 and then 2.

**Example 2:**

**Input:** nums = `[2,1,2]`, k = 2

**Output:** -1

**Explanation:**

It is impossible to make all the values equal to 2.

**Example 3:**

**Input:** nums = `[9,7,5,3]`, k = 1

**Output:** 4

**Explanation:**

The operations can be performed using valid integers in the order 7, 5, 3, and 1.

**Constraints:**

- `1 <= nums.length <= 100`
- `1 <= nums[i] <= 100`
- `1 <= k <= 100`
## Notes

- If the smallest element is bigger than k, then we automatically return -1
- We turn the array into a set and see how many distinct elements there are (we remove k, if k is in the set as this operation is not needed)
- After we have the set, the number of operations is the number of distinct elements, since we incrementally turn the biggest element into the second biggest element etc...
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code


```python
class Solution:

    def minOperations(self, nums: List[int], k: int) -> int:

        if min(nums) < k:

            return -1

        distinct = set(nums)

        if k in distinct:

            distinct.remove(k)

        return len(distinct)
```

#easy
#arrays 
#hashmap