## 208. Implement Prefix Tree

The idea here is to make a tree where each node has a child node of the next letters in the word.
We add to the tree by traversing it while the letters are the same and then appending new nodes after they differ.

                     L
                  O    I
                V   S    V
               E     T     E

    class Node:
        def __init__(self):
            self.children = {}
            self.end = False

    class Trie:

        def __init__(self):
            self.root = Node()

        def insert(self, word: str) -> None:
            current = self.root
            for letter in word:
                if letter not in current.children:
                    current.children[letter] = Node()
                current = current.children[letter]
            current.end = True

        def search(self, word: str) -> bool:
            current = self.root
            for letter in word:
                if letter not in current.children:
                    return False
                current = current.children[letter]
            return current.end

        def startsWith(self, prefix: str) -> bool:
            current = self.root
            for letter in prefix:
                if letter not in current.children:
                    return False
                current = current.children[letter]
            return True

## 1268 Search Suggestions System

Solved mostly with non prefix tree (sort and binary search or 2 pointers)

    class Trie:
        def __init__(self):
            self.d = collections.defaultdict(list)

        def insert(self, word):
            for i in range(len(word)):
                self.d[word[:i + 1]].append(word)

        def find(self, word):
            res = []
            for i in range(len(word)):
                res.append(self.d[word[:i + 1]][:3])
            return res

    class Solution:
        def suggestedProducts(self, products: List[str], searchWord: str) -> List[List[str]]:
            products.sort()
            t = Trie()
            for i in products:
                t.insert(i)

            res = t.find(searchWord)
            return res
