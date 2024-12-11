**We are using recursion, so first let's think of the base case.**
___
🌟🌟🌟🌟🌟 **Base Case for dfs**: I will use climbing stairs to illustrate it. At every given point, we have 2 decisions to make, either climb one or two. **When we reach 5**, it is our base case, we're gonna solve this recursively. When reach 5, **return 1**, this is when we find one way. And if this number of steps ever **exceeds five**, this is also the base case, we're going to **return 0**. https://leetcode.com/problems/climbing-stairs/description/
___
**Inorder Traversal**

In Inorder Traversal, the order of visiting nodes is:

1.  **Visit the left subtree**.
2.  **Visit the root node**.
3.  **Visit the right subtree**.

**Preorder Traversal**

In Preorder traversal, the order of visiting nodes is:

1.  **Visit the root node.**
2.  **Visit the left subtree.**
3.  **Visit the right subtree.**

**Postorder Traversal**

In Postorder traversal, the order of visiting nodes is:

1.  **Visit the left subtree.**
2.  **Visit the right subtree.**
3.  **Visit the root node.**

___
**bfs on a tree is basically level order traversal.**
___

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
___
More detail can see in [climbing stair](https://github.com/purepisces/Wenqing-LeetcodeSolution/blob/main/1-D-Dynamic-Programming/Easy-70-Climbing-Stairs.md).
```python
# inefficient solution
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        def dfs(i):
            if i >= n:
                return i == n
            return dfs(i + 1) + dfs(i + 2)
        return dfs(0)
```
Time Complexity: O($2^n$) 
Space Complexity: O(n)

> 🌟🌟🌟🌟🌟🌟🌟🌟🌟🌟 Time Complexity: When analyzing recursion, **time complexity** accounts for the **total number of calls** made to the function. In this case, the total number of recursive calls is proportional to the **total number of nodes in the recursion tree**. 
> - At each call to `dfs(i)`, the function does work in the form of making **two recursive calls**: `dfs(i + 1)` and `dfs(i + 2)`.
> -   These recursive calls are **new computations** — they explore different paths in the recursion tree and **add to the total number of operations performed**.
> -   Therefore, the total number of recursive calls is proportional to the **total number of nodes in the recursion tree**, which grows exponentially as $O(2^n)$.
> 
> Space Complexity: Each recursive call pushes the current state of the function onto the stack. The maximum depth of the recursion stack is equal to the **depth of the recursion tree**, which is O(n) in this case.
___

### Total Number of Nodes in a Full Binary Tree

The given tree has nodes doubling at each level, forming a full binary tree. The number of nodes at each level corresponds to the terms of a geometric progression:

$$1, 2, 4, 8, \dots, 2^{h-1}$$

where hhh is the height of the tree.

The total number of nodes in the tree is the sum of the geometric series:

$$S = 1 + 2 + 4 + 8 + \cdots + 2^{h-1}$$

The sum of a geometric series can be calculated using the formula:

$$S = \frac{2^h - 1}{2 - 1} = 2^h - 1$$

So, the total number of nodes in the tree is:

$$\text{Total nodes} = 2^h - 1$$

If the tree height $h = n$, the total number of nodes is:

$$\text{Total nodes} = 2^n - 1$$
___
