## Link:
- [49-Group-Anagrams](https://leetcode.com/problems/group-anagrams/description/)
  
# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->

This problem is coding difficult. I watched neetcode for the solution. Firstly, like the problem anagrams, we need to count the appearance of each character. But for the previous problem, we just count for two words anagram, and we use two hashmaps and compare. However, the difficulty in this problem is if we make each hashmap for the word and compare if they are the same, it will be very complex. So! We can just store one key for each anagram and append the value of different words to the same key.

For the coding part, firstly note that list is an unhashable type. So, `res[count].append(s)` is not correct, we should use `res[tuple(count)].append(s)`. For this type of hashtable, we should define `res = collections.defaultdict(list)`. Then for loop each value in strs. The critical point is how we define key and value. Initially, in the anagram problem, the key is the character, and the value is the appearance rate. In this problem, the value is the group anagram. Neetcode selects a clever key value. Since we know if all the character and appearance times are the same, then they append to the same list. So now the value is the list, and the key is the same construction of character. For this, we can initially set 26 zero values in an array. For the character's order - the order of "a" - we will update the corresponding position's value by 1 and make a new array. The new array will count for each word's appearance.


# Approach
<!-- Describe your approach to solving the problem. -->
Make a hashtable to store it, the value is list of group of anagrams. The key is the array which counts each word's appearance time. For hashtable's value is list, we should write like this:

    res = collections.defaultdict(list)
Then for loop these str list, and for each str, we make a array to count each word's appearance. Then

    res[tuple(count)].append(s)

❌❌❌

If we use  

    temp[count].append(str)
    
then

    TypeError: unhashable type: 'list'
    temp[count].append(str)
    
# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
 $$O(n*m)$$ 

The time complexity is $O(n*m)$ because we iterate over each of the $n$ strings, and for each string, we count the characters which takes $O(m)$ time where $m$ is the maximum length of any string in strs.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
 $$O(n*m)$$ 

The space complexity is $O(n*m)$ because we store the count of characters (which takes $O(m)$ space for each string) for $n$ strings in the hash table.

# Code
```
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        temp = collections.defaultdict(list)
        for str in strs:
            count = [0]*26
            for c in str:
                count[ord(c)-ord('a')] +=1
            temp[count].append(str)
        return temp.values()
```

# Technical
```python
res = collections.defaultdict(list)
```
```python
count[ord(c)-ord("a")] +=1
```
