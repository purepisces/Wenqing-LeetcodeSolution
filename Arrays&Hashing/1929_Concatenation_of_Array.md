# Link:
- [1929-Concatenation-of-Array](https://leetcode.com/problems/concatenation-of-array/description/)
  
# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
This problem is super easy, we just for loop twice and add all the elements in each loop, then return it.

# Approach
<!-- Describe your approach to solving the problem. -->
This problem is super easy, we just for loop twice and add all the elements in each loop, then return it.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
$$O(n)$$ 
- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
$$O(n)$$ 
# Code
```
class Solution(object):
    def getConcatenation(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        result= []
        for i in range(2):
            for n in nums:
                result.append(n)
        return result
```
