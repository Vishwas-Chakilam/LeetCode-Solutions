# 1963. Minimum Number of Swaps to Make the String Balanced

## 1. Problem Statement

You are given a string `s` of even length consisting of `[` and `]` brackets. A string is considered **balanced** if it consists entirely of pairs of opening and closing brackets: `[]`.

You can swap two brackets at any position to make the string balanced. Return the **minimum** number of swaps needed to make the string balanced.

### Example 1:
```python
Input: s = "]]][[["
Output: 2
Explanation: The two swaps are:
1. Swap the first and last brackets -> "[[]][]"
2. Swap the second and fifth brackets -> "[[][]]"
```

### Example 2:
```python
Input: s = "[]"
Output: 0
Explanation: The string is already balanced.
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: s = "[]][][[]"
Output: 1
Explanation: Swap the second and third bracket -> "[][][]"
```

### Test Case 2:
```python
Input: s = "[]"
Output: 0
Explanation: No swaps are needed as the string is already balanced.
```

### Test Case 3:
```python
Input: s = "]]]][[[["
Output: 3
Explanation: Swap three pairs of brackets to make the string balanced.
```

---

## 3. Approach

### 3a. Brute Force with Time and Space Complexity

- A brute force approach would involve trying to swap brackets in multiple ways, but this is inefficient.
- Time complexity: **O(n^2)** due to multiple swaps and checking at each step.
- Space complexity: **O(n)** for storing the string.

### 3b. Optimized Method with Time and Space Complexity

- We can maintain a count of unbalanced brackets while iterating through the string.
- When encountering a closing bracket `]` before a matching opening bracket `[`, this indicates an imbalance.
- Count how many times the closing bracket appears out of order, and calculate the number of swaps required to fix it.
- This can be achieved by counting the maximum depth of imbalance (`maxclose`), and the minimum number of swaps needed will be `(maxclose + 1) // 2`.

#### Time Complexity:
- **O(n)**, where n is the length of the string (one pass).

#### Space Complexity:
- **O(1)**, constant extra space is used.

---

## 4. Code Implementation

### Python Implementation:
```python
def minSwaps(s: str) -> int:
    close, maxclose = 0, 0
    for char in s:
        if char == '[':
            close -= 1
        else:
            close += 1
        maxclose = max(close, maxclose)
    return (maxclose + 1) // 2

# Example usage:
s = "[]][][[]"
print(minSwaps(s))  # Output: 1
```

### Java Implementation:
```java
public class Solution {
    public int minSwaps(String s) {
        int close = 0, maxClose = 0;
        for (char c : s.toCharArray()) {
            if (c == '[') {
                close--;
            } else {
                close++;
            }
            maxClose = Math.max(maxClose, close);
        }
        return (maxClose + 1) / 2;
    }
}
```

---

## 5. Edge Cases

- **Already Balanced String**: If the string is already balanced, no swaps are required (return `0`).
- **Maximum Imbalance**: If the string consists of only closing brackets followed by opening brackets, multiple swaps will be required.
- **Empty string**: The output will be `0` since no operations are needed.

---

## 6. References
- **LeetCode Problem**: [1963. Minimum Number of Swaps to Make the String Balanced](https://leetcode.com/problems/minimum-number-of-swaps-to-make-the-string-balanced/)
