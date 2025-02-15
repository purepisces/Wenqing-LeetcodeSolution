For example if 
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.

Then premap will contain {0: [], 1: [0]}, since we need take 0 to finish 1.

dfs(c) is for checking if this course we can finish.


```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        # dfs
        preMap = {i: [] for i in range(numCourses)}

        # map each course to : prereq list
        for crs, pre in prerequisites:
            preMap[crs].append(pre)

        visiting = set()

        def dfs(crs):
            if crs in visiting:
                return False
            if preMap[crs] == []:
                return True

            visiting.add(crs)
            for pre in preMap[crs]:
                if not dfs(pre):
                    return False
            visiting.remove(crs)
            preMap[crs] = []
            return True

        for c in range(numCourses):
            if not dfs(c):
                return False
        return True
```
___
wrong implementation
```python
# wrong implementation
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        preMap = {i: [] for i in range(numCourses)}
        for crs, pre in prerequisites:
            preMap[crs].append(pre)
        visit = set()
        def dfs(c):
            if c in visit:
                return False
            visit.add(c)
            for pre in preMap[c]:
                if not dfs(pre):
                    return False
            visit.remove(c)
            return True
        for c in range(numCourses):
            if not dfs(c):
                return False
        return True
```
