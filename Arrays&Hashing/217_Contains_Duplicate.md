## Link:
- [217_Contains_Duplicate](https://leetcode.com/problems/contains-duplicate/description/)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
It just tests duplicate elements. So we can consider using HashSet.
Hashtable is essentially a Key-Value-Pair collection where you define the key and the value then you can find the value by using the key.
HashSet allowes you to add a value, this value is unique and you do not define the key.
Hash Table and Hash Set are the data structures used to store data in the form of key-value pairs and objects respectively. 

# Approach
<!-- Describe your approach to solving the problem. -->
Using set function in python. If encounter previous element, return True. If first encounter the element, add it. False condition needs to check over all array elements.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
$$O(n)$$ 
- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
$$O(n)$$ 
# Code
```python
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        # new = set(nums)
        # return not len(new) == len(nums)
        hashset = set()
        for n in nums:
            if n in hashset:
                return True
            hashset.add(n)
        return False     
```
