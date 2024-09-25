# 2416. Sum of Prefix Scores of Strings

## 1. Problem Statement

You are given an array of strings `words`. Every string in `words` is a lowercase English letter string.

A **prefix** of a string is any leading contiguous substring of the string. For example, "abc" is a prefix of "abcdef".

The **prefix score** of a string is the sum of scores for all of its prefixes. The score of a prefix is defined as the number of strings in `words` that contain the prefix.

Return an array of integers `answer` where `answer[i]` is the prefix score of `words[i]`.

### Example:
```python
Input: words = ["abc", "ab", "bc", "b"]
Output: [5, 4, 3, 2]

Explanation:
For "abc", the prefixes are "a", "ab", and "abc".
    - "a" is a prefix of 2 strings: "abc", "ab".
    - "ab" is a prefix of 2 strings: "abc", "ab".
    - "abc" is a prefix of 1 string: "abc".
  Prefix score of "abc" = 2 + 2 + 1 = 5.

For "ab", the prefixes are "a", "ab".
  Prefix score of "ab" = 2 + 2 = 4.

For "bc", the prefixes are "b", "bc".
  Prefix score of "bc" = 2 + 1 = 3.

For "b", the prefix is "b".
  Prefix score of "b" = 2.
```

---

## 2. Test Cases

### Test Case 1:
```python
words = ["abc", "ab", "bc", "b"]
# Expected Output: [5, 4, 3, 2]
```

### Test Case 2:
```python
words = ["a", "b", "c", "abc", "ab"]
# Expected Output: [4, 2, 1, 5, 4]
```

### Test Case 3:
```python
words = ["apple", "ape", "app", "banana"]
# Expected Output: [5, 3, 3, 1]
```

### Test Case 4:
```python
words = ["dog", "dot", "dove", "do"]
# Expected Output: [3, 3, 2, 3]
```

---

## 3. Approach

### 3a. Brute Force Approach

The brute-force approach involves generating all prefixes for each word and counting how many words in the list contain each prefix. This can be done using nested loops, where for each word, we check all other words to count occurrences of the current prefix.

#### Time Complexity:
- **Time**: O(n * m^2), where `n` is the number of words, and `m` is the average length of the words. Each word generates multiple prefixes, and for each prefix, we search in the list of words.
- **Space**: O(n * m) for storing prefixes.

#### Code Implementation (Python):
```python
def sumPrefixScoresBruteForce(words):
    def prefix_score(word, words):
        score = 0
        for i in range(1, len(word) + 1):
            prefix = word[:i]
            score += sum(1 for w in words if w.startswith(prefix))
        return score
    
    return [prefix_score(word, words) for word in words]
```

### 3b. Optimized Approach (Trie)

We can optimize the brute-force approach by using a **Trie** (Prefix Tree) data structure. We build the Trie from all the words and, for each node in the Trie, maintain a count of how many words have passed through that node. This way, when we calculate the score for a word, we just need to traverse the Trie, and the score for each prefix is the count stored in the Trie node corresponding to that prefix.

#### Time Complexity:
- **Time**: O(n * m), where `n` is the number of words, and `m` is the average length of the words. Inserting each word into the Trie and calculating the score takes linear time.
- **Space**: O(n * m) for storing the Trie nodes.

#### Code Implementation (Python):
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.count = 0

class Solution:
    def sumPrefixScores(self, words):
        root = TrieNode()

        # Build the Trie
        for word in words:
            node = root
            for char in word:
                if char not in node.children:
                    node.children[char] = TrieNode()
                node = node.children[char]
                node.count += 1

        # Calculate scores for each word
        res = []
        for word in words:
            node = root
            score = 0
            for char in word:
                node = node.children[char]
                score += node.count
            res.append(score)
        
        return res
```

---

## 4. Edge Cases

- **Single letter words**: The algorithm should handle single-letter words, where the prefix is the word itself.
- **All words are the same**: The algorithm should correctly calculate the prefix scores when all words are identical.
- **No common prefix**: If there are no common prefixes among any words, each word's score should reflect that.
- **Large input size**: The optimized approach should handle large input sizes efficiently without timing out.

---

## 5. References
- **LeetCode Problem**: [Sum of Prefix Scores of Strings](https://leetcode.com/problems/sum-of-prefix-scores-of-strings/)

---
