# Longest Substring Without Repeating Characters

## Description

Given a string `s`, find the length of the longest substring without repeating characters.

**Example 1:**

**Input:**
```python
s = "abcabcbb"
```

**Output:**
```python
3
```

**Explanation:** The answer is `"abc"`, with the length of 3.

**Example 2:**

**Input:**
```python
s = "bbbbb"
```

**Output:**
```python
1
```

**Explanation:** The answer is `"b"`, with the length of 1.

**Example 3:**

**Input:**
```python
s = "pwwkew"
```

**Output:**
```python
3
```

**Explanation:** The answer is `"wke"`, with the length of 3. Note that the answer must be a substring, `"pwke"` is a subsequence and not a substring.

---

## Solution

### Approach

We can solve this problem using the **sliding window** technique. We use two pointers (`left` and `right`) to define a window in the string, which expands to the right as we find new unique characters and contracts from the left if we encounter repeating characters.

Steps:
1. Use a **set** to track characters within the current window.
2. Move the `right` pointer and add characters to the set.
3. If a character repeats, move the `left` pointer until there are no repeating characters in the window.
4. Keep track of the maximum length of all such windows.

### Code

```python
def lengthOfLongestSubstring(s):
    char_set = set()
    left = 0
    max_len = 0

    for right in range(len(s)):
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        char_set.add(s[right])
        max_len = max(max_len, right - left + 1)

    return max_len
```

### Complexity Analysis

- **Time Complexity:** O(n), where `n` is the length of the string `s`. Both the `right` and `left` pointers move at most `n` times.
- **Space Complexity:** O(min(n, m)), where `n` is the length of the string and `m` is the size of the character set. The size of the character set is typically constant for ASCII (256 characters), making this approach efficient in terms of space.

---

## Edge Cases

- **Empty String:** If `s` is an empty string, the result is `0`.
- **String with All Unique Characters:** If all characters in the string are unique, the result is the length of the string.
- **String with All Repeated Characters:** If the string consists of one repeated character (e.g., `"aaaaa"`), the result is `1`.

---

## Additional Notes

- This problem is a classic example of the sliding window technique combined with a hash set to efficiently track the characters in the current window.
- The sliding window approach helps in reducing the time complexity from O(n^2) (brute force) to O(n).

---

## References

**LeetCode Problem Link:** [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
