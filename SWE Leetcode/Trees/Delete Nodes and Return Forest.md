## Problem statement

Given the `root` of a binary tree, each node in the tree has a distinct value.

After deleting all nodes with a value in `to_delete`, we are left with a forest (a disjoint union of trees).

Return the roots of the trees in the remaining forest. You may return the result in any order.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/07/01/screen-shot-2019-07-01-at-53836-pm.png)

**Input:** root = `[1,2,3,4,5,6,7]`, to_delete = `[3,5]`
**Output:** `[[1,2,null,4],[6],[7]]`

**Example 2:**

**Input:** root = `[1,2,4,null,3]`, to_delete = `[3]`
**Output:** `[[1,2,4]]`

**Constraints:**

- The number of nodes in the given tree is at most `1000`.
- Each node has a distinct value between `1` and `1000`.
- `to_delete.length <= 1000`
- `to_delete` contains distinct values between `1` and `1000`.
## Notes

- Use hashmap to enable $O(1)$ lookup to check if a node is going to be deleted
- Perform dfs on the root and append to res if it is a root and not in to be deleted
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

    def delNodes(self, root: Optional[TreeNode], to_delete: List[int]) -> List[TreeNode]:

        to_delete_set = set(to_delete)

        forest = []

  

        def dfs(node, is_root):

            if not node:

                return None

            is_deleted = node.val in to_delete_set

            if is_root and not is_deleted:

                forest.append(node)

            node.left = dfs(node.left, is_deleted)

            node.right = dfs(node.right, is_deleted)

            return None if is_deleted else node

  

        dfs(root, True)

        return forest
```

#dfs 
#hashmap 
#trees 