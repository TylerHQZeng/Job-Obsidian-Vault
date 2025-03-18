## Problem statement

You are given a **0-indexed** 2D matrix `grid` of size `m x n`, where `(r, c)` represents:

- A **land** cell if `grid[r][c] = 0`, or
- A **water** cell containing `grid[r][c]` fish, if `grid[r][c] > 0`.

A fisher can start at any **water** cell `(r, c)` and can do the following operations any number of times:

- Catch all the fish at cell `(r, c)`, or
- Move to any adjacent **water** cell.

Return _the **maximum** number of fish the fisher can catch if he chooses his starting cell optimally, or_ `0` if no water cell exists.

An **adjacent** cell of the cell `(r, c)`, is one of the cells `(r, c + 1)`, `(r, c - 1)`, `(r + 1, c)` or `(r - 1, c)` if it exists.

**Example 1:**

![](https://assets.leetcode.com/uploads/2023/03/29/example.png)

**Input:** grid = `[[0,2,1,0],[4,0,0,3],[1,0,0,4],[0,3,2,0]]`
**Output:** 7
**Explanation:** The fisher can start at cell `(1,3)` and collect 3 fish, then move to cell `(2,3)` and collect 4 fish.

**Example 2:**

![](https://assets.leetcode.com/uploads/2023/03/29/example2.png)

**Input:** grid = `[[1,0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,1]]`
**Output:** 1
**Explanation:** The fisher can start at cells (0,0) or (3,3) and collect a single fish. 

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 10`
- `0 <= grid[i][j] <= 10`
## Notes

- DFS
## Complexity

- Time: $O(m + n)$
- Space: $O(m * n)$
## Code

```python
class Solution:

  

    def dfs(self, grid, x, y):

        directions = [(1,0),(-1,0),(0,1),(0,-1)]

        res = grid[x][y]

        grid[x][y] = -1    

        for dr, dc in directions:

            nr, nc = x + dr, y + dc

            if nr > -1 and nr < len(grid) and nc > -1 and nc < len(grid[0]) and grid[nr][nc] > 0:

                res += self.dfs(grid, nr, nc)

        return res

  

    def findMaxFish(self, grid: List[List[int]]) -> int:

        res = 0

  

        for r in range(len(grid)):

            for c in range(len(grid[0])):

                if grid[r][c] > 0:

                    res = max(res, self.dfs(grid, r, c))

  

        return res
```

#dfs 
#graphs 
#medium