# Link:
- [42-Trapping-Rain-Water](https://leetcode.com/problems/trapping-rain-water/description/)

# Intuition

This problem can be approached by visualizing a graph, making it easier to understand and solve.

<img src="Trapping-Rain-Water.png" alt="Trapping-Rain-Water" width="400" height="300"/>


# Approach
Make two pointers, left pointer and right pointer, start position of the array and end position of the array separately. Initialize leftmax and rightmax to be the start position and end position. Then move the smallest value and update max value and final result value.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
$$O(n)$$

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
$$O(1)$$

# Code
```
class Solution(object):
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        l = 0
        r = len(height)-1
        leftmax = height[l]
        rightmax = height[r]
        res = 0
        while l < r:
            if leftmax < rightmax:
                l+=1
                leftmax = max(leftmax, height[l])
                res += leftmax - height[l]
            else:
                r-=1
                rightmax = max(rightmax, height[r])
                res += rightmax - height[r]
        return res
```
