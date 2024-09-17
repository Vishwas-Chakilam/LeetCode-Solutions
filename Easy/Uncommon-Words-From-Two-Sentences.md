# Uncommon Words from Two Sentences

## Description

We are given two sentences `s1` and `s2`. A word is **uncommon** if it appears exactly once in one of the sentences and does not appear in the other sentence. We need to return a list of all such uncommon words.

**Example 1:**

**Input:**
```python
s1 = "this apple is sweet"
s2 = "this apple is sour"
```

**Output:**
```python
["sweet", "sour"]
```

**Example 2:**

**Input:**
```python
s1 = "apple apple"
s2 = "banana"
```

**Output:**
```python
["banana"]
```

---

## Solution

### Approach

The problem can be solved by breaking it into the following steps:

1. **Count the frequency of each word** in both sentences combined. This can be done using a `Counter` from the `collections` module, which will store the count of each word in a dictionary-like structure.
2. **Identify uncommon words** by selecting the words that appear exactly once across both sentences.
3. **Return the list** of words that are uncommon based on the criteria.

### Code

```python
from collections import Counter

def uncommonFromSentences(s1, s2):
    # Split the sentences into words and combine them into one list
    words = s1.split() + s2.split()
    
    # Count the frequency of each word
    word_count = Counter(words)
    
    # Return the words that appear exactly once
    return [word for word in word_count if word_count[word] == 1]
```

### Complexity Analysis

- **Time Complexity:** O(n + m), where `n` is the number of words in `s1` and `m` is the number of words in `s2`. We traverse both sentences once to count the words.
- **Space Complexity:** O(n + m), where `n` and `m` are the number of words in `s1` and `s2`, respectively. This is due to the storage of word counts.

---

## Edge Cases

- **No Uncommon Words:** If all words appear more than once or in both sentences, the result will be an empty list.
- **Single Word Sentences:** If one or both sentences contain only one word, the result depends on whether the word appears in both or just one of the sentences.
- **Empty Input:** If either or both of the sentences are empty, the result will be based on the words from the non-empty sentence.

---

## Additional Notes

- The use of a `Counter` allows us to efficiently count word occurrences and filter out words that appear more than once.
- The order of the uncommon words in the result does not matter, as the problem does not specify any particular order for the output.

---

## References

**LeetCode Problem Link:** [Uncommon Words from Two Sentences](https://leetcode.com/problems/uncommon-words-from-two-sentences/)
