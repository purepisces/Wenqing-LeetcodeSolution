# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
This problem is not that difficult. Since it requires us to find 2 value that sum to the target and return their index, we can use hashmap to store key(number) and value(number's index). And we can then for loop the entire array, if target - nums[i] already inside the hashmap, we can just get the value of it and return. Else, we add a new key-value pair to the hashmap.
# Approach
<!-- Describe your approach to solving the problem. -->
Construct a hashmap and for loop the entrie array, we store the key(number) and value(number's index) to the hashmap. Each time if the target - nums[i] in the hashmap, we can just get the value and return it. If not, add new key-value pair to the hashmap.
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
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        temp = {}
        for i in range(len(nums)):
            if target-nums[i] in temp:
                return [temp[target -nums[i]], i]
            temp[nums[i]] = i
```
