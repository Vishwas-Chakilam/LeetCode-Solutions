# Length of Last Word - Leetcode Solution

## Problem Statement
Given a string `s` consisting of words and spaces, return the length of the last word in the string.

### Constraints:
- `1 <= s.length <= 10^4`
- `s` consists of only English letters and spaces.
- There will be at least one word in `s`.

## Code Implementation

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        s = s.strip()
        s = s.split(' ')
        return len(s[-1])
```

## Test Cases

| Input | Expected Output |
|-------|----------------|
| "Hello World" | 5 |
| "   fly me   to   the moon  " | 4 |
| "luffy is still joyboy" | 6 |

## Test Results
- **Input:** `"Hello World"`
  - **Output:** `5`
- **Input:** `"   fly me   to   the moon  "`
  - **Output:** `4`
- **Input:** `"luffy is still joyboy"`
  - **Output:** `6`

## Complexity Analysis
- **Time Complexity:** \(O(n)\), where `n` is the length of the string.
- **Space Complexity:** \(O(1)\), since only a few extra variables are used.

## References
- [Leetcode Problem](https://leetcode.com/problems/length-of-last-word/)

