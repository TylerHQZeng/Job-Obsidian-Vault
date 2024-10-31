## Problem statement

Given an `m x n` binary `matrix` filled with `0`'s and `1`'s, _find the largest square containing only_ `1`'s _and return its area_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/max1grid.jpg)

**Input:** matrix = `[["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]`
**Output:** 4

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/26/max2grid.jpg)

**Input:** matrix = `[["0","1"],["1","0"]]`
**Output:** 1

**Example 3:**

**Input:** matrix = `[["0"]]`
**Output:** 0

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 300`
- `matrix[i][j]` is `'0'` or `'1'`.
## Notes

- On every cell where there is a 1, check its left, top and topleft adjacent cells and take the minimum of all three and add 1

![[Pasted image 20241026114834.png]]
## Complexity

- Time: $O(n * m)$
- Space: $O(n * m)$
## Code

```python
class Solution:

    def maximalSquare(self, matrix: List[List[str]]) -> int:

        # iterate over each cell and check if the surrounding topleft and top cells are 1's

        # if they are 1's and the current cell is 1, we can add the areas, else just set as 0

        if matrix is None or len(matrix) < 1:

            return 0

        rows = len(matrix)

        cols = len(matrix[0])

        dp = [[0]*(cols+1) for _ in range(rows+1)]

        max_side = 0

  

        for r in range(rows):

            for c in range(cols):

                if matrix[r][c] == '1':

                    dp[r+1][c+1] = min(dp[r][c], dp[r+1][c], dp[r][c+1]) + 1

                    max_side = max(max_side, dp[r+1][c+1])

  

        return max_side * max_side
```

#medium 
#dp 
#matrix 