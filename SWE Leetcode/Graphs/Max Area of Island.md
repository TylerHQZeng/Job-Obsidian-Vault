## Problem statement

You are given an `m x n` binary matrix `grid`. An island is a group of `1`'s (representing land) connected **4-directionally** (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The **area** of an island is the number of cells with a value `1` in the island.

Return _the maximum **area** of an island in_ `grid`. If there is no island, return `0`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg)

**Input:** grid = `[[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]`
**Output:** 6
**Explanation:** The answer is not 11, because the island must be connected 4-directionally.

**Example 2:**

**Input:** grid = `[[0,0,0,0,0,0,0,0]]`
**Output:** 0

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 50`
- `grid[i][j]` is either `0` or `1`.
## Notes

- Very similar to num islands, but we just have a counter of the current island size and take the max over all islands
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
class Solution:

    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:

        max_island = 0

        directions = [(1,0),(-1,0),(0,1),(0,-1)]

  

        def dfs(row, col):

            grid[row][col] = 0

            size = 1

            for dr, dc in directions:

                nr, nc = row + dr, col + dc

                if 0 <= nr < len(grid) and 0 <= nc < len(grid[0]) and grid[nr][nc] == 1:

                    size += dfs(nr,nc)

  

            return size

        for row in range(len(grid)):

            for col in range(len(grid[0])):

                if grid[row][col] == 1:

                    max_island = max(max_island, dfs(row, col))

  

        return max_island
```

#medium 
#dfs 
#graphs