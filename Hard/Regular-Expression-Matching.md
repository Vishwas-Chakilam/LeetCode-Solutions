# Regular Expression Matching

## Description

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `.` and `*` where:

- `.` Matches any single character.
- `*` Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

**Example:**

**Input:**
```python
s = "aab"
p = "c*a*b"
```

**Output:**
```python
True
```

**Explanation:**
The pattern `c*a*b` matches the string `aab`. Here, `c*` matches zero `c`s, `a*` matches two `a`s, and `b` matches `b`.

---

## Solution

### Approach

To solve this problem, we use dynamic programming (DP). We create a 2D DP table where `dp[i][j]` is `True` if the first `i` characters of the string `s` match the first `j` characters of the pattern `p`.

1. **Initialize the DP Table:** Set `dp[0][0]` to `True`, as an empty string matches an empty pattern.
2. **Handle Pattern with `*`:** A `*` can match zero or more characters of the preceding element, so initialize the table accordingly.
3. **Fill the DP Table:** Iterate over each character of `s` and `p`, updating the DP table based on the matching rules.

### Code

```python
def is_match(s, p):
    m, n = len(s), len(p)
    dp = [[False] * (n + 1) for _ in range(m + 1)]
    dp[0][0] = True

    # Handle patterns with '*' at the beginning
    for j in range(1, n + 1):
        if p[j - 1] == '*':
            dp[0][j] = dp[0][j - 2]

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if p[j - 1] == s[i - 1] or p[j - 1] == '.':
                dp[i][j] = dp[i - 1][j - 1]
            elif p[j - 1] == '*':
                dp[i][j] = dp[i][j - 2] or (dp[i - 1][j] and (s[i - 1] == p[j - 2] or p[j - 2] == '.'))

    return dp[m][n]
```

### Complexity Analysis

- **Time Complexity:** O(m * n), where `m` is the length of the string `s` and `n` is the length of the pattern `p`. This is because we fill a DP table of size `m x n`.
- **Space Complexity:** O(m * n), due to the DP table used to store intermediate results.

---

## Edge Cases

- **Empty String and Pattern:** An empty string matches an empty pattern, but a non-empty pattern might match an empty string if it consists of characters and `*` that account for the whole string.
- **Patterns with Consecutive `*`:** Handle patterns where `*` follows another `*`, e.g., `a**b`.

---

## Additional Notes

- This DP approach ensures that all possible matches are considered and efficiently computed.
- The solution handles various edge cases and ensures correct matching based on the regular expression rules.

---

## References

**LeetCode Problem Link:** [Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

---
