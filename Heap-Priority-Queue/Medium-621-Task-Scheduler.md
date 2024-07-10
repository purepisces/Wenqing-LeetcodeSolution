In each time, the lenghth of maxheap should represent the number of tasks it can choose, and each element of maxheap represents how many numbers it left for this certain tasks. From the stdout, you can see when time = 1, maxheap = [-3,-3], it means we have 2 tasks we can choose, and each one has 3.

When time = 4 it is [], since it is idle time. And when time = 5, it is [-2], since we can just choose one task, and it has 2 left.

Example
```
Task = ["A","A","A", "B","B","B"]
n = 3
Explanation: A possible sequence is: A -> B -> idle -> idle -> A -> B -> idle -> idle -> A -> B.
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
        q = deque()  
        while maxHeap or q:
            print("1 is", maxHeap)
            time += 1
            if not maxHeap:
                time = q[0][1]
            else:
                cnt = 1 + heapq.heappop(maxHeap)
                if cnt:
                    q.append([cnt, time + n])
            print("2 is time",time)
            print("3 is q", q)
            if q and q[0][1] == time:
                heapq.heappush(maxHeap, q.popleft()[0])
        print(count)
        return time
```
output
```
('1 is', [-3, -3])
('2 is time', 1)
('3 is q', deque([[-2, 4]]))
('1 is', [-3])
('2 is time', 2)
('3 is q', deque([[-2, 4], [-2, 5]]))
('1 is', [])
('2 is time', 4)
('3 is q', deque([[-2, 4], [-2, 5]]))
('1 is', [-2])
('2 is time', 5)
('3 is q', deque([[-2, 5], [-1, 8]]))
('1 is', [-2])
('2 is time', 6)
('3 is q', deque([[-1, 8], [-1, 9]]))
('1 is', [])
('2 is time', 8)
('3 is q', deque([[-1, 8], [-1, 9]]))
('1 is', [-1])
('2 is time', 9)
('3 is q', deque([[-1, 9]]))
('1 is', [-1])
('2 is time', 10)
('3 is q', deque([]))
```






















        
