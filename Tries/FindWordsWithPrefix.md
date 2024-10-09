This is a question I wrote for myself, not exist in leetcode.

```python
class Trienode(object):
    def __init__(self):
        self.children = {}
        self.endofword = False

class Trie(object):

    def __init__(self):
        self.root = Trienode()
        
    def insert(self, word):
        """
        :type word: str
        :rtype: None
        """
        cur = self.root
        for c in word:
            if c not in cur.children:
                cur.children[c] = Trienode()
            cur = cur.children[c]
        cur.endofword = True

    def search(self, word):
        """
        :type word: str
        :rtype: bool
        """
        cur = self.root
        for c in word:
            if c not in cur.children:
                return False
            cur = cur.children[c]
        return cur.endofword

    def startsWith(self, prefix):
        """
        :type prefix: str
        :rtype: bool
        """
        cur = self.root
        for c in prefix:
            if c not in cur.children:
                return False
            cur = cur.children[c]
        return True
    
    def _collectAllWords(self, node, prefix):
        """
        Helper function to recursively collect all words starting from the given node.
        :type node: Trienode
        :type prefix: str
        :rtype: List[str]
        """
        words = []
        if node.endofword:
            words.append(prefix)  # Add the word formed by prefix
        
        for char, child in node.children.items():
            words.extend(self._collectAllWords(child, prefix + char))  # Recursively collect all child words
        
        return words
    
    def findWordsWithPrefix(self, prefix):
        """
        Return all words in the Trie that start with the given prefix.
        :type prefix: str
        :rtype: List[str]
        """
        cur = self.root
        for c in prefix:
            if c not in cur.children:
                return []  # No words with the given prefix
            cur = cur.children[c]
        
        # From here, collect all words starting with the prefix
        return self._collectAllWords(cur, prefix)


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert("apple")
# obj.insert("app")
# obj.insert("apply")
# print(obj.findWordsWithPrefix("app"))  # Should return ['app', 'apple', 'apply']
# Instantiate the Trie
obj = Trie()

# Insert words into the Trie
obj.insert("apple")
obj.insert("app")
obj.insert("apply")
obj.insert("application")
obj.insert("apt")
obj.insert("bat")
obj.insert("batch")
obj.insert("banana")

# Test cases to validate the functionality
test_cases = [
    ("app", ["app", "apple", "apply", "application"]),  # Words starting with 'app'
    ("ap", ["app", "apple", "apply", "application", "apt"]),  # Words starting with 'ap'
    ("bat", ["bat", "batch"]),  # Words starting with 'bat'
    ("ban", ["banana"]),  # Words starting with 'ban'
    ("b", ["bat", "batch", "banana"]),  # Words starting with 'b'
    ("xyz", []),  # No words should match this prefix
]

# Run each test case
for prefix, expected in test_cases:
    result = obj.findWordsWithPrefix(prefix)
    print(f"Prefix: '{prefix}', Expected: {expected}, Result: {result}")
    assert sorted(result) == sorted(expected), f"Test failed for prefix: {prefix}"

print("All test cases passed!")
```
