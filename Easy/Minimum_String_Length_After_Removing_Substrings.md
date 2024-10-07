# 2698. Minimum String Length After Removing Substrings

## 1. Problem Statement

You are given a string `s` consisting of only characters 'A', 'B', and 'C'. You can perform the following operation on the string any number of times:

- Remove the substring "AB" or "BA" from the string.

Your task is to return the minimum length of the string after performing any number of these operations.

### Example 1:
```python
Input: s = "ABFCACDB"
Output: 5
Explanation: Remove "AB" -> "FCACDB", then no more "AB" or "BA" can be removed.
```

### Example 2:
```python
Input: s = "ACBBD"
Output: 5
Explanation: There are no "AB" or "BA" substrings to remove.
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: s = "ABAB"
Output: 0
Explanation: Remove both "AB"s -> "" (empty string), the string becomes empty.
```

### Test Case 2:
```python
Input: s = "AABBCC"
Output: 4
Explanation: Remove both "AB"s -> "BBCC".
```

### Test Case 3:
```python
Input: s = "ABCBAC"
Output: 2
Explanation: Remove "AB" -> "CBAC", then remove "BA" -> "CC".
```

---

## 3. Approach

### 3a. Brute Force with Time and Space Complexity

- Iterate through the string and remove "AB" or "BA" whenever found.
- Keep track of changes made. If no more changes are possible, the final string length will be the answer.

#### Time Complexity:
- **O(n)** per operation (n is the length of the string), but repeated until no changes occur, so it can go up to **O(n^2)** in the worst case.

#### Space Complexity:
- **O(n)** due to space used to store intermediate results.

### 3b. Optimized Method with Time and Space Complexity

- Use a stack to efficiently remove the substrings.
- As we traverse the string, we push characters onto the stack.
- If the top of the stack and the current character form the substring "AB" or "BA", pop the top and continue.
- Finally, the size of the stack will be the minimum length of the string.

#### Time Complexity:
- **O(n)**, where n is the length of the string. Each character is pushed and popped from the stack at most once.

#### Space Complexity:
- **O(n)** for the stack.

---

## 4. Code Implementation

### Python Implementation:
```python
def minLength(s: str) -> int:
    stack = []
    for char in s:
        if stack and ((stack[-1] == 'A' and char == 'B') or (stack[-1] == 'B' and char == 'A')):
            stack.pop()  # Remove the pair "AB" or "BA"
        else:
            stack.append(char)
    return len(stack)

# Example usage
s = "ABFCACDB"
print(minLength(s))  # Output: 5
```

### Java Implementation:
```java
public class Solution {
    public int minLength(String s) {
        Stack<Character> stack = new Stack<>();
        for (char ch : s.toCharArray()) {
            if (!stack.isEmpty() && ((stack.peek() == 'A' && ch == 'B') || (stack.peek() == 'B' && ch == 'A'))) {
                stack.pop();  // Remove the pair "AB" or "BA"
            } else {
                stack.push(ch);
            }
        }
        return stack.size();
    }
}
```

---

## 5. Edge Cases

- **Empty string**: The output will be `0`.
- **No removable substrings**: If there are no "AB" or "BA" substrings, the length of the string remains the same.
- **Multiple "AB" or "BA" substrings**: All possible substrings should be removed.
- **All removable substrings**: If the string consists only of "AB" or "BA", it should reduce to an empty string.

---

## 6. References
- **LeetCode Problem**: [2698. Minimum String Length After Removing Substrings](https://leetcode.com/problems/minimum-string-length-after-removing-substrings/)
