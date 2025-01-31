# 🚀 LeetCode 997: Find the Town Judge

## 📝 Problem Statement
In a town of `n` people labeled from `1` to `n`, there is a rumor that one of them is the **town judge**.

The town judge must satisfy the following conditions:
1. The judge **trusts nobody**.
2. **Everybody (except the judge)** trusts the judge.
3. **Exactly one** person satisfies these conditions.

Given an array `trust` where `trust[i] = [a, b]` means that **person `a` trusts person `b`**, return the **label of the town judge** if they exist. Otherwise, return `-1`.

---

## 🔍 Example Cases

### **Example 1**
**Input:**
```python
n = 3
trust = [[1,3], [2,3]]
```
**Output:**
```python
3
```
**Explanation:**  
- `1` trusts `3`  
- `2` trusts `3`  
- `3` trusts no one and is trusted by `2` people → ✅ Judge is `3`

---

### **Example 2**
**Input:**
```python
n = 3
trust = [[1,3], [2,3], [3,1]]
```
**Output:**
```python
-1
```
**Explanation:**  
- `1` and `2` trust `3`, but `3` also trusts `1`, violating the "judge trusts nobody" rule.

---

## 💡 Approach

### **Using In-Degree & Out-Degree (Efficient Approach)**
- Maintain two arrays:
  - **`indegree[i]`** → Counts how many people trust person `i`.
  - **`outdegree[i]`** → Counts how many people person `i` trusts.
- A **judge** should satisfy:
  - `indegree[i] == n-1` (trusted by everyone except themselves)
  - `outdegree[i] == 0` (trusts no one)

---

## 🏆 Optimal Python Solution
```python
from typing import List

class Solution:
    def findJudge(self, n: int, trust: List[List[int]]) -> int:
        indegree = [0] * (n + 1)

        for a, b in trust:
            indegree[a] -= 1  # If someone trusts another, they can't be the judge
            indegree[b] += 1  # Increase trust score of the person being trusted

        for i in range(1, n + 1):
            if indegree[i] == n - 1:
                return i
        return -1
```

### **Complexity Analysis**
| Approach  | Time Complexity | Space Complexity |
|-----------|---------------|----------------|
| Using In-Degree & Out-Degree | `O(N)` | `O(N)` |

---

## 🔷 Java Implementation
```java
class Solution {
    public int findJudge(int n, int[][] trust) {
        int[] trustScore = new int[n + 1]; // 1-based index

        for (int[] t : trust) {
            trustScore[t[0]]--; // If someone trusts, they can't be the judge
            trustScore[t[1]]++; // If someone is trusted, increase their trust score
        }

        for (int i = 1; i <= n; i++) {
            if (trustScore[i] == n - 1) {
                return i;
            }
        }
        return -1;
    }
}
```

---

## 📌 Edge Cases Considered
✔ **No trust relationships (`trust` is empty)** → Return `n` (everyone trusts the judge implicitly).  
✔ **Judge does not exist** → Return `-1`.  
✔ **Multiple possible judges** → Should not happen since only one judge can exist.  

---

## 🏅 Related Topics
- Graph Theory
- Hash Maps
- In-Degree & Out-Degree

---

---

## 🌟 Contributing
If you have an optimized solution or additional test cases, feel free to submit a **pull request**! 🤝

---

## 📌 References
- [LeetCode 997 - Find the Town Judge](https://leetcode.com/problems/find-the-town-judge/)
```

