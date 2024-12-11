Remember to add the condition `while cur:`
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        cur = root
        while cur:
            if min(p.val,q.val) > cur.val:
                cur = cur.right
            elif max(p.val,q.val) < cur.val:
                cur = cur.left
            else:
                return cur
```
**Time Complexity:** O(h), where h is the height of the tree.
- Balanced BST: O(log⁡(n))
- Unbalanced BST: O(n)

 **Space Complexity:** O(1)

 ___
 When update, write it to root.right, root.left. It should be cur.right, cur.left.
 ```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        cur = root
        while cur: 
            if min(p.val, q.val) > cur.val:
                cur = root.right
            elif max(p.val, q.val) < cur.val:
                cur = root.left
            else:
                return cur
```
