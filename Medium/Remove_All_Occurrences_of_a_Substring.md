# Remove All Occurrences of a Substring

## Problem Statement
Given a string `s` and a string `part`, remove all occurrences of `part` in `s` until `part` can no longer be found. The final string should be returned.

### **Example 1:**
#### **Input:**
```plaintext
s = "daabcbaabcbc"
part = "abc"
```
#### **Output:**
```plaintext
"dab"
```
#### **Explanation:**
- Remove `"abc"` → `"dabaabcbc"`
- Remove `"abc"` again → `"dab"`

---

## **Approach**
We use a **stack-based approach** to efficiently remove occurrences of `part` in `s`. 

### **Algorithm**
1. **Use a stack (list) to store characters of `s`**.
2. **Iterate through each character in `s`**:
   - Append it to the stack.
   - If the last `len(part)` characters in the stack match `part`, remove them.
3. **Convert the stack to a string and return the result**.

---

## **Python Solution**
```python
class Solution:
    def removeOccurrences(self, s: str, part: str) -> str:
        stack = []
        part_len = len(part)

        for char in s:
            stack.append(char)
            if ''.join(stack[-part_len:]) == part:
                del stack[-part_len:]  # Remove the last occurrence of "part"

        return ''.join(stack)

# Example Usage:
sol = Solution()
print(sol.removeOccurrences("daabcbaabcbc", "abc"))  # Output: "dab"
```

---

## **Complexity Analysis**
- **Time Complexity**: **O(n * m)** (where `n` is the length of `s` and `m` is the length of `part`).
- **Space Complexity**: **O(n)** (for the stack storage).

---

## **Edge Cases Considered**
✅ `s` does not contain `part` → Returns `s` unchanged.  
✅ `s` is an empty string → Returns `""`.  
✅ `part` is an empty string → Returns `s` unchanged.  
✅ Multiple non-overlapping occurrences of `part`.  
✅ Consecutive overlapping occurrences of `part`.  

---

## **Alternative Approach (Using `str.replace`)**
If `part` is small compared to `s`, we can repeatedly use the `replace()` function:
```python
class Solution:
    def removeOccurrences(self, s: str, part: str) -> str:
        while part in s:
            s = s.replace(part, "")
        return s
```
✅ **Time Complexity**: Approx. **O(n * m)**  
✅ **Space Complexity**: **O(1)** (modifying `s` directly)  

However, this approach is less efficient for large `s` as `replace()` creates new strings.

---

## **Contributing**
Feel free to open an issue or submit a pull request if you find a more optimal approach or want to add additional test cases!

---

## **License**
This code is available under the MIT License.

---

### 🚀 **Happy Coding!**
---
