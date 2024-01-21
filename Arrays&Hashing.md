# Data Structures: Hash Table, Hash Set, and HashMap
Hash Table and Hash Set are the data structures used to store data in the form of key-value pairs and objects respectively. Python's dict is a built-in HashMap which allows you to store key-value pairs. We can create a dictionary (serves as both Hashtable and HashMap). HashSet in Python (Using set). HashMap is generally preferred over HashTable if thread synchronization is not needed. Hashtable is synchronized, whereas HashMap is not. HashMap allows one null key and multiple null values, whereas Hashtable does not allow any null key or value.


## Hash Set
A **Hash Set** allows you to add unique values without defining a key for each value. It's used to store a collection of unique objects.

In Python, a `set` is used as a Hash Set. For example:
```python
my_set = {'apple', 'banana', 'cherry'}
```
Leetcode: 217_Contains_Duplicate

## Hash Table
A **Hash Table** is a data structure used to store data in key-value pairs. It's a collection where you define both the key and the value. You can then retrieve the value using its corresponding key. 

Key characteristics of a Hash Table:
- Does **not allow null keys or values**.
- It is **synchronized**, meaning it's thread-safe. However, this can make it generally slower than some unsynchronized data structures.


## Hashmap
HashMap is an advanced version and improvement on the Hashtable.

Key characteristics of a Hash Map:
- Does **allow one null key and multiple null values**.
- It is **non synchronized**.
Leetcode: 242_Valid_Anagram






