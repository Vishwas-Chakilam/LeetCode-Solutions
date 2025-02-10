# **LeetCode Solution: 3174. Clear Digits**  

## 📌 Problem Statement  
**Problem Name:** **Clear Digits** (LeetCode **3174**)  
📎 **Difficulty:** *TBD (Easy/Medium/Hard)*  

🔹 Given a **string `s` containing digits and lowercase letters**, the task is to **remove all digits** while maintaining the relative order of the remaining characters.  

### **Example**  
#### **Input:**  
```plaintext
s = "a1b2c3"
```
#### **Output:**  
```plaintext
"abc"
```
#### **Explanation:**  
- Remove `1`, `2`, and `3`, resulting in `"abc"`.  

---

## 💡 Approach  
### **Method 1: Using List Comprehension (Python)**
- Iterate through each character in `s`.  
- **Keep only non-digit characters**.  
- Join them to form the final output string.  

### **Code Implementation (Python)**
```python
def clear_digits(s: str) -> str:
    return ''.join([char for char in s if not char.isdigit()])
```

⏳ **Time Complexity:** `O(n)` (where `n` is the length of the string)  
💾 **Space Complexity:** `O(n)` (as we store the filtered characters)  

---

## 🏆 Alternative Approaches  
### **Method 2: Using Regular Expressions (Regex)**
```python
import re

def clear_digits(s: str) -> str:
    return re.sub(r'\d', '', s)
```
🔹 Uses `re.sub()` to replace all digits (`\d`) with an empty string.  
⚡ **Performance:** Comparable to list comprehension, but may be slower for small inputs.  

---

## 🤝 Contributions  
📌 **Found a better solution?** Open a **pull request** with your optimized approach!  

✅ Ensure:  
- **Efficient code** ⏳  
- **Proper documentation** 📄  
- **Edge case handling** 💡  

---

## 📜 License  
This repository is **open-source** under the **MIT License**.  

---

## 📬 Contact  
For questions, reach out via **GitHub Issues** or **email**.  

📌 **Found this helpful? Star ⭐ the repo!** 🚀  

---

### **Happy Coding! 🚀🎯**  

---
