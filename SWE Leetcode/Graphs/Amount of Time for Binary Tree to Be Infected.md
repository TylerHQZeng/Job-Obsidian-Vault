## Problem statement

You are given the `root` of a binary tree with **unique** values, and an integer `start`. At minute `0`, an **infection** starts from the node with value `start`.

Each minute, a node becomes infected if:

- The node is currently uninfected.
- The node is adjacent to an infected node.

Return _the number of minutes needed for the entire tree to be infected._

**Example 1:**

![](https://assets.leetcode.com/uploads/2022/06/25/image-20220625231744-1.png)

**Input:** root = `[1,5,3,null,4,10,6,9,2]`, start = 3
**Output:** 4
**Explanation:** The following nodes are infected during:
- Minute 0: Node 3
- Minute 1: Nodes 1, 10 and 6
- Minute 2: Node 5
- Minute 3: Node 4
- Minute 4: Nodes 9 and 2
It takes 4 minutes for the whole tree to be infected so we return 4.

**Example 2:**

![](https://assets.leetcode.com/uploads/2022/06/25/image-20220625231812-2.png)

**Input:** root = [1], start = 1
**Output:** 0
**Explanation:** At minute 0, the only node in the tree is infected so we return 0.

**Constraints:**

- The number of nodes in the tree is in the range `[1, 105]`.
- `1 <= Node.val <= 105`
- Each node has a **unique** value.
- A node with a value of `start` exists in the tree.
## Notes

- Convert the tree into an undirected graph and then perform BFS on the start node
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def amountOfTime(self, root: Optional[TreeNode], start: int) -> int:

        adj = {}

        visited = set()

        def dfs(node):

            if not node:

                return

            if node.val not in adj:

                adj[node.val] = []

            if node.left:

                adj[node.val].append(node.left.val)

                adj[node.left.val] = [node.val]

                dfs(node.left)

            if node.right:

                adj[node.val].append(node.right.val)

                adj[node.right.val] = [node.val]

                dfs(node.right)

        dfs(root)

        t = -1

        q = deque([start])

  

        while q:

            for _ in range(len(q)):

                node = q.popleft()

                neighbors = adj[node]

                visited.add(node)

                for neighbor in neighbors:

                    if neighbor not in visited:

                        q.append(neighbor)

            t += 1

        return t
```

#medium 
#trees 
#graphs 
#bfs 
#dfs 
