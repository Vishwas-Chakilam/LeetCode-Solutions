# 1590. Make Sum Divisible by P

## 1. Problem Statement

Given an array of positive integers `nums`, remove the **smallest** subarray (could be empty) such that the **sum** of the remaining elements is divisible by a positive integer `p`. Return the length of the smallest subarray that you need to remove, or -1 if it's impossible.

A **subarray** is defined as a contiguous block of elements in the array.

### Example 1:
```python
Input: nums = [3,1,4,2], p = 6
Output: 1
Explanation: After removing [4], the sum of the remaining elements is 3 + 1 + 2 = 6, which is divisible by 6.
```

### Example 2:
```python
Input: nums = [6,3,5,2], p = 9
Output: 2
Explanation: We need to remove [5, 2], the sum of the remaining elements is 6 + 3 = 9, which is divisible by 9.
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: nums = [1,2,3], p = 3
Output: 0
Explanation: The entire array sum is already divisible by 3, so no removal is needed.
```

### Test Case 2:
```python
Input: nums = [1,2,3], p = 7
Output: -1
Explanation: It's impossible to make the sum divisible by 7 by removing any subarray.
```

### Test Case 3:
```python
Input: nums = [8,1,2,3,9], p = 7
Output: 1
Explanation: Removing [1] results in the remaining sum being divisible by 7.
```

---

## 3. Approach

### 3a. Brute Force Approach:
- Find all subarrays and calculate the sum of the remaining elements after removing the subarray.
- If the sum of the remaining elements is divisible by `p`, record the length of the subarray.
- Return the length of the smallest valid subarray.

#### Time Complexity:
- **O(n^3)** for generating all subarrays and checking sums.

#### Space Complexity:
- **O(1)** for storing the subarrays and results.

### 3b. Optimized Approach (Using Prefix Sums and Modulo Arithmetic):
- Compute the total sum of the array and calculate `target = total_sum % p`.
- If `target == 0`, return 0 (no removal needed).
- Use a hashmap to store the prefix sums modulo `p` and find the smallest subarray that can make the sum divisible by `p`.

#### Time Complexity:
- **O(n)** for traversing the array once and using a hashmap.

#### Space Complexity:
- **O(n)** for storing the prefix sums.

---

## 4. Code Implementation

### Python Implementation:
```python
def minSubarray(nums, p):
    total_sum = sum(nums)
    target = total_sum % p
    if target == 0:
        return 0

    prefix_sum = 0
    prefix_map = {0: -1}
    min_length = len(nums)

    for i, num in enumerate(nums):
        prefix_sum = (prefix_sum + num) % p
        required = (prefix_sum - target) % p

        if required in prefix_map:
            min_length = min(min_length, i - prefix_map[required])

        prefix_map[prefix_sum] = i

    return min_length if min_length != len(nums) else -1

# Example
nums = [3, 1, 4, 2]
p = 6
print(minSubarray(nums, p))  # Output: 1
```

### Java Implementation:
```java
import java.util.HashMap;

public class Solution {
    public int minSubarray(int[] nums, int p) {
        int totalSum = 0;
        for (int num : nums) {
            totalSum += num;
        }
        int target = totalSum % p;
        if (target == 0) {
            return 0;
        }

        int prefixSum = 0;
        int minLen = nums.length;
        HashMap<Integer, Integer> prefixMap = new HashMap<>();
        prefixMap.put(0, -1);

        for (int i = 0; i < nums.length; i++) {
            prefixSum = (prefixSum + nums[i]) % p;
            int required = (prefixSum - target + p) % p;

            if (prefixMap.containsKey(required)) {
                minLen = Math.min(minLen, i - prefixMap.get(required));
            }

            prefixMap.put(prefixSum, i);
        }

        return minLen == nums.length ? -1 : minLen;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] nums = {3, 1, 4, 2};
        int p = 6;
        System.out.println(solution.minSubarray(nums, p));  // Output: 1
    }
}
```

---

## 5. Edge Cases
- **All elements are divisible by `p`**: Return 0.
- **No possible removal to make the sum divisible**: Return -1.
- **Empty array**: Return -1.
- **Small array with sum already divisible by `p`**: Return 0.

---

## 6. References
- **LeetCode Problem**: [1590. Make Sum Divisible by P](https://leetcode.com/problems/make-sum-divisible-by-p/)
