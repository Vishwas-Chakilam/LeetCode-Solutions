# Longest Common Prefix

## Description

Write a function to find the longest common prefix string amongst an array of strings. If there is no common prefix, return an empty string `""`.

**Example:**

**Input:**
```python
strs = ["flower","flow","flight"]
```

**Output:**
```python
"fl"
```

**Explanation:**
The longest common prefix among the given strings is `"fl"`.

---

## Solution

### Approach

To find the longest common prefix:
1. **Sort the Array:** Sort the input list of strings. After sorting, the common prefix of the entire array must be the common prefix between the first and the last strings.
2. **Compare Characters:** Compare characters one by one between the first and the last strings until a mismatch is found.

### Code

```python
def longest_common_prefix(strs):
    if not strs:
        return ""
    
    # Sort the array of strings
    strs.sort()
    
    # Compare the first and last strings
    first, last = strs[0], strs[-1]
    i = 0
    
    # Find the common prefix between the first and last strings
    while i < len(first) and i < len(last) and first[i] == last[i]:
        i += 1
    
    return first[:i]
```

### Complexity Analysis

- **Time Complexity:** O(n * log n + m), where `n` is the number of strings and `m` is the length of the shortest string. Sorting the array takes O(n * log n), and comparing characters takes O(m).
- **Space Complexity:** O(1), as we are only using a few extra variables for comparison.

---

## Edge Cases

- **Empty Input Array:** If the input array is empty, return an empty string.
- **No Common Prefix:** If no common prefix exists, return an empty string.
- **Single String:** If there is only one string in the input array, the longest common prefix is the string itself.

---

## Additional Notes

- Sorting the array ensures that the strings with the most differences are compared first, allowing for a more efficient comparison.
- This solution efficiently handles edge cases, including arrays with no common prefix.

---

## References

**LeetCode Problem Link:** [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

---
