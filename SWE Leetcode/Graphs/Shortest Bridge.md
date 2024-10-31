## Problem statement

You are given an `n x n` binary matrix `grid` where `1` represents land and `0` represents water.

An **island** is a 4-directionally connected group of `1`'s not connected to any other `1`'s. There are **exactly two islands** in `grid`.

You may change `0`'s to `1`'s to connect the two islands to form **one island**.

Return _the smallest number of_ `0`_'s you must flip to connect the two islands_.

**Example 1:**

**Input:** grid = `[[0,1],[1,0]]`
**Output:** 1

**Example 2:**

**Input:** grid = `[[0,1,0],[0,0,0],[0,0,1]]`
**Output:** 2

**Example 3:**

**Input:** grid = `[[1,1,1,1,1],[1,0,0,0,1],[1,0,1,0,1],[1,0,0,0,1],[1,1,1,1,1]]`
**Output:** 1

**Constraints:**

- `n == grid.length == grid[i].length`
- `2 <= n <= 100`
- `grid[i][j]` is either `0` or `1`.
- There are exactly two islands in `grid`.
## Notes

- Use DFS first to identify an island, then run BFS to find the shortest distance between the two islands
- To prevent TLE, we only do BFS on the boundary nodes
## Complexity

- Time: $O(n^{2})$
- Space: $O(n^{2})$
## Code

```python
class Solution:

    def shortestBridge(self, grid: List[List[int]]) -> int:

        visited = set()

        directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]

        def flip(idx1, idx2):

            grid[idx1][idx2] = 2

            visited.add((idx1, idx2))

            q = deque([(idx1, idx2)])

            while q:

                r, c = q.popleft()

                for dr, dc in directions:

                    nr, nc = r + dr, c + dc

                    if 0 <= nr < len(grid) and 0 <= nc < len(grid[0]):

                        if grid[nr][nc] == 1 and (nr, nc) not in visited:

                            visited.add((nr, nc))

                            grid[nr][nc] = 2

                            q.append((nr, nc))

                        elif grid[nr][nc] == 0:

                            boundary.append((r, c))

  

        boundary = []

        found = False

        for idx1 in range(len(grid)):

            if found:

                break

            for idx2 in range(len(grid[0])):

                if grid[idx1][idx2] == 1:

                    flip(idx1, idx2)

                    found = True

                    break

        q = deque([(r, c, 0) for r, c in boundary])

        visited = set(boundary)

  

        while q:

            r, c, distance = q.popleft()

            for dr, dc in directions:

                nr, nc = r + dr, c + dc

                if 0 <= nr < len(grid) and 0 <= nc < len(grid[0]) and (nr, nc) not in visited:

                    if grid[nr][nc] == 1:

                        return distance

                    visited.add((nr, nc))

                    q.append((nr, nc, distance + 1))

  

        return -1
```

#dfs 
#bfs 
#graphs 