In https://leetcode.com/problems/word-search/
```python
count = defaultdict(int, sum(map(Counter, board), Counter()))
```
___
```python
for i in range(len(freq)-1,-1,-1):
```
___
```python
points = [[1,3],[-2,2]]
for x, y in points:
    print("x is", x)
    print("y is", y)
```
```css
# printing result
x is 1
y is 3
x is -2
y is 2
```
-----------------------
```python
count = [0] * 8
count = [0 for i in range(8)]
print(count)
# [0, 0, 0, 0, 0, 0, 0, 0]
```
___

```python
for key, value in temp.items()
```
The dict.values() method in Python returns a view object that displays a list of all the values in the dictionary.

Code
```python
my_dict = {
            'name': 'Alice',
            'age': 25,
            'city': 'New York'
        }

values = my_dict.values()

print(values)
```
Output
```
['New York', 25, 'Alice']
```
The default_factory is a function that provides the default value for the dictionary. When a key that does not exist in the dictionary is accessed, the default_factory function is called to provide a default value for the key.
```
temp =  collections.defaultdict(list)
```
-----------------------

Solving Dictionary key value doesn't exist
```python
temp = {}
temp1[s[i]] = 1 + temp1.get(s[i],0)
```

-----------------------

```python
print(ord("b") - ord("a"))
```
output
```
1
```
-----------------------


Code
```python
tasks = ["A","A","A", "B","B","B"]
count = Counter(tasks)
print(count)
```
output
```
Counter({'A': 3, 'B': 3})
```
-----------------------

Code
```python
print([0]*5)
```
output
```
[0, 0, 0, 0, 0]
```
Code
```python
print([[0] for _ in range(5)])
```
output
```
[[0], [0], [0], [0], [0]]
```
Code
```python
freq = [[]for i in range(5)]
print(freq)
```
output
```
[[], [], [], [], []]
```


-----------------------
s.index('#', i) returns the index of the first occurrence of # starting from position i in the string s.
```python
s.index('#', i)
```
-----------------------

The enumerate function in Python is a built-in function that adds a counter to an iterable (such as a list) and returns it as an enumerate object. 

```python
heights = [170, 165, 180, 175]

for index, height in enumerate(heights):
    print(f"Index: {index}, Height: {height}")

```
output:
```
Index: 0, Height: 170
Index: 1, Height: 165
Index: 2, Height: 180
Index: 3, Height: 175

```

-----------------------


The statement pair = [(p, s) for p, s in zip(position, speed)] is a list comprehension in Python that creates a list of tuples by combining elements from two iterables, position and speed.

Example:
```
position = [1, 2, 3]
speed = [10, 20, 30]
```

zip(position, speed): The zip function takes two or more iterables and returns an iterator of tuples, where the i-th tuple contains the i-th element from each of the input iterables. For the given example, zip(position, speed) would produce:

- (1, 10)
- (2, 20)
- (3, 30)

```python
position = [1, 2, 3]
speed = [10, 20, 30]
pair = [(p, s) for p, s in zip(position, speed)]
```
output
```
pair = [(1, 10), (2, 20), (3, 30)]
```




-----------------------



pair.sort(reverse=True) is a Python command used to sort a list named pair in descending order.

reverse=True: This is an optional argument for the sort() method. By default, sort() arranges the list in ascending order (from smallest to largest). When you set reverse=True, it sorts the list in descending order (from largest to smallest).

```python
pair = [5, 2, 9, 1]
pair.sort(reverse=True)
print(pair)
```
output
```
[9, 5, 2, 1]
```
-----------------------

```python
countT = {}
for c in t:
    countT[c] = 1 + countT.get(c, 0)
```
same to 
```python
countT = {}
for c in t:
    if c not in countT:
        countT[c] = 1
    else:
        countT[c] += 1
```
-----------------------
The expression ",".join(res) is used in Python to concatenate a list of strings into a single string, with each element separated by a comma.
```python
res = ["apple", "banana", "cherry"]
result = ",".join(res)
print(result)
```
output
```
apple,banana,cherry
```

The expression vals = data.split(",") is used in Python to split a string into a list of substrings based on a specified delimiter, in this case, a comma.
```python
data = "apple,banana,cherry"
vals = data.split(",")
print(vals)
```
output
```
['apple', 'banana', 'cherry']
```




