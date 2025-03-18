## Problem statement

In this problem, a tree is an **undirected graph** that is connected and has no cycles.

You are given a graph that started as a tree with `n` nodes labeled from `1` to `n`, with one additional edge added. The added edge has two **different** vertices chosen from `1` to `n`, and was not an edge that already existed. The graph is represented as an array `edges` of length `n` where `edges[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the graph.

Return _an edge that can be removed so that the resulting graph is a tree of_ `n` _nodes_. If there are multiple answers, return the answer that occurs last in the input.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/05/02/reduntant1-1-graph.jpg)

**Input:** edges = `[[1,2],[1,3],[2,3]]`
**Output:** `[2,3]`

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/05/02/reduntant1-2-graph.jpg)

**Input:** edges = `[[1,2],[2,3],[3,4],[1,4],[1,5]]`
**Output:** `[1,4]`

**Constraints:**

- `n == edges.length`
- `3 <= n <= 1000`
- `edges[i].length == 2`
- `1 <= ai < bi <= edges.length`
- `ai != bi`
- There are no repeated edges.
- The given graph is connected.
## Notes

- Use union find and check if two nodes that are next to each other share a parent, if they do, then there is a cycle
## Complexity

- Time: $O(n \cdot \alpha(n))$
- Space: $O(n)$
## Code

```python
class UF:

    def __init__(self, N):

        self.N = N

        self.size = [1] * N

        self.parent = list(range(N))

    def _find(self, node):

        if node == self.parent[node]:

            return node

        self.parent[node] = self._find(self.parent[node])

        return self.parent[node]

    def _union(self, n1, n2):

        n1, n2 = self._find(n1), self._find(n2)

  

        if n1 == n2:

            return False

        else:

            if self.size[n1] > self.size[n2]:

                self.parent[n2] = n1

                self.size[n1] += self.size[n2]

            else:

                self.parent[n1] = n2

                self.size[n2] += self.size[n1]

            return True

  

class Solution:

    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:

        N = len(edges)

  

        dsu = UF(N)

        for edge in edges:

            if not dsu._union(edge[0] - 1, edge[1] - 1):

                return edge

  

        return []
```

#graphs 
#unionfind
#medium