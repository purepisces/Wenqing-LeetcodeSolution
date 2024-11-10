```python
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        dp = len(nums) * [1]
        for i in range(len(nums)-1,-1,-1):
            for j in range(i+1, len(nums)):
                if nums[i] < nums[j]:
                    dp[i] = max(dp[i], 1+ dp[j])
        return max(dp)
```
```python
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        dp = len(nums) * [1]
        for i in range(len(nums)-1,-1,-1):
            print("i is", i)
            for j in range(i+1, len(nums)):
                print(" j is", j)
                if nums[i] < nums[j]:
                    dp[i] = max(dp[i], 1+ dp[j])
        print(dp)
        return max(dp)
```
```css
('i is', 7)
('i is', 6)
(' j is', 7)
('i is', 5)
(' j is', 6)
(' j is', 7)
('i is', 4)
(' j is', 5)
(' j is', 6)
(' j is', 7)
('i is', 3)
(' j is', 4)
(' j is', 5)
(' j is', 6)
(' j is', 7)
('i is', 2)
(' j is', 3)
(' j is', 4)
(' j is', 5)
(' j is', 6)
(' j is', 7)
('i is', 1)
(' j is', 2)
(' j is', 3)
(' j is', 4)
(' j is', 5)
(' j is', 6)
(' j is', 7)
('i is', 0)
(' j is', 1)
(' j is', 2)
(' j is', 3)
(' j is', 4)
(' j is', 5)
(' j is', 6)
(' j is', 7)
[2, 2, 4, 3, 3, 2, 1, 1]
```
