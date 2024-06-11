## Link:
- [49-Group-Anagrams](https://leetcode.com/problems/group-anagrams/description/)
  
# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
This problem is coding difficult. I watched neetcode for the solution. Firstly, like the problem anagrams, we need to count the appearance of each character. But for the previous problem, we just count for 2 words anagram, and we use 2 hashmap and compare. However, the difficult in this problem is if we make each hashmap for the word and compare if they are the same it will be very complex. So! We can just store one key for each anagram, and append value of different words to the same key. 
For the coding part, firstly note that list is unhashable type. So res[count].append(s) is not correct, we should use res[tuple(count)].append(s). For this type of hashtable, we should define  res = collections.defaultdict(list). Then for loop each value in strs. The critic point is how we define key and value, initially in anagram problem, key is character, value is appearance rate. In this problem, value is group anagram. And neetcode select a clever key value. Since we know if all the character and appearance time be same, then they append to the same list. So now value is the list, key is the smae construction of character. For this, we can initially set 26 zero values in a array. For the character's order - order of "a" , we will update the corresponding position's value by 1 and make a new array. The new array will count for each word's appearance.

# Approach
<!-- Describe your approach to solving the problem. -->
Make a hashtable to store it, the value is list of group of anagrams. The key is the array which counts each word's appearance time. For hashtable's value is list, we should write like this:

    res = collections.defaultdict(list)
Then for loop these str list, and for each str, we make a array to count each word's appearance. Then

    res[tuple(count)].append(s)


# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
 $$O(n*m)$$ 

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
 $$O(n*m)$$ 
# Code
```
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        res = collections.defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c)-ord("a")] +=1
            res[tuple(count)].append(s)
        return res.values()
```

# Technical
```python
res = collections.defaultdict(list)
```
```python
count[ord(c)-ord("a")] +=1
```
