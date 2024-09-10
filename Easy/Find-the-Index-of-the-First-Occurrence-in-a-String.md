# Find the Index of the First Occurrence in a String

## Description

Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

**Example:**

**Input:**
```python
haystack = "sadbutsad"
needle = "sad"
```

**Output:**
```python
0
```

**Explanation:**
The substring "sad" is found at index `0` in the string `haystack`. The first occurrence is at index `0`, even though "sad" appears again later at index `6`.

---

## Solution

### Approach

To solve this problem:
1. **String Search:** You can directly search for the `needle` in `haystack` using Python’s built-in string function `find()` which returns the index of the first occurrence of the substring or `-1` if it's not found.
2. Alternatively, a **Sliding Window Technique** can be used, where you iterate through `haystack` while checking for the substring match starting from each index.

### Code

```python
def str_str(haystack, needle):
    # Using Python's built-in find() method
    return haystack.find(needle)
```

#### Sliding Window Approach (Manual Implementation):

```python
def str_str(haystack, needle):
    if not needle:
        return 0
    
    for i in range(len(haystack) - len(needle) + 1):
        if haystack[i:i + len(needle)] == needle:
            return i
    
    return -1
```

### Complexity Analysis

- **Time Complexity:** O(n * m), where `n` is the length of `haystack` and `m` is the length of `needle`. In the worst case, the algorithm needs to check each substring of `haystack` of length `m`.
- **Space Complexity:** O(1), as we are not using any extra space aside from input strings.

---

## Edge Cases

- **Empty `needle`:** If `needle` is an empty string, return `0` (as per the problem statement).
- **`needle` larger than `haystack`:** If the length of `needle` is greater than `haystack`, return `-1`.
- **No match found:** If `needle` does not exist in `haystack`, return `-1`.

---

## Additional Notes

- The `find()` method is highly optimized in Python, making it a good default choice for simple string search problems.
- For large datasets or more complex matching, consider using more advanced algorithms like KMP (Knuth-Morris-Pratt) or Boyer-Moore.

---

## References

**LeetCode Problem Link:** [Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

---
