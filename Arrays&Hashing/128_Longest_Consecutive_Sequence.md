```python
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        numset = set(nums)
        longest = 0
        for n in nums:
            # calculate just from the starting position
            if n-1 not in numset:
                length = 1
                while n + length in numset:
                    length+=1
                longest = max(longest, length)
        return longest
```

# Link:
- [128_Longest_Consecutive_Sequence](https://leetcode.com/problems/longest-consecutive-sequence/description/)

# Intuition

- **Input:** `nums = [100, 4, 200, 1, 3, 2]`
- **Output:** `4`
- **Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is `4`.

Initially, we need to find the starting position of each increasing sequence and discard repeated values. So first, convert `nums` to a set using `set(nums)`. Each value in the set could either be the start position or just part of the sequence. We only need to find the starting values.

Consider the list `[1, 2, 3, 4, 5, 6]`. Without finding only the starting points, it would calculate sequences starting from `1-6`, `2-6`, `3-6`, and so on, leading to $(O(n^2)$ complexity. To ensure linear time complexity, we need to identify only the starting points in each interval.

When encountering a value, if `n-1` is in the set, skip it since it is not the starting position. If `n-1` is not in the set, it means `n` is a start value, and we initialize the length to `1`. While `n + length` is in the set, increase `length` by `1`. Then, update the result to be the maximum of `length` and the current result.

## Approach

We will find each starting position and use a hashset to store all the values of `nums`. When we find a starting position, we will calculate the sequence's length from this position. Then, we update the final result and return it.

To find the starting position:
- If `n-1` is not in `numset`, then `n` is a starting position.
- Initialize the length to be `1`.
- While `n + length` is in `numset`, we increase the length.
- Finally, update the result with the longest length found.
  
# Complexity
- Time complexity:
  $$O(n)$$
  - Creating the set: $O(n)$
  - Iterating over the list: $O(n)$
  - Checking for sequence starts and calculating lengths: $O(n)$
    
- Space complexity:
  $$O(n)$$
  - Space for the set: $O(n)$
  - Space for other variables: $O(1)$

# Code
```python
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        numset = set(nums)
        longest = 0
        for n in nums:
            # calculate just from the starting position
            if n-1 not in numset:
                length = 1
                while n + length in numset:
                    length+=1
                longest = max(longest, length)
        return longest
```
___
my not good version, very slow but accept:
```python
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        tmp = set()
        res = 0
        for num in nums:
            tmp.add(num)
        for num in nums:
            if num -1 not in tmp:
                length = 1
                while (num + 1) in tmp:
                    length+=1
                    num+=1
                res = max(res, length)
        return res
```
