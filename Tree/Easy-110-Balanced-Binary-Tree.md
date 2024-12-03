```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        def dfs(root):
            if not root:
                return [True, 0]
            left = dfs(root.left)
            right = dfs(root.right)
            depth = 1 + max(left[1],right[1])
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
            return [balanced, depth]
        return dfs(root)[0]
```

**Time Complexity**

The `isBalanced` function uses a Depth-First Search (DFS) approach, visiting each node of the tree exactly once. For each node, the computation involves:

1.  Recursive calls to check the left and right subtrees.
2.  Computation of `depth` and `balanced` at the current node, which is O(1).

Thus, the total time complexity is proportional to the number of nodes in the tree, denoted as nnn. Therefore, the **time complexity is O(n)**.


**Space Complexity**

The space complexity is determined by the maximum depth of the recursion stack, which corresponds to the height of the binary tree. Let hhh be the height of the tree:

-   In the best case (balanced tree), the height h=log⁡n.
-   In the worst case (skewed tree), the height h=n.

Additionally, the function does not use any significant extra space beyond the recursion stack (only a few variables like `left`, `right`, `depth`, and `balanced`).

Thus, the **space complexity is O(h)**, where h is the height of the tree. This can range from O(log⁡n) for a balanced tree to O(n) for a skewed tree.

-   **Time Complexity**: O(n)
-   **Space Complexity**: O(h), where hhh is the height of the tree, ranging from O(log⁡n) to O(n).
___
My accepted solution, I think is better than needcode solution, since I add an early stop.
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        def dfs(root):
            if not root:
                return [True, 0]
            left = dfs(root.left)
            right = dfs(root.right)
            depth = 1 + max(left[1],right[1])
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
            if not balanced:
                return [False, depth]
            return [balanced, depth]
        return dfs(root)[0]
```
My wrong implementation
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: bool
        """
        def dfs(root, isbalance):
            if not root:
                return [0,True]
            left = dfs(root.left)
            right = dfs(root.right)
            return [1+max(left[0],right[0]), left[1] and right[1] and abs(left[0]-right[0])<=1]
        return dfs(root,[0,True])[1]
```
