## Problem statement

Given the `head` of a linked list and a value `x`, partition it such that all nodes **less than** `x` come before nodes **greater than or equal** to `x`.

You should **preserve** the original relative order of the nodes in each of the two partitions.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/partition.jpg)

**Input:** head = `[1,4,3,2,5,2]`, x = 3
**Output:** `[1,2,2,4,3,5]`

**Example 2:**

**Input:** head = `[2,1]`, x = 2
**Output:** `[1,2]`

**Constraints:**

- The number of nodes in the list is in the range `[0, 200]`.
- `-100 <= Node.val <= 100`
- `-200 <= x <= 200`
## Notes

- Have 2 other linked lists which hold all values lower than x and bigger than x
## Complexity

- Time: $O(n)$
- Space: $O(n)$
## Code

```python
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:

        small, big = ListNode(-1), ListNode(-1)

        dummy1, dummy2 = ListNode(-1, small), ListNode(-1, big)

        while head:

            if head.val < x:

                small.next = head

                small = small.next

            else:

                big.next = head

                big = big.next

            head = head.next

        big.next = None

        small.next = dummy2.next.next

        return dummy1.next.next
```

#linkedlists 
#medium 