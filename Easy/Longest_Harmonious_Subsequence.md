# Longest Harmonious Subsequence

## 1. Problem Statement

We define a harmonious array as an array where the difference between its maximum value and its minimum value is exactly 1.

Given an integer array `nums`, return the length of its longest harmonious subsequence among all its possible subsequences.

A **subsequence** of array is a sequence that can be derived from the array by deleting some or no elements without changing the order of the remaining elements.

### Example:

```python
Input: nums = [1,3,2,2,5,2,3,7]
Output: 5

Explanation: The longest harmonious subsequence is [3,2,2,2,3].
```

### Constraints:
- `1 <= nums.length <= 2 * 10^4`
- `-10^9 <= nums[i] <= 10^9`

---

## 2. Test Cases

### Test Case 1:
```python
nums = [1, 3, 2, 2, 5, 2, 3, 7]
# Expected Output: 5
```

### Test Case 2:
```python
nums = [1, 2, 3, 4]
# Expected Output: 2
```

### Test Case 3:
```python
nums = [1, 1, 1, 1]
# Expected Output: 0
```

### Test Case 4:
```python
nums = [10, 10, 9, 9, 8]
# Expected Output: 4
```

---

## 3. Approach

### 3a. Brute Force Approach

In the brute-force approach, we can check every possible subsequence and verify whether it is harmonious. A subsequence is harmonious if the difference between its maximum and minimum values is exactly 1.

#### Time Complexity:
- **Time**: O(n^2), where `n` is the length of the array.
- **Space**: O(1).

#### Code Implementation (Python):
```python
def findLHSBruteForce(nums):
    max_length = 0
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if abs(nums[i] - nums[j]) == 1:
                length = sum(1 for x in nums if x == nums[i] or x == nums[j])
                max_length = max(max_length, length)
    return max_length
```

### 3b. Optimized Approach (HashMap)

A more efficient approach is to use a **hashmap** to count the frequency of each number in the array. Then, for each key in the hashmap, check whether there is a key that differs by exactly 1 (i.e., `key + 1`). If such a key exists, the harmonious subsequence consists of elements from both `key` and `key + 1`.

#### Time Complexity:
- **Time**: O(n), where `n` is the length of the array.
- **Space**: O(n) for the hashmap.

#### Code Implementation (Python):
```python
from collections import Counter

def findLHS(nums):
    freq_map = Counter(nums)
    max_length = 0
    
    for num in freq_map:
        if num + 1 in freq_map:
            max_length = max(max_length, freq_map[num] + freq_map[num + 1])
    
    return max_length
```

---

## 4. Edge Cases

- **Array with all same elements**: If all elements in `nums` are the same, there is no harmonious subsequence, and the result should be 0.
- **Array with no harmonious pairs**: If the difference between any two numbers is not exactly 1, there is no harmonious subsequence, and the result should be 0.
- **Large array size**: The optimized approach should efficiently handle large input sizes without exceeding time limits.

---

## 5. References

- **HashMap Approach**: [GeeksforGeeks - Find the Longest Harmonious Subsequence](https://www.geeksforgeeks.org/longest-harmonious-subsequence/)
- **LeetCode Problem**: [Longest Harmonious Subsequence](https://leetcode.com/problems/longest-harmonious-subsequence/)

---
