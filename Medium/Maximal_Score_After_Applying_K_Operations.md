# Problem: Maximal Score After Applying K Operations

## 1. Problem Statement

You are given a **zero-indexed** integer array `nums` and an integer `k`. You have to perform exactly `k` operations on the array. In an operation, choose any index `i` such that `0 <= i < nums.length`, replace `nums[i]` with `ceil(nums[i] / 3)` (replace it with the smallest integer greater than or equal to `nums[i] / 3`), and add the original value of `nums[i]` to your score. 

Return the maximal score you can obtain after exactly `k` operations.

### Example 1:
```python
Input: nums = [10,10,10,10,10], k = 5
Output: 50
Explanation:
- The array initially is [10,10,10,10,10].
- Apply the operation on index 0, the array becomes [4,10,10,10,10]. The score becomes 10.
- Apply the operation on index 1, the array becomes [4,4,10,10,10]. The score becomes 20.
- Apply the operation on index 2, the array becomes [4,4,4,10,10]. The score becomes 30.
- Apply the operation on index 3, the array becomes [4,4,4,4,10]. The score becomes 40.
- Apply the operation on index 4, the array becomes [4,4,4,4,4]. The score becomes 50.
So, the maximal score is 50.
```

### Example 2:
```python
Input: nums = [1,10,3,3,3], k = 3
Output: 17
Explanation:
- The array initially is [1,10,3,3,3].
- Apply the operation on index 1, the array becomes [1,4,3,3,3]. The score becomes 10.
- Apply the operation on index 1 again, the array becomes [1,2,3,3,3]. The score becomes 14.
- Apply the operation on index 1 again, the array becomes [1,1,3,3,3]. The score becomes 17.
```

### Constraints:
- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^9`
- `1 <= k <= 10^5`

---

## 2. Test Cases

### Test Case 1:
```python
Input: nums = [10,10,10,10,10], k = 5
Output: 50
```

### Test Case 2:
```python
Input: nums = [1,10,3,3,3], k = 3
Output: 17
```

### Test Case 3:
```python
Input: nums = [1000000000], k = 1
Output: 1000000000
```

### Test Case 4:
```python
Input: nums = [5,10,15], k = 2
Output: 25
```

---

## 3. Approach

### 3a. Brute Force with Time and Space Complexity

In a brute-force approach, we would repeatedly find the largest number in the array, apply the operation, and repeat this process `k` times. This approach is inefficient because finding the largest number takes `O(n)` time, and we do it `k` times, leading to a high time complexity.

#### Time Complexity:
- **O(k * n)** where `n` is the size of the array and `k` is the number of operations.

#### Space Complexity:
- **O(1)** since no extra space is used beyond the input array.

### 3b. Optimized Approach with Max-Heap (Priority Queue)

We can optimize the approach using a **max-heap** (priority queue). The steps are as follows:
1. Add all elements of `nums` into a max-heap.
2. For each operation:
   - Extract the largest number from the heap.
   - Add the number to the score.
   - Replace the number with `ceil(num / 3)` and push it back into the heap.
3. Repeat this for `k` operations.

#### Time Complexity:
- **O(k log n)** where `n` is the size of the array and `k` is the number of operations. Each heap operation (pop and push) takes `O(log n)` time.

#### Space Complexity:
- **O(n)** for storing the heap.

---

## 4. Code Implementation

### Python Implementation:
```python
import heapq
import math

def maxScoreAfterKOperations(nums, k):
    # Convert to a max-heap by negating the numbers
    maxHeap = [-num for num in nums]
    heapq.heapify(maxHeap)
    
    score = 0
    
    for _ in range(k):
        # Pop the largest number from the heap
        largest = -heapq.heappop(maxHeap)
        score += largest
        
        # Calculate the next value after applying the operation and push it back
        nextValue = math.ceil(largest / 3)
        heapq.heappush(maxHeap, -nextValue)
    
    return score
```

### Java Implementation:
```java
import java.util.PriorityQueue;

public class Solution {
    public int maxScoreAfterKOperations(int[] nums, int k) {
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
        
        for (int num : nums) {
            maxHeap.add(num);
        }
        
        int score = 0;
        
        for (int i = 0; i < k; i++) {
            int largest = maxHeap.poll();
            score += largest;
            
            // Apply the operation and push the new value back to the heap
            maxHeap.add((largest + 2) / 3);
        }
        
        return score;
    }
}
```

---

## 5. Edge Cases

- **Single element in the list**: The largest element will be repeatedly divided until k operations are exhausted.
- **All elements are the same**: The algorithm should correctly handle this case and apply operations on any element.
- **k is greater than the number of elements**: The algorithm should efficiently handle repeated operations even when the heap only has a few elements.

---

## 6. References

- **LeetCode Problem**: [Maximal Score After Applying K Operations](https://leetcode.com/problems/maximal-score-after-applying-k-operations/)

---
