## Problem statement

You are given a **0-indexed** `m x n` matrix `grid` consisting of **positive** integers.

You can start at **any** cell in the first column of the matrix, and traverse the grid in the following way:

- From a cell `(row, col)`, you can move to any of the cells: `(row - 1, col + 1)`, `(row, col + 1)` and `(row + 1, col + 1)` such that the value of the cell you move to, should be **strictly** bigger than the value of the current cell.

Return _the **maximum** number of **moves** that you can perform._

**Example 1:**

![](https://assets.leetcode.com/uploads/2023/04/11/yetgriddrawio-10.png)

**Input:** grid = `[[2,4,3,5],[5,4,9,3],[3,4,2,11],[10,9,13,15]]`
**Output:** 3
**Explanation:** We can start at the cell (0, 0) and make the following moves:
- (0, 0) -> (0, 1).
- (0, 1) -> (1, 2).
- (1, 2) -> (2, 3).
It can be shown that it is the maximum number of moves that can be made.

**Example 2:**

![](https://assets.leetcode.com/uploads/2023/04/12/yetgrid4drawio.png)
**Input:** grid = `[[3,2,4],[2,1,9],[1,1,7]]`
**Output:** 0
**Explanation:** Starting from any cell in the first column we cannot perform any moves.

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `2 <= m, n <= 1000`
- `4 <= m * n <= 105`
- `1 <= grid[i][j] <= 106`
## Notes

- Use DFS and cache the results of each cell
## Complexity

- Time: $O(m * n)$
- Space: O(m * n)$
## Code

```python
class Solution:

    def maxMoves(self, grid: List[List[int]]) -> int:

        directions = [(-1,1),(0,1),(1,1)]

        dp = {}

        res = 0

        def dfs(r, c):

            if (r, c) in dp:

                return dp[(r, c)]

            if r < 0 or r >= len(grid) or c < 0 or c >= len(grid[0]):

                return 0

  

            max_moves = 0

            for dr, dc in directions:

                nr, nc = r + dr, c + dc

                if 0 <= nr < len(grid) and 0 <= nc < len(grid[0]) and grid[nr][nc] > grid[r][c]:

                    max_moves = max(max_moves, 1 + dfs(nr, nc))

  

            dp[(r, c)] = max_moves

            return dp[(r, c)]

  
  

        for r in range(len(grid)):

            res = max(res, dfs(r, 0))

        return res
```

#graphs 
#medium 
#dfs 