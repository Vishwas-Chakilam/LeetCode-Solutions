# 1497. Check If Array Pairs Are Divisible by k

## 1. Problem Statement

Given an array of integers `arr` and an integer `k`, you need to check whether the array can be divided into pairs such that the sum of each pair is divisible by `k`.

### Example:
```python
Input: arr = [3, 8, 17, 2], k = 5
Output: True
Explanation: Pairs (3, 2) and (8, 17) have sums 5 and 25, which are divisible by 5.
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: arr = [9, 7, 5, 3], k = 3
Output: True
Explanation: Pairs (9, 3) and (7, 5) both have sums divisible by 3.
```

### Test Case 2:
```python
Input: arr = [9, 7, 5, 3], k = 2
Output: False
Explanation: It is not possible to find pairs where the sum is divisible by 2.
```

### Test Case 3:
```python
Input: arr = [1, 2, 3, 4, 5, 10], k = 5
Output: True
Explanation: Pairs (1, 4), (2, 3), and (5, 10) all have sums divisible by 5.
```

---

## 3. Approach

### 3a. Brute Force Approach:
In the brute force approach, we can generate all possible pairs from the array and check if their sum is divisible by `k`. This will take O(n^2) time to generate the pairs and check their sums. This approach is inefficient for larger inputs.

#### Time Complexity:
- **O(n^2)** for generating all pairs and checking their sums.

#### Space Complexity:
- **O(1)** as no additional space is required apart from the input array.

### 3b. Optimized Approach (Using Remainders):
1. Calculate the remainder of each element when divided by `k` (`arr[i] % k`).
2. Store the frequency of each remainder in a hashmap.
3. For the array to be divisible into valid pairs:
   - For each element `x`, the remainder `x % k` must have a complementary remainder `(k - (x % k)) % k` present in the hashmap with equal frequency.
   - Handle special cases when `remainder == 0` and when `remainder == k/2`.

#### Time Complexity:
- **O(n)** because we only need to calculate the remainders and check their frequencies.

#### Space Complexity:
- **O(k)** for storing remainder frequencies in a hashmap.

---

## 4. Code Implementation

### Python Implementation:
```python
from collections import defaultdict

def canArrange(arr, k):
    remainder_count = defaultdict(int)
    
    # Calculate the remainder count
    for num in arr:
        remainder = num % k
        if remainder < 0:
            remainder += k
        remainder_count[remainder] += 1
    
    # Check pairs
    for rem in remainder_count:
        if rem == 0:
            if remainder_count[rem] % 2 != 0:
                return False
        elif remainder_count[rem] != remainder_count[k - rem]:
            return False
    
    return True

# Example
arr = [3, 8, 17, 2]
k = 5
print(canArrange(arr, k))  # Output: True
```

### Java Implementation:
```java
import java.util.HashMap;

public class Solution {
    public boolean canArrange(int[] arr, int k) {
        HashMap<Integer, Integer> remainderCount = new HashMap<>();
        
        // Calculate the remainder count
        for (int num : arr) {
            int remainder = num % k;
            if (remainder < 0) {
                remainder += k;
            }
            remainderCount.put(remainder, remainderCount.getOrDefault(remainder, 0) + 1);
        }
        
        // Check pairs
        for (int rem : remainderCount.keySet()) {
            if (rem == 0) {
                if (remainderCount.get(rem) % 2 != 0) {
                    return false;
                }
            } else if (!remainderCount.get(rem).equals(remainderCount.get(k - rem))) {
                return false;
            }
        }
        
        return true;
    }
    
    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] arr = {3, 8, 17, 2};
        int k = 5;
        System.out.println(solution.canArrange(arr, k));  // Output: True
    }
}
```

---

## 5. Edge Cases
- **Negative numbers**: Remainders should always be positive. Adjust negative remainders accordingly.
- **When no valid pairs exist**: If the sum of all possible pairs is not divisible by `k`, return `False`.
- **Single element**: If the array contains only one element, no valid pair can be formed.

---

## 6. References
- **LeetCode Problem**: [1497. Check If Array Pairs Are Divisible by k](https://leetcode.com/problems/check-if-array-pairs-are-divisible-by-k/)
- **Collections Documentation (Python)**: [Defaultdict](https://docs.python.org/3/library/collections.html#collections.defaultdict)

---
