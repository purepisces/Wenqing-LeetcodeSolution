## Link:
- [242-Valid-Anagram](https://leetcode.com/problems/valid-anagram/description/)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
This problem is not that difficult. It is just counting the numbers of each characters appearance. We can use hashmaps to deal with this problem, by setting keys(characters) and corresponding values(occurrence time).

# Approach
<!-- Describe your approach to solving the problem. -->
Hashmap1 for s, hashmap2 for t. Each hashmap stores key and value, key is the character, value is the occurence time. Note for not rasing key error problem, we should using temp1.get(s[i],0), which ensures if the key doesn't exist, then the value will be 0.
Finally, compare these 2 hashmaps to see if they are equal.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
$$O(n)$$
- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
$$O(1)$$
# Code
Solution 1:
```python
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        if len(s) != len(t):
            return False
        temp1 = {}
        temp2 = {}
        for i in range(len(s)):
            temp1[s[i]] = 1 + temp1.get(s[i],0)
            temp2[t[i]] = 1 + temp2.get(t[i],0)
        return temp1 == temp2   
```
Solution 2:
```python
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        if len(s) != len(t):
            return False
        count1 = [0] *26
        count2 = [0]*26
        for i in range(len(s)):
            count1[ord(s[i]) - ord("a")] +=1
            count2[ord(t[i]) - ord("a")] +=1
        return count1 == count2
```
