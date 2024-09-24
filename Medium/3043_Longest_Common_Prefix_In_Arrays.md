# Longest Common Prefix in Arrays

## 1. Problem Statement

You are given two arrays with positive integers `arr1` and `arr2`.

A prefix of a positive integer is an integer formed by one or more of its digits, starting from its leftmost digit. For example, 123 is a prefix of the integer 12345, while 234 is not.

A common prefix of two integers `a` and `b` is an integer `c`, such that `c` is a prefix of both `a` and `b`. For example, 5655359 and 56554 have a common prefix `565` while `1223` and `43456` do not have a common prefix.

You need to find the length of the longest common prefix between all pairs of integers `(x, y)` such that `x` belongs to `arr1` and `y` belongs to `arr2`.

Return the length of the longest common prefix among all pairs. If no common prefix exists among them, return `0`.

### Example:
```python
Input: arr1 = [1, 10, 100], arr2 = [1000]
Output: 3
```

---

## 2. Test Cases

### Test Case 1:
```python
arr1 = [1, 10, 100]
arr2 = [1000]
# Expected Output: 3
```

### Test Case 2:
```python
arr1 = [123, 567, 789]
arr2 = [456, 678]
# Expected Output: 0 (No common prefix)
```

### Test Case 3:
```python
arr1 = [100, 101, 102]
arr2 = [10, 100]
# Expected Output: 2 (Common prefix "10")
```

### Test Case 4:
```python
arr1 = [34567, 12345]
arr2 = [345, 98765]
# Expected Output: 3 (Common prefix "345")
```

---

## 3. Approach

### 3a. Brute Force Approach

In this method, we compare every pair `(x, y)` where `x` is an element from `arr1` and `y` is an element from `arr2`. For each pair, we find the length of the common prefix by comparing digits one by one.

#### Time Complexity:
- **Time**: O(m * n * k), where `m` is the length of `arr1`, `n` is the length of `arr2`, and `k` is the number of digits (average) in each integer.
- **Space**: O(m + n) to store the string versions of integers.

#### Code Implementation:

```python
def longestCommonPrefixBruteForce(arr1, arr2):
    def common_prefix_length(s1, s2):
        i = 0
        while i < len(s1) and i < len(s2) and s1[i] == s2[i]:
            i += 1
        return i
    
    max_length = 0
    str_arr1 = [str(x) for x in arr1]
    str_arr2 = [str(y) for y in arr2]
    
    for x in str_arr1:
        for y in str_arr2:
            max_length = max(max_length, common_prefix_length(x, y))
    
    return max_length
```

---

### 3b. Optimized Approach (Two Pointer Method)

This optimized method sorts both `arr1` and `arr2` and uses two pointers to traverse through the sorted arrays. This allows us to reduce the number of unnecessary comparisons, and since numbers with similar values are closer in sorted order, it is more efficient.

#### Time Complexity:
- **Time**: O(m log m + n log n) for sorting both arrays, plus O(m + n) for comparing the integers.
- **Space**: O(m + n) for storing the string versions of the integers.

#### Code Implementation:

**Python**:
```python
def longestCommonPrefixOptimized(arr1, arr2):
    def common_prefix_length(s1, s2):
        i = 0
        while i < len(s1) and i < len(s2) and s1[i] == s2[i]:
            i += 1
        return i
    
    arr1.sort()
    arr2.sort()

    max_length = 0
    str_arr1 = [str(x) for x in arr1]
    str_arr2 = [str(y) for y in arr2]

    i, j = 0, 0
    while i < len(str_arr1) and j < len(str_arr2):
        max_length = max(max_length, common_prefix_length(str_arr1[i], str_arr2[j]))
        if str_arr1[i] < str_arr2[j]:
            i += 1
        else:
            j += 1

    return max_length
```

**Java**:
```java
import java.util.Arrays;

public class Solution {
    public static int longestCommonPrefix(int[] arr1, int[] arr2) {
        Arrays.sort(arr1);
        Arrays.sort(arr2);
        
        int maxLength = 0;
        int i = 0, j = 0;

        while (i < arr1.length && j < arr2.length) {
            String s1 = String.valueOf(arr1[i]);
            String s2 = String.valueOf(arr2[j]);
            maxLength = Math.max(maxLength, commonPrefixLength(s1, s2));
            
            if (arr1[i] < arr2[j]) {
                i++;
            } else {
                j++;
            }
        }

        return maxLength;
    }

    private static int commonPrefixLength(String s1, String s2) {
        int length = 0;
        while (length < s1.length() && length < s2.length() && s1.charAt(length) == s2.charAt(length)) {
            length++;
        }
        return length;
    }
}
```

---

## 4. Edge Cases

- **Empty Arrays**: If either `arr1` or `arr2` is empty, the result should be `0`.
- **No Common Prefix**: If there is no common prefix between any elements of `arr1` and `arr2`, the function should return `0`.
- **Single-Digit Numbers**: The algorithm should handle single-digit numbers, where there may or may not be common prefixes.
- **Duplicate Values**: If there are duplicate values in the arrays, the algorithm should still compute the correct result.

---

## 5. References

- **LeetCode Problem**: [Link to LeetCode Problem](https://leetcode.com/problems/)
