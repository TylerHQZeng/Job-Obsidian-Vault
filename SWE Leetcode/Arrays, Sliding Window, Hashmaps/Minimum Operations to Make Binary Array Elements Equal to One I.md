## Problem statement

You are given a binary array `nums`.

You can do the following operation on the array **any** number of times (possibly zero):

- Choose **any** 3 **consecutive** elements from the array and **flip** **all** of them.

**Flipping** an element means changing its value from 0 to 1, and from 1 to 0.

Return the **minimum** number of operations required to make all elements in `nums` equal to 1. If it is impossible, return -1.

**Example 1:**

**Input:** nums = `[0,1,1,1,0,0]`

**Output:** 3

**Explanation:**  
We can do the following operations:

- Choose the elements at indices 0, 1 and 2. The resulting array is `nums = [**1**,**0**,**0**,1,0,0]`.
- Choose the elements at indices 1, 2 and 3. The resulting array is `nums = [1,**1**,**1**,**0**,0,0]`.
- Choose the elements at indices 3, 4 and 5. The resulting array is `nums = [1,1,1,**1**,**1**,**1**]`.

**Example 2:**

**Input:** nums = `[0,1,1,1]`

**Output:** -1

**Explanation:**  
It is impossible to make all elements equal to 1.

**Constraints:**

- `3 <= nums.length <= 105`
- `0 <= nums[i] <= 1`
## Notes

From Leetcode editorial:
```
### Approach 3: Bit Manipulation & Greedy

#### Intuition

Instead of checking the last element of a triplet (`nums[i-2]`), here we directly iterate through the array from left to right and flip any `0` we encounter at `nums[i]`. Additionally, flipping `nums[i]` also forces us to flip the next two elements, `nums[i + 1]` and `nums[i + 2]`. This ensures that the `0` at `nums[i]` is turned into `1` while maintaining correctness for future elements.

To achieve this, whenever we find a `0` at `nums[i]`, we perform the following operation and increase the count of operations:

- Flip `nums[i]` (turning it into `1`).
- Flip `nums[i + 1]` and `nums[i+2]`.

Since we are scanning left to right, we only modify elements that are still `0` at the moment they are encountered.

Now let's prove the greedy approach via the method of induction.

#### Proof By Induction:

**Base Cases**:

We consider the smallest possible cases explicitly, as these provide the foundation for our inductive proof:

1. n = 3 (e.g., `[0, 0, 0]` → flip once to get `[1, 1, 1]`)
2. n = 4 (e.g., `[0, 0, 0, 0]` → flip first three to `[1, 1, 1, 0]`, then flip last three to `[1, 1, 1, 1]`)
3. n = 5 (e.g., `[0, 0, 0, 0, 0]` → similar steps, flipping strategically in two operations)

We explicitly check all possible cases for `n = 3, 4, 5` and verify that our algorithm produces the minimum number of flips in all cases. These serve as our base cases.

We require three base cases because our induction step will rely on the fact that when `n ≥ 6`, we must have `n - 3 ≥ 3`. This ensures that our inductive reasoning applies properly.

**Inductive Hypothesis**:  
Assume that for some `nums` of size `k - 3`, our algorithm performs the minimum number of operations optimally. That is, we have already shown that for any valid `nums` of size `k - 3`, our approach leads to the fewest possible flips.

Since we have proved this holds for `k - 3 ∈ {3,4,5}`, we assume it also holds for any general `k - 3`.

**Inductive Step**:  
We now extend our proof to an array of size `k`.

Our algorithm flips elements greedily from left to right, ensuring that `nums[0:k - 3]` has been fully processed optimally. From our assumed correctness for `k - 3`, we know that all values in `nums[0:k - 3]` are `1`, except possibly `nums[k - 5]` and `nums[k - 4]`, since `k - 3 > 3` ensures these exist.

Now, we consider the last three elements `nums[k - 5:k]`. We enumerate all possible cases for their values and verify that our greedy strategy of flipping when encountering `0` remains the most optimal approach.

A key assumption is that if we perform any operation at an index `< k - 5`, it would change already correct elements in `nums[0:k - 5]`. Since we have already shown that our solution for `nums[0:k - 3]` is optimal, such an operation would be redundant or suboptimal.

Therefore, the only way to minimize operations is to follow the same strategy as before i.e., handling `nums[k - 5:k]` optimally using our greedy approach.

Since the algorithm maintains optimality at every step and does not perform unnecessary operations, the hypothesis extends to size `k`.

**Conclusion**:  
Since our base cases hold for `n = 3, 4, 5`, and we have shown that assuming correctness for `k - 3` leads to correctness for `k`, we conclude by mathematical induction that our greedy approach is optimal for all `n ≥ 3`.

#### Algorithm

- Initialize `n` as the size of `nums`.
    
- Initialize `count` to track the number of flip operations.
    
- Iterate through `nums` up to `n - 3`:
    
    - If `nums[i]` is `0`, perform a triplet flip starting at `i`:
        - Flip `nums[i]` to `1`.
        - Flip `nums[i + 1]` (toggle `0` to `1` or `1` to `0`).
        - Flip `nums[i + 2]` (toggle `0` to `1` or `1` to `0`).
        - Increment `count` as a flip operation was performed.
- If `nums[n - 2]` or `nums[n - 1]` is still `0`, return `-1` since making all elements `1` is impossible.
    
- Otherwise, return `count` as the minimum number of operations needed.
```
## Complexity

- Time: $O(n)$
- Space: $O(1)$
## Code

```python
class Solution:

    def minOperations(self, nums: List[int]) -> int:

        res = 0

        # 6

        for i in range(len(nums) - 2):

            if nums[i] == 0:

                nums[i], nums[i+1], nums[i+2] = 1, 1 - nums[i+1], 1 - nums[i+2]

                res += 1

  

        if nums[-1] == 0 or nums[-2] == 0:

            return -1

        return res
```

#medium 
#arrays 
#bitmanipulation 
#slidingwindow
#math