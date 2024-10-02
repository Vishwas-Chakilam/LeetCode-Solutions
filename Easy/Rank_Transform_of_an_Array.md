# 1331. Rank Transform of an Array

## 1. Problem Statement

Given an array of integers `arr`, replace each element with its rank. The rank represents how large the element is compared to the other elements, where the smallest element is assigned the rank `1`. If two elements are equal, they should have the same rank.

### Example:
```python
Input: arr = [40, 10, 20, 30]
Output: [4, 1, 2, 3]
Explanation: The ranks are assigned as follows: 40 is the largest, so it gets rank 4, 30 gets rank 3, 20 gets rank 2, and 10 gets rank 1.
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: arr = [100, 100, 100]
Output: [1, 1, 1]
Explanation: Since all elements are the same, they all get the same rank of 1.
```

### Test Case 2:
```python
Input: arr = [37, 12, 28, 9, 100, 56]
Output: [5, 3, 4, 1, 6, 5]
Explanation: The ranks are assigned based on the sorted order of the unique elements.
```

### Test Case 3:
```python
Input: arr = [-5, 0, 10, -10]
Output: [2, 3, 4, 1]
Explanation: -10 is the smallest, so it gets rank 1, -5 gets rank 2, 0 gets rank 3, and 10 gets rank 4.
```

---

## 3. Approach

### 3a. Brute Force Approach:
Sort the array, then replace each element with its position in the sorted array. However, this approach would require sorting and looping multiple times, leading to inefficiencies.

#### Time Complexity:
- **O(n log n)** for sorting the array.

#### Space Complexity:
- **O(n)** for storing the sorted array and ranks.

### 3b. Optimized Approach (Using a Hashmap):
1. First, create a sorted version of the array with unique elements.
2. Assign ranks based on the sorted position of the unique elements.
3. Use a hashmap to store the ranks for each element in the original array.
4. Replace each element in the original array with its rank.

#### Time Complexity:
- **O(n log n)** because we sort the array.
  
#### Space Complexity:
- **O(n)** for storing the ranks in a hashmap.

---

## 4. Code Implementation

### Python Implementation:
```python
def arrayRankTransform(arr):
    # Step 1: Sort the unique elements
    sorted_unique = sorted(set(arr))
    
    # Step 2: Assign ranks based on the sorted position
    rank_map = {num: rank + 1 for rank, num in enumerate(sorted_unique)}
    
    # Step 3: Replace elements with their ranks
    return [rank_map[num] for num in arr]

# Example
arr = [40, 10, 20, 30]
print(arrayRankTransform(arr))  # Output: [4, 1, 2, 3]
```

### Java Implementation:
```java
import java.util.Arrays;
import java.util.HashMap;

public class Solution {
    public int[] arrayRankTransform(int[] arr) {
        int[] sortedArr = Arrays.copyOf(arr, arr.length);
        Arrays.sort(sortedArr);
        
        // Use a hashmap to store ranks
        HashMap<Integer, Integer> rankMap = new HashMap<>();
        int rank = 1;
        for (int num : sortedArr) {
            if (!rankMap.containsKey(num)) {
                rankMap.put(num, rank++);
            }
        }
        
        // Replace each element in the original array with its rank
        for (int i = 0; i < arr.length; i++) {
            arr[i] = rankMap.get(arr[i]);
        }
        
        return arr;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] arr = {40, 10, 20, 30};
        System.out.println(Arrays.toString(solution.arrayRankTransform(arr)));  // Output: [4, 1, 2, 3]
    }
}
```

---

## 5. Edge Cases
- **Empty array**: Return an empty array.
- **All elements are the same**: All elements should be assigned the same rank.
- **Negative numbers**: The solution should work with negative integers as well.
  
---

## 6. References
- **LeetCode Problem**: [1331. Rank Transform of an Array](https://leetcode.com/problems/rank-transform-of-an-array/)

---
