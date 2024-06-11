# Link:
- [347_Top_K_Frequent_Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
I watched neetcode for solution, but this problem is not that difficult.
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
Firstly, the intuition is that we need to count the frequency of each number's, then we can return for most kth frequent number. For example, in this case it will be {1: 3, 2: 2, 3: 1}.
Then neetcode come up with a really clever way, it reserved len(nums)+1 position for store the frequency and corresponding value. In this case, frequency is [[],[],[],[],[],[],[]], and fre[0] represents appear 0 time, fre[1] represents appear 1 time, freq[2] represnets appear 2 time and so on... Then we can in reverse order and find the kth most frequent element.
How to make freq store our wanted value? We can for loop {1: 3, 2: 2, 3: 1}. For ele, fre in res.items():.

    for ele, fre in res.items():
        freq[fre].append(ele)

[[],[1],[2],[3],[],[],[]]
Then after updated the freq, we could for loop it in reverse order, and append value to our final result array.

# Approach
<!-- Describe your approach to solving the problem. -->
Construct a hashtable that stores each num and their corresponding frequency values. Construct a frequency array, each index represents the appearance time, and the value stores in this index means that for value x it appears i time. The frequency array should be len(nums)+1, since the frequency could be 0 to len(nums), so the total length is len(nums) + 1. Then in reverse order, we extract the value and append it to the final result array. When the length of the result array is equal to k, we early stop the for loop.



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
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        res = {}
        freq = [[]for i in range(len(nums)+1)]
        for n in nums:
            res[n] = 1+ res.get(n,0)
        for ele, fre in res.items():
            freq[fre].append(ele)
        tmp = []
        for i in range(len(freq)-1,-1,-1):
            for item in freq[i]:
                tmp.append(item)
                if len(tmp) == k:
                    return tmp
```
# Tech

```python
res = {}
for ele, fre in res.items()
```
