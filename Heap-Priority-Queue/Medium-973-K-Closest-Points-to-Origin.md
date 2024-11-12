Such a easy problem, but pay attention to `for x, y in points:`, because I write like this `for point in points: x = point[0] y = point[1]`
```python
class Solution(object):
    def kClosest(self, points, k):
        """
        :type points: List[List[int]]
        :type k: int
        :rtype: List[List[int]]
        """
        res = []
        for x, y in points:
            dist = (x**2 + y**2)
            res.append([dist,x,y])
        heapq.heapify(res)
        tmp = []
        while k > 0:
            dist,x,y = heapq.heappop(res)
            tmp.append([x,y])
            k-=1
        return tmp
```
