# Reverse String II

## Problem Statement
Given a string `s` and an integer `k`, reverse the first `k` characters for every `2k` characters counting from the start of the string. If there are fewer than `k` characters left, reverse all of them. If there are between `k` and `2k` characters, reverse the first `k` characters and leave the rest as is.

### Example 1:
**Input:**
```plaintext
s = "abcdefg", k = 2
```
**Output:**
```plaintext
"bacdfeg"
```

### Example 2:
**Input:**
```plaintext
s = "abcd", k = 2
```
**Output:**
```plaintext
"bacd"
```

## Approach
1. Convert the string to a list of characters (since strings are immutable in Python and Java).
2. Iterate through the string in steps of `2k`.
3. Reverse the first `k` characters in each `2k` segment.
4. Convert the list back to a string and return the result.

## Complexity Analysis
- **Time Complexity:** `O(n)`, where `n` is the length of the string, as we traverse the string once.
- **Space Complexity:** `O(n)`, due to storing the mutable list.

## Solutions
### Python Solution
```python
def reverseStr(s: str, k: int) -> str:
    s = list(s)
    for i in range(0, len(s), 2 * k):
        s[i:i + k] = reversed(s[i:i + k])
    return "".join(s)

# Example Usage
s = "abcdefg"
k = 2
print(reverseStr(s, k))  # Output: "bacdfeg"
```

### Java Solution
```java
class Solution {
    public String reverseStr(String s, int k) {
        char[] arr = s.toCharArray();
        for (int i = 0; i < arr.length; i += 2 * k) {
            int left = i, right = Math.min(i + k - 1, arr.length - 1);
            while (left < right) {
                char temp = arr[left];
                arr[left++] = arr[right];
                arr[right--] = temp;
            }
        }
        return new String(arr);
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.reverseStr("abcdefg", 2)); // Output: "bacdfeg"
    }
}
```

## Edge Cases Considered
- `s` is an empty string.
- `k` is larger than the length of `s`.
- `k` is 1 (single character swaps).
- `s` contains special characters or spaces.

## Related Topics
- String Manipulation
- Two Pointers
- Greedy Algorithm
---
