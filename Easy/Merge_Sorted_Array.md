# **Merge Sorted Array**

## **Problem Statement**
You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2`, respectively.

Modify `nums1` **in-place** to merge `nums1` and `nums2` into a single sorted array.

### **Example**
#### **Input:**
```python
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6], n = 3
```
#### **Output:**
```python
nums1 = [1,2,2,3,5,6]
```

---

## **Optimized Two-Pointer Approach**
### **Approach**
1. We start filling `nums1` from the **end** (rightmost index) to avoid extra space usage.
2. Use two pointers:  
   - `p1` at index `m - 1` (last valid element of `nums1`)  
   - `p2` at index `n - 1` (last element of `nums2`)  
   - `p` at index `m + n - 1` (last index of `nums1`)  
3. Compare elements from `nums1[p1]` and `nums2[p2]`, placing the **larger** element at `nums1[p]`.
4. Continue the process until all elements are merged.

### **Code Implementation (Python)**
```python
from typing import List

class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        p1, p2, p = m - 1, n - 1, m + n - 1

        while p1 >= 0 and p2 >= 0:
            if nums1[p1] > nums2[p2]:
                nums1[p] = nums1[p1]
                p1 -= 1
            else:
                nums1[p] = nums2[p2]
                p2 -= 1
            p -= 1

        # If there are remaining elements in nums2, copy them
        while p2 >= 0:
            nums1[p] = nums2[p2]
            p2 -= 1
            p -= 1
```

---

## **Time Complexity Analysis**
- **Merging elements using two pointers:** **O(m + n)**
- **No extra space used**, as merging happens in-place.

---

## **Why This Approach?**
✔ **Efficient** – Only O(m + n) operations  
✔ **No Extra Space** – Modifies `nums1` directly  
✔ **Optimal** – Beats the sorting-based O((m+n) log(m+n)) solution  

---

This approach is widely used in **merging sorted arrays** in-place efficiently. 🚀  
