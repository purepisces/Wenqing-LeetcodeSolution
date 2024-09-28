```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def rightSideView(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        res = []
        q = collections.deque()
        if root:
            q.append(root)
        while q:
            rightnode = None
            for i in range(len(q)):
                node = q.popleft()
                rightnode = node
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            res.append(rightnode.val)
        return res
```
