# Problem: Smallest Range Covering Elements from K Lists

## 1. Problem Statement

You are given `k` lists of sorted integers `nums[k]`. Your task is to find the smallest range `[a, b]` that includes at least one number from each of the `k` lists.

### Example 1:
```python
Input: nums = [[4,10,15,24,26], [0,9,12,20], [5,18,22,30]]
Output: [20,24]
Explanation: 
- The range [20, 24] includes at least one number from each list.
```

### Example 2:
```python
Input: nums = [[1,2,3], [1,2,3], [1,2,3]]
Output: [1,1]
```

### Constraints:
- `nums.length == k`
- `1 <= k <= 3500`
- `1 <= nums[i].length <= 50`
- `-10^5 <= nums[i][j] <= 10^5`

---

## 2. Test Cases

### Test Case 1:
```python
Input: nums = [[4,10,15,24,26], [0,9,12,20], [5,18,22,30]]
Output: [20,24]
```

### Test Case 2:
```python
Input: nums = [[1,2,3], [1,2,3], [1,2,3]]
Output: [1,1]
```

### Test Case 3:
```python
Input: nums = [[10,12,14], [11,13,15], [5,9,17]]
Output: [10,11]
```

---

## 3. Approach

### 3a. Brute Force with Time and Space Complexity

In the brute-force approach, we can try to calculate all possible ranges that include at least one element from each list. However, this approach is inefficient because we would have to check all combinations of elements from each list, resulting in a high time complexity.

#### Time Complexity:
- **O(n^k)** where `n` is the number of elements in each list and `k` is the number of lists.

#### Space Complexity:
- **O(n*k)** for storing all the elements and ranges.

### 3b. Optimized Approach with Min-Heap (Priority Queue)

We use a **min-heap** (or priority queue) to efficiently find the smallest range. The heap keeps track of the smallest elements from each list, and the largest element in the current range is tracked as well. 

The algorithm proceeds as follows:
1. Push the first element of each list into a min-heap.
2. Track the maximum element of the current range.
3. Pop the smallest element from the heap, update the range if necessary.
4. Continue by adding the next element from the list that was popped until one list is exhausted.

#### Time Complexity:
- **O(n log k)** where `n` is the total number of elements, and `k` is the number of lists. Sorting and heap operations contribute to the complexity.

#### Space Complexity:
- **O(k)** for storing elements in the heap.

---

## 4. Code Implementation

### Python Implementation:
```python
from heapq import heappush, heappop

def smallestRange(nums):
    minHeap = []
    maxInRange = float('-inf')
    
    # Push the first element of each list along with its indices
    for i in range(len(nums)):
        heappush(minHeap, (nums[i][0], i, 0))
        maxInRange = max(maxInRange, nums[i][0])
    
    smallestRange = [float('-inf'), float('inf')]
    
    while minHeap:
        minInRange, listIndex, elementIndex = heappop(minHeap)
        
        # Update smallest range
        if maxInRange - minInRange < smallestRange[1] - smallestRange[0]:
            smallestRange = [minInRange, maxInRange]
        
        # If the list is exhausted, break the loop
        if elementIndex + 1 == len(nums[listIndex]):
            break
        
        # Push the next element from the same list into the heap
        nextElement = nums[listIndex][elementIndex + 1]
        heappush(minHeap, (nextElement, listIndex, elementIndex + 1))
        
        # Update max in range
        maxInRange = max(maxInRange, nextElement)
    
    return smallestRange
```

### Java Implementation:
```java
import java.util.PriorityQueue;

public class Solution {
    public int[] smallestRange(List<List<Integer>> nums) {
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        int maxInRange = Integer.MIN_VALUE;
        
        // Add the first element of each list into the heap
        for (int i = 0; i < nums.size(); i++) {
            minHeap.add(new int[] { nums.get(i).get(0), i, 0 });
            maxInRange = Math.max(maxInRange, nums.get(i).get(0));
        }
        
        int[] smallestRange = { -100000, 100000 };
        
        while (true) {
            int[] current = minHeap.poll();
            int minInRange = current[0];
            int listIndex = current[1];
            int elementIndex = current[2];
            
            // Update smallest range
            if (maxInRange - minInRange < smallestRange[1] - smallestRange[0]) {
                smallestRange[0] = minInRange;
                smallestRange[1] = maxInRange;
            }
            
            // If we have exhausted a list, break
            if (elementIndex + 1 == nums.get(listIndex).size()) {
                break;
            }
            
            // Add the next element from the same list to the heap
            int nextElement = nums.get(listIndex).get(elementIndex + 1);
            minHeap.add(new int[] { nextElement, listIndex, elementIndex + 1 });
            maxInRange = Math.max(maxInRange, nextElement);
        }
        
        return smallestRange;
    }
}
```

---

## 5. Edge Cases

- **Lists of different lengths**: The algorithm should still work correctly when the lists have varying lengths.
- **Single list**: The smallest range is the range covered by the single list.
- **Overlapping ranges**: The algorithm should efficiently find the minimum range in case of overlapping ranges.

---

## 6. References

- **LeetCode Problem**: [Smallest Range Covering Elements from K Lists](https://leetcode.com/problems/smallest-range-covering-elements-from-k-lists/)

---