-----------------------
```
q = deque()
```

stands for "double-ended queue." It is a part of the collections module in Python and provides an efficient way to work with a sequence of elements that can be added or removed from both ends.

Efficient O(1) Operations: Appending and popping from both ends of a deque are O(1) operations. This is more efficient than using a list where these operations are O(n) at the front.
Flexible Data Structure: You can use it as a queue (FIFO - First In, First Out) or as a stack (LIFO - Last In, First Out).

Append Elements:

q.append(x): Adds x to the right end of the deque.
q.appendleft(x): Adds x to the left end of the deque.

Pop Elements:

q.pop(): Removes and returns the element from the right end.
q.popleft(): Removes and returns the element from the left end.

both q.append(x), q.appendleft(x), q.pop(), and q.popleft() operations on a deque are O(1) operations.


-----------------------

-   **Lists** are mutable and unhashable, so they cannot be used in sets or as dictionary keys.
-   **Tuples** are immutable and hashable, so they can be used in sets or as dictionary keys.

In [200. Number of Islands](https://leetcode.com/problems/number-of-islands/) when we make `visit = set()` and  `visit.add((r,c))`
we should not `visit.add([r,c])` since type 'list' is unhashable

In [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/), we should not make `ans[tuple(count)].append(s)` where count is a list, we should make it to`ans[tuple(count)].append(s)`, since TypeError: unhashable type: 'list'.

-----------------------

Mutable Objects: Lists in Python are mutable. When you modify a list (e.g., by appending or popping elements), these modifications affect the original list. This behavior is different from modifying immutable objects (like integers), where you would need to declare the variable as nonlocal to modify it in an inner function.

correct:
```
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        subset = []
        def dfs(i):
            if i == len(nums):
                res.append(subset[:])
                return 
            subset.append(nums[i])
            dfs(i+1) 
            subset.pop()
            dfs(i+1) 
        dfs(0)
        return res
```
incorrect: UnboundLocalError: local variable 'res' referenced before assignment

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def diameterOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        res = 0
        def dfs(root):
            if not root:
                return -1
            left = dfs(root.left)
            right = dfs(root.right)
            res = max(res, 2+left+right)
            return 1 + max(left, right)
        dfs(root)
        return res
```

-----------------------

Make the result truncate towards zero, using `int(float(b)/a)`: https://leetcode.com/problems/evaluate-reverse-polish-notation/description/
However, note that in online python compiler, i`nt(float(b)/a)` and `int(b/a)` both truncate towards zero, but in leetcode it doesn't work.
```python
result = int(float(b)/a) # Leetcode will truncate towards zero
result = int(b/a) # Leetcode will not truncate towards zero
result = 6/-132 #-0.045454545454545456
result = int(float(6)/-132) #Leetcode result = 0
result = int(6/132)  #Leetcode result = -1
```


-----------------------
count = defaultdict(int, sum(map(Counter, board), Counter())) : https://leetcode.com/problems/word-search/description/

Code:
```python
# The expression map(Counter, board) applies the Counter function from the collections module to each element (row) of the board.

# The sum function here is used to combine these Counter objects into a single Counter with combined frequencies

# defaultdict(int, sum(map(Counter, board), Counter())) converts this combined Counter into a defaultdict(int). This way, if you access a character that is not in the combined Counter, it will return 0 instead of raising a KeyError.

from collections import defaultdict, Counter

board = [
    ['A', 'B', 'C', 'E'],
    ['S', 'F', 'C', 'S'],
    ['A', 'D', 'E', 'E']
]

count = defaultdict(int, sum(map(Counter, board), Counter()))

counters = list(map(Counter, board))
for counter in counters:
    print(counter)

print(count) 
print("count['Z'] is", count['Z'])
```
Output
```
Counter({'A': 1, 'B': 1, 'C': 1, 'E': 1})
Counter({'S': 2, 'F': 1, 'C': 1})
Counter({'E': 2, 'A': 1, 'D': 1})
defaultdict(<class 'int'>, {'A': 2, 'B': 1, 'C': 2, 'E': 3, 'S': 2, 'F': 1, 'D': 1})
count['Z'] is 0
```
