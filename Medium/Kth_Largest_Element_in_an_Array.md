# 🔢 Kth Largest Element in an Array (LeetCode)


## 📌 **Problem Statement**
Given an integer array `nums` and an integer `k`, return the `k`th largest element in the array.

**Example 1:**
```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```
**Example 2:**
```
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

---

## 🚀 **Solution Approach**
We use a **Min-Heap** (`heapq`) of size `k` to efficiently find the **Kth largest element** in `O(n log k)` time complexity.

### **Optimized Min-Heap Approach**
```python
import heapq

def findKthLargest(nums, k):
    min_heap = nums[:k]  # Take first k elements
    heapq.heapify(min_heap)  # Convert to Min-Heap

    for num in nums[k:]:  # Process remaining elements
        if num > min_heap[0]:  # If num is larger than heap's smallest
            heapq.heappushpop(min_heap, num)  # Replace it

    return min_heap[0]  # Kth largest element

# Example Usage
nums = [3, 2, 1, 5, 6, 4]
k = 2
print(findKthLargest(nums, k))  # Output: 5
```

---

## ⚡ **Complexity Analysis**
| Approach | Time Complexity | Space Complexity |
|----------|---------------|----------------|
| Sorting | `O(n log n)` | `O(1)` |
| Min-Heap | `O(n log k)` | `O(k)` |

🔹 **Min-Heap is better for large `n` when `k` is small!**  

---


## 🏆 **Topics Covered**
✅ **Heaps & Priority Queues**  
✅ **Sorting & Selection Algorithms**  
✅ **Optimized Searching**  

---

## 🌟 **How to Run**
1. Clone the repository:
   ```bash
   git clone https://github.com/VishwasChakilam/LeetCode-Solutions.git
   ```
---

## 🏆 **Contribute**
Found a better approach? Feel free to fork and submit a **pull request**! 🚀  

---

## 📬 **Connect With Me**
🔗 **GitHub**: [VishwasChakilam](https://github.com/Vishwas-Chakilam)  
🔗 **LinkedIn**: [Your LinkedIn Profile](https://linkedin.com/in/Vishwas-Chakilam)  
🔗 **YouTube**: [Vcode](https://www.youtube.com/@Vcode)  

⭐ **If this helped, give it a star!** 🌟


---

### **🔹 Why is this README effective?**
✅ **Explains problem clearly**  
✅ **Includes optimized solution with explanation**  
✅ **Has clear project structure & instructions**  
✅ **Encourages contributions**  
---
