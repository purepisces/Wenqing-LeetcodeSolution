我们通过树结构来优化算法, 可以画个图.
首先比如apple的话 第一层root就是a, 然后第二层是p,第三层是p,第四层是l, 第五层是e.
然后就需要每个node有children这个概念来保存代表这个递进性,同时还需要每个node有endofword的标识,因为search apple True, 但是search app false.
```css
Root (TrieNode) -> children = {'c': TrieNode}
 |
 -- 'c' (TrieNode) -> children = {'a': TrieNode}
      |
      -- 'a' (TrieNode) -> children = {'t': TrieNode, 'r': TrieNode}
          |
          -- 't' (TrieNode) -> children = {}, endOfWord = True (for "cat")
          -- 'r' (TrieNode) -> children = {}, endOfWord = True (for "car")
```

```python
class TrieNode():
    def __init__(self):
        self.children = {}
        self.endOfWord = False
class Trie(object):

    def __init__(self):
        self.root = TrieNode()
        
    def insert(self, word):
        """
        :type word: str
        :rtype: None
        """
        cur = self.root
        for c in word:
            if c not in cur.children:
                cur.children[c] = TrieNode()
            cur = cur.children[c]
        cur.endOfWord = True
        

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
        return cur.endOfWord
        

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
        

        


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```
___
Wrong Implementation:
1.mistakenly assigned the Trienode class itself to cur.children[c] instead of creating an instance of it. Specifically, this line:
```
# wrong implementation
cur.children[c] = Trienode
```
should be
```
# correct implementation
cur.children[c] = Trienode()
```
Wrong implementation:

Stuck here, don't know how to append characters in this structure. Should just be `cur.children[c] = TrieNode()`, we can just insert the c as the key, and leave the value just be TrieNode().
```python
class TrieNode(object):
    def __init__(self, val=0):
        self.val = val
        self.child = {}
        self.endofword = False
class Trie(object):

    def __init__(self):
        self.root = TrieNode()
        

    def insert(self, word):
        """
        :type word: str
        :rtype: None
        """
        cur = self.root
        for c in word:
            if c not in cur.child:
                cur.child[c] = TrieNode(val = c)

        

    def search(self, word):
        """
        :type word: str
        :rtype: bool
        """
        

    def startsWith(self, prefix):
        """
        :type prefix: str
        :rtype: bool
        """
        


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```
