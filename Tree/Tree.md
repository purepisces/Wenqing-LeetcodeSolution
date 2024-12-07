🌟🌟🌟🌟🌟 **Base Case for dfs**: I will use climbing stairs to illustrate it. At every given point, we have 2 decisions to make, either climb one or two. **When we reach 5**, it is our base case, we're gonna solve this recursively. When reach 5, **return 1**, this is when we find one way. And if this number of steps ever **exceeds five**, this is also the base case, we're going to **return 0**. https://leetcode.com/problems/climbing-stairs/description/

102. Binary Tree Level Order Traversal: https://leetcode.com/problems/binary-tree-level-order-traversal/description/

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        res = []
        q = collections.deque()
        if root:
            q.append(root)

        while q:
            val = []
            for i in range(len(q)):
                node = q.popleft()
                val.append(node.val)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            res.append(val)
        return res
```
