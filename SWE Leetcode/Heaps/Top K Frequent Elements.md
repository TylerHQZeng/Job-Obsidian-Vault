## Problem statement

Given an integer array `nums` and an integer `k`, return _the_ `k` _most frequent elements_. You may return the answer in **any order**.

**Example 1:**

**Input:** nums = `[1,1,1,2,2,3]`, k = 2
**Output:** `[1,2]`

**Example 2:**

**Input:** nums = `[1]`, k = 1
**Output:** `[1]`

**Constraints:**

- `1 <= nums.length <= 105`
- `-104 <= nums[i] <= 104`
- `k` is in the range `[1, the number of unique elements in the array]`.
- It is **guaranteed** that the answer is **unique**.

**Follow up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.
## Notes

- Use a max heap to store the frequency and pop the first k elements
- For the followup, we use Hoare's partition algorithm
## Complexity

- Time: $O(k\log{n})$
- Space: $O(n)$
## Code

```python
class Solution:

    def topKFrequent(self, nums: List[int], k: int) -> List[int]:

        m = {}

  

        for num in nums:

            m[num] = m.get(num, 0) + 1

        heap = [(-freq, num) for num, freq in m.items()]

        heapq.heapify(heap)

  

        result = [heapq.heappop(heap)[1] for _ in range(k)]

        return result
```

Followup:

```python
from collections import Counter
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = Counter(nums)
        unique = list(count.keys())
        
        def partition(left, right, pivot_index) -> int:
            pivot_frequency = count[unique[pivot_index]]
            # 1. Move the pivot to end
            unique[pivot_index], unique[right] = unique[right], unique[pivot_index]  
            
            # 2. Move all less frequent elements to the left
            store_index = left
            for i in range(left, right):
                if count[unique[i]] < pivot_frequency:
                    unique[store_index], unique[i] = unique[i], unique[store_index]
                    store_index += 1

            # 3. Move the pivot to its final place
            unique[right], unique[store_index] = unique[store_index], unique[right]  
            
            return store_index
        
        def quickselect(left, right, k_smallest) -> None:
            """
            Sort a list within left..right till kth less frequent element
            takes its place. 
            """
            # base case: the list contains only one element
            if left == right: 
                return
            
            # Select a random pivot_index
            pivot_index = random.randint(left, right)     
                            
            # Find the pivot position in a sorted list   
            pivot_index = partition(left, right, pivot_index)
            
            # If the pivot is in its final sorted position
            if k_smallest == pivot_index:
                 return 
            # go left
            elif k_smallest < pivot_index:
                quickselect(left, pivot_index - 1, k_smallest)
            # go right
            else:
                quickselect(pivot_index + 1, right, k_smallest)
         
        n = len(unique) 
        # kth top frequent element is (n - k)th less frequent.
        # Do a partial sort: from less frequent to the most frequent, till
        # (n - k)th less frequent element takes its place (n - k) in a sorted array. 
        # All elements on the left are less frequent.
        # All the elements on the right are more frequent.  
        quickselect(0, n - 1, n - k)
        # Return top k frequent elements
        return unique[n - k:]
```

#heaps 
#medium