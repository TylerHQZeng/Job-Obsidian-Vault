## Problem statement

You are given an integer array `ranks` representing the **ranks** of some mechanics. ranksi is the rank of the ith mechanic. A mechanic with a rank `r` can repair n cars in `r * n2` minutes.

You are also given an integer `cars` representing the total number of cars waiting in the garage to be repaired.

Return _the **minimum** time taken to repair all the cars._

**Note:** All the mechanics can repair the cars simultaneously.

**Example 1:**

**Input:** ranks = `[4,2,3,1]`, cars = 10
**Output:** 16
**Explanation:** 
- The first mechanic will repair two cars. The time required is 4 * 2 * 2 = 16 minutes.
- The second mechanic will repair two cars. The time required is 2 * 2 * 2 = 8 minutes.
- The third mechanic will repair two cars. The time required is 3 * 2 * 2 = 12 minutes.
- The fourth mechanic will repair four cars. The time required is 1 * 4 * 4 = 16 minutes.
It can be proved that the cars cannot be repaired in less than 16 minutes.​​​​​

**Example 2:**

**Input:** ranks = `[5,1,8]`, cars = 6
**Output:** 16
**Explanation:** 
- The first mechanic will repair one car. The time required is 5 * 1 * 1 = 5 minutes.
- The second mechanic will repair four cars. The time required is 1 * 4 * 4 = 16 minutes.
- The third mechanic will repair one car. The time required is 8 * 1 * 1 = 8 minutes.
It can be proved that the cars cannot be repaired in less than 16 minutes.​​​​​

**Constraints:**

- `1 <= ranks.length <= 105`
- `1 <= ranks[i] <= 100`
- `1 <= cars <= 106`
## Notes

- Similar to [[House Robber IV]] we want to binary search on the number of minutes and check if we can reach the midpoint and alter the bounds based on that
## Complexity

- Time: $O(n\log m)$
- Space: $O(1)$
## Code

```python
  

class Solution:

    def repairCars(self, ranks: List[int], cars: int) -> int:

        # Binary search on the number of minutes it takes

        l, r = 1, max(ranks) * cars * cars

        while l < r:

            m = (l + r) // 2

            curr = 0

  

            for rank in ranks:

                curr += int((m // rank) ** 0.5)  

  

            if curr >= cars:

                r = m  

            else:

                l = m + 1  

        return l
```

#medium 
#binarysearch
#arrays