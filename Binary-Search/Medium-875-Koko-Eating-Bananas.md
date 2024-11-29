```python
class Solution(object):
    def minEatingSpeed(self, piles, h):
        """
        :type piles: List[int]
        :type h: int
        :rtype: int
        """
        l = 1
        r = max(piles)
        res = max(piles)
        while l <= r:
            mid = (l+r)//2
            time = 0
            for p in piles:
                time+=(p// mid)
                if p % mid != 0:
                    time +=1
            if time <= h:
                res = min(res, mid)
                r = mid -1
            else:
                l = mid+1
        return res
```
___
My wrong implementation, can't pass piles = [312884470] h = 312884469 expected output: 2 my wrong output is 1
```python
class Solution(object):
    def minEatingSpeed(self, piles, h):
        """
        :type piles: List[int]
        :type h: int
        :rtype: int
        """
        l = 1
        r = max(piles)
        while l <= r:
            mid = (l+r) // 2
            time = 0
            for pile in piles:
                if (pile % mid) != 0:
                    time+= 1
                time += pile/mid
            if time < h:
                r = mid - 1
            elif time > h:
                l = mid + 1       
            else:
                break         
        return mid
```
