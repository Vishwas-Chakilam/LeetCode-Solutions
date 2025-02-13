# 🔢 LeetCode 3066: Minimum Operations to Exceed Threshold Value II

## 📌 **Problem Statement**
You are given an integer array `nums` and an integer `k`.  
In one operation, you can:
- Remove two smallest numbers, say `a` and `b`
- Insert a new number `2a + b` back into the array

The goal is to perform **minimum operations** until the smallest number in the array becomes **at least `k`**.

---

## 🚀 **Optimized Solution Approach**
We use a **Min-Heap (`heapq`)** to always extract the two smallest elements efficiently.

### **Heap Approach (Greedy + Priority Queue)**
```python
import heapq

class Solution:
    def minOperations(self, nums: list[int], k: int) -> int:
        heapq.heapify(nums)  # Convert array to Min-Heap
        op = 0
        
        while nums[0] < k:  # Repeat until min element >= k
            a = heapq.heappop(nums)  # Smallest element
            b = heapq.heappop(nums)  # Second smallest
            heapq.heappush(nums, a * 2 + b)  # Insert new element
            op += 1
        
        return op
```

---

## ⚡ **Complexity Analysis**
| Approach | Time Complexity | Space Complexity |
|----------|---------------|----------------|
| Sorting (Brute Force) | `O(n log n)` | `O(1)` |
| Min-Heap (Optimized) | `O(n log n)` | `O(n)` |

🔹 **Min-Heap is the best approach as it ensures we always pick the smallest elements efficiently.**  

---

## 🏆 **Topics Covered**
✅ **Heaps & Priority Queues**  
✅ **Greedy Algorithms**  
✅ **Sorting & Selection Algorithms**  

---

## 🌟 **How to Run**
1. Clone the repository:
   ```bash
   git clone https://github.com/Vishwas-Chakilam/LeetCode-Solutions.git
   ```

---

## 🏆 **Contribute**
Found a better approach? Feel free to fork and submit a **pull request**! 🚀  

---

## 📬 **Connect With Me**
🔗 **GitHub**: [Vishwas-Chakilam](https://github.com/Vishwas-Chakilam)  
🔗 **LinkedIn**: [Vishwas-Chakilam](https://linkedin.com/in/Vishwas-Chakilam)  
🔗 **YouTube**: [Vcode](https://www.youtube.com/@Vcode)  

⭐ **If this helped, give it a star!** 🌟


### **🔹 Why is this README effective?**
✅ **Clearly explains the problem**  
✅ **Includes an optimized solution with explanation**  
✅ **Has a structured project directory**  
✅ **Encourages contributions and engagement**  
---
