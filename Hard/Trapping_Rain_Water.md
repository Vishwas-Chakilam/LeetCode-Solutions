# Trapping Rain Water Problem  

## Problem Statement  
Given an array `height` of non-negative integers where each element represents the height of a bar in a histogram, compute how much water can be trapped between the bars after raining.  

### Example  
#### Input:  
```python
height = [0,1,0,2,1,0,1,3,2,1,2,1]
```
#### Output:  
```python
6
```
#### Explanation:  
The bars form valleys where water gets trapped. The total trapped water in this case is `6` units.

---

## Approach  
This solution uses **Dynamic Programming (DP)** to precompute maximum heights from the left and right.  

### Algorithm:  
1. **Edge Case Check**: If the `height` list is empty, return `0`.  
2. **Precompute Left Max Heights**: Create an array `left_max` where `left_max[i]` stores the maximum height from the start to index `i`.  
3. **Precompute Right Max Heights**: Create an array `right_max` where `right_max[i]` stores the maximum height from the end to index `i`.  
4. **Compute Trapped Water**: Iterate over the array and for each index `i`, calculate the trapped water as:  
   \[
   \text{water} = \min(\text{left\_max}[i], \text{right\_max}[i]) - \text{height}[i]
   \]
   Add this value to the result.  

---

## Code Implementation  

```python
from typing import List

class Solution:
    def trap(self, height: List[int]) -> int:
        if not height:
            return 0

        n = len(height)
        left_max = [0] * n
        right_max = [0] * n
        res = 0

        # Fill left_max array
        left_max[0] = height[0]
        for i in range(1, n):
            left_max[i] = max(left_max[i - 1], height[i])

        # Fill right_max array
        right_max[n - 1] = height[n - 1]
        for i in range(n - 2, -1, -1):
            right_max[i] = max(right_max[i + 1], height[i])

        # Calculate trapped water
        for i in range(n):
            res += min(left_max[i], right_max[i]) - height[i]

        return res
```

---

## Complexity Analysis  
- **Time Complexity**: \( O(n) \) → Three passes are made over the array (one for `left_max`, one for `right_max`, and one for computing trapped water).  
- **Space Complexity**: \( O(n) \) → Two extra arrays (`left_max` and `right_max`) are used.  

---

## Optimized Approach (Two Pointers)  
To reduce space complexity to \( O(1) \), we can use the **two-pointer** approach instead of extra arrays.

### Steps:
1. Use `left` and `right` pointers to traverse the array.  
2. Maintain `left_max` and `right_max` variables instead of arrays.  
3. Compute trapped water using the **minimum of left and right max heights** dynamically.  

### Optimized Code:
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        if not height:
            return 0

        left, right = 0, len(height) - 1
        left_max, right_max = 0, 0
        res = 0

        while left < right:
            if height[left] < height[right]:
                if height[left] >= left_max:
                    left_max = height[left]
                else:
                    res += left_max - height[left]
                left += 1
            else:
                if height[right] >= right_max:
                    right_max = height[right]
                else:
                    res += right_max - height[right]
                right -= 1

        return res
```

- **Time Complexity**: \( O(n) \)  
- **Space Complexity**: \( O(1) \)  

---

## Summary  
- The **DP approach** precomputes max heights on both sides and runs in \( O(n) \) time with \( O(n) \) space.  
- The **Two Pointers approach** reduces space complexity to \( O(1) \) while keeping the time complexity \( O(n) \).  
- Both approaches are efficient for solving the problem.  

---

## Related Topics  
✅ **Dynamic Programming**  
✅ **Two Pointers**  
✅ **Stack-Based Approach** (Alternate solution)  

---
