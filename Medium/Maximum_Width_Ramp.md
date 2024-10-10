# 962. Maximum Width Ramp

## 1. Problem Statement

A ramp is defined as a pair `(i, j)` for `i < j` and `A[i] <= A[j]`. The width of such a ramp is `j - i`. We are given an integer array `A`, and we need to find the maximum width of a ramp in this array.

### Example 1:
```python
Input: A = [6,0,8,2,1,5]
Output: 4
Explanation: The maximum width ramp is between A[1] and A[5].
```

### Example 2:
```python
Input: A = [9,8,1,0,1,9,4,0,4,1]
Output: 7
Explanation: The maximum width ramp is between A[2] and A[9].
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: A = [6,0,8,2,1,5]
Output: 4
```

### Test Case 2:
```python
Input: A = [9,8,1,0,1,9,4,0,4,1]
Output: 7
```

### Test Case 3:
```python
Input: A = [5,5,5,5,5]
Output: 4
Explanation: Any pair can be a ramp, the largest possible difference is between indices `0` and `4`.
```

---

## 3. Approach

### 3a. Brute Force Approach

- We can try all possible pairs `(i, j)` with `i < j` and check if `A[i] <= A[j]`, then calculate the width `j - i` and keep track of the maximum width.
- **Time Complexity**: O(n^2), where n is the length of the array, as we compare each pair.
- **Space Complexity**: O(1).

### 3b. Optimized Approach with Time and Space Complexity

#### Sorted Index Approach:

- We create an array of sorted indices based on their corresponding values in `A`.
- We then iterate over the sorted indices and, at each index, calculate the maximum possible ramp width using the minimum index encountered so far.
- This ensures that we find the maximum difference where the value at `i` is less than or equal to the value at `j`.

#### Time Complexity:
- **O(n log n)** due to sorting, where n is the length of the array.

#### Space Complexity:
- **O(n)**, for storing the sorted indices.

---

## 4. Code Implementation

### Python Implementation:
```python
def maxWidthRamp(A: list[int]) -> int:
    sorted_indices = sorted(range(len(A)), key=lambda x: A[x])
    
    min_index = float('inf')
    max_width = 0
    
    for idx in sorted_indices:
        min_index = min(min_index, idx)
        max_width = max(max_width, idx - min_index)
    
    return max_width

# Example usage:
A = [6, 0, 8, 2, 1, 5]
print(maxWidthRamp(A))  # Output: 4
```

### Java Implementation:
```java
import java.util.*;

public class Solution {
    public int maxWidthRamp(int[] A) {
        Integer[] sortedIndices = new Integer[A.length];
        for (int i = 0; i < A.length; i++) {
            sortedIndices[i] = i;
        }
        
        Arrays.sort(sortedIndices, (a, b) -> Integer.compare(A[a], A[b]));
        
        int minIndex = Integer.MAX_VALUE;
        int maxWidth = 0;
        
        for (int idx : sortedIndices) {
            minIndex = Math.min(minIndex, idx);
            maxWidth = Math.max(maxWidth, idx - minIndex);
        }
        
        return maxWidth;
    }
}
```

---

## 5. Edge Cases

- **All elements are the same**: In this case, the entire array can be considered a ramp.
- **Already sorted array**: The width of the ramp will be the length of the array minus 1.
- **Descending array**: The width will be 0 as no valid ramp exists.

---

## 6. References

- **LeetCode Problem**: [962. Maximum Width Ramp](https://leetcode.com/problems/maximum-width-ramp/)

---
