For the example 

Input: tasks = ["A","A","A","B","B","B"], n = 2

Output: 8

Explanation: A possible sequence is: A -> B -> idle -> A -> B -> idle -> A -> B.

When time = 3, maxHeap = [], q = deque([[-2, 3], [-2, 4]]) since time 3 is idle time, so maxHeap is empty, it means we don't have item to choose. And the next time we can choose is for time = 4, and we add it back to maxheap. However, when time = 4, maxHeap = [-2], which means we have item to choose. 
```python
class Solution(object):
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        """
        count = Counter(tasks)
        maxHeap = [-cnt for cnt in count.values()]
        heapq.heapify(maxHeap)

        time = 0
        q = deque()  # pairs of [-cnt, idleTime]
        while maxHeap or q:
            time += 1
            if not maxHeap:
                time = q[0][1]
            else:
                cnt = 1 + heapq.heappop(maxHeap)
                if cnt:
                    q.append([cnt, time + n])
            if q and q[0][1] == time:
                heapq.heappush(maxHeap, q.popleft()[0])
        return time
```


```python
class Solution(object):
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        """
        count = Counter(tasks)
        maxHeap = [-cnt for cnt in count.values()]
        heapq.heapify(maxHeap)

        time = 0
        q = deque()  # pairs of [-cnt, idleTime]
        print(maxHeap)
        while maxHeap or q:
            time += 1
            print("####")
            print("time",time)
            print("maxHeap", maxHeap)
            print("q", q)
            if not maxHeap:
                time = q[0][1]
            else:
                cnt = 1 + heapq.heappop(maxHeap)
                if cnt:
                    q.append([cnt, time + n])
                    print(q)
            if q and q[0][1] == time:
                heapq.heappush(maxHeap, q.popleft()[0])
        return time
```
```python
[-3, -3]
####
('time', 1)
('maxHeap', [-3, -3])
('q', deque([]))
deque([[-2, 3]])
####
('time', 2)
('maxHeap', [-3])
('q', deque([[-2, 3]]))
deque([[-2, 3], [-2, 4]])
####
('time', 3)
('maxHeap', [])
('q', deque([[-2, 3], [-2, 4]]))
####
('time', 4)
('maxHeap', [-2])
('q', deque([[-2, 4]]))
deque([[-2, 4], [-1, 6]])
####
('time', 5)
('maxHeap', [-2])
('q', deque([[-1, 6]]))
deque([[-1, 6], [-1, 7]])
####
('time', 6)
('maxHeap', [])
('q', deque([[-1, 6], [-1, 7]]))
####
('time', 7)
('maxHeap', [-1])
('q', deque([[-1, 7]]))
####
('time', 8)
('maxHeap', [-1])
('q', deque([]))
```
