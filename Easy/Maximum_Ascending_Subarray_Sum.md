# 🚀 LeetCode 1800: Maximum Ascending Subarray Sum

## 📌 Problem Statement
Given an array of positive integers `nums`, return the **maximum possible sum** of an **ascending subarray**.

A subarray is **ascending** if every element is **strictly greater** than the previous one.

### 🔹 Example 1:
```plaintext
Input: nums = [10, 20, 30, 5, 10, 50]
Output: 65
Explanation: The maximum ascending subarray is [5, 10, 50] with sum = 65.
```

### 🔹 Example 2:
```plaintext
Input: nums = [10, 20, 30, 40, 50]
Output: 150
Explanation: The entire array is an ascending subarray.
```

### 🔹 Constraints:
- `1 <= nums.length <= 100`
- `1 <= nums[i] <= 100`

---

## 🛠 Solution Approach

We traverse the array **once** and keep track of:
- The **current ascending subarray sum**.
- The **maximum sum encountered**.

### **Time Complexity:**
- **O(n)** → Single-pass traversal.

---

## 💻 Solutions in Different Languages

### ✅ **Python Solution**
```python
from typing import List

class Solution:
    def maxAscendingSum(self, nums: List[int]) -> int:
        max_sum = 0
        current_sum = nums[0]

        for i in range(1, len(nums)):
            if nums[i] > nums[i - 1]:  
                current_sum += nums[i]  
            else:  
                max_sum = max(max_sum, current_sum)
                current_sum = nums[i]  
        
        return max(max_sum, current_sum)
```

---

### ✅ **Java Solution**
```java
class Solution {
    public int maxAscendingSum(int[] nums) {
        int maxSum = 0, currentSum = nums[0];

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > nums[i - 1]) {
                currentSum += nums[i];
            } else {
                maxSum = Math.max(maxSum, currentSum);
                currentSum = nums[i];
            }
        }

        return Math.max(maxSum, currentSum);
    }
}
```


---

## 🔥 Contribute
If you find an optimized solution, feel free to **contribute**!  

1. **Fork the repository**  
2. **Create a new branch**  
   ```sh
   git checkout -b feature-better-solution
   ```
3. **Commit your changes**  
   ```sh
   git commit -m "Optimized solution for LeetCode 1800"
   ```
4. **Push and create a pull request**!  

---

## ⭐ Show Some Love
If you like this repository, **star ⭐ it and follow** for more solutions! 🚀  



## 🎯 Why is this README Effective?
✅ Clear explanation of the problem  
✅ Well-structured solutions in multiple languages  
✅ Instructions on how to run the code  
✅ Encourages contribution  
✅ Professional and engaging format  
---
```
