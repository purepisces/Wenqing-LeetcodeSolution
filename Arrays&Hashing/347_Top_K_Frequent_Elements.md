```python
class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        freq = [[] for i in range(len(nums) + 1)]
        temp = {}
        for num in nums:
            temp[num] = 1 + temp.get(num, 0)
        for ele, fre in temp.items():
            freq[fre].append(ele)
        res = []
        for i in range(len(freq)-1, -1, -1):
            for ele in freq[i]:
                res.append(ele)
                if len(res) == k:
                    return res
```
# Link:
- [347_Top_K_Frequent_Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->

Initially, I wanted to count each number's occurrence and store it in a dictionary like `{1: 3, 2: 2, 3: 1}`, where the key is the element and the value is the frequency. But then, how to compare the values? I thought I should make `{3: 1, 2: 2, 1: 3}`, where the key is the frequency and the value is the element. However, I got stuck on how to order the key. Sorting the key would have a time complexity of $O(n \log n)$, but the question asks for a better time complexity, so we should discard this method.

I watched Neetcode for a solution, but this problem is not that difficult.
For example, given the input `nums = [1,1,1,2,2,3]` and `k = 2`, the output should be `[1,2]`.

Firstly, the intuition is that we need to count the frequency of each number, and then we can return the most frequent numbers up to the k-th most frequent. For example, in this case, it will be `{1: 3, 2: 2, 3: 1}`.

Neetcode came up with a really clever way to solve this. It reserves `len(nums) + 1` positions to store the frequency and corresponding values. In this case, the frequency array would be `[[], [], [], [], [], [], []]`, where `fre[0]` represents elements that appear 0 times, `fre[1]` represents elements that appear 1 time, `fre[2]` represents elements that appear 2 times, and so on. Then, we can iterate in reverse order to find the k-th most frequent element.

To make the frequency array store our desired values, we can loop through `{1: 3, 2: 2, 3: 1}` like this:
```python
for ele, fre in res.items():
    freq[fre].append(ele)
```
After updating the frequency array, it looks like `[[], [3], [2], [1], [], [], []]`. Then, we can loop through it in reverse order and append the values to our final result array.

# Approach
<!-- Describe your approach to solving the problem. -->

Construct a hashtable that stores each number and its corresponding frequency values. Construct a frequency array where each index represents the appearance count, and the values stored at each index represent the numbers that appear that many times. The frequency array should have a length of `len(nums) + 1`, since the frequency could range from 0 to `len(nums)`, making the total length `len(nums) + 1`. Then, in reverse order, we extract the values and append them to the final result array. When the length of the result array equals `k`, we can stop the loop early.

# Complexity
- Time complexity:
  $$O(n)$$

  - We iterate over the `nums` list once to count the frequency of each element, which takes $O(n)$ time.
  - Constructing the frequency array also takes $O(n)$ time since we populate it with the frequencies of each unique element.
  - Finally, we iterate over the frequency array to extract the top $k$ frequent elements, which again takes $O(n)$ time in the worst case.

- Space complexity:
    $$O(n)$$ 

  - We use a dictionary `temp` to store the frequency of each element, which takes $O(n)$ space where $n$ is the number of unique elements.
  - We use a list `freq` of lists to store elements by their frequency, which also takes $O(n)$ space in the worst case where all elements are unique and each list within `freq` has at most one element.
  - The result list `res` will store the top $k$ frequent elements, which in the worst case can be $O(k)$. However, since $k \leq n$, this contributes to $O(n)$ space complexity.

# Code
```python
class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        freq = [[] for i in range(len(nums) + 1)]
        temp = {}
        for num in nums:
            temp[num] = 1 + temp.get(num, 0)
        for ele, fre in temp.items():
            freq[fre].append(ele)
        res = []
        for i in range(len(freq)-1, -1, -1):
            for ele in freq[i]:
                res.append(ele)
                if len(res) == k:
                    return res
```
# Tech

```python
res = {}
for ele, fre in res.items()
```
