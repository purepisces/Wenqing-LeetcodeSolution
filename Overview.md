# Tree
1. In a tree problem, consider the base case where the root node doesn't exist.
2. Consider the tree's depth to see how the problem relates to its depth."


BFS Template
102. Binary Tree Level Order Traversal: 
https://leetcode.com/problems/binary-tree-level-order-traversal/description/
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
        if not root:
            return []
        q = deque()
        q.append(root)
        res = []
        while q:
            tmp = []
            for i in range(len(q)):
                node = q.popleft()
                tmp.append(node.val)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            res.append(tmp)
        return res 
```
