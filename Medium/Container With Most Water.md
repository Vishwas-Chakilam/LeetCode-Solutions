# Container With Most Water - Leetcode Solution

## Problem Statement
Given an integer array `height` of length `n`, where `height[i]` represents the height of a vertical line at index `i`, find two lines that together with the x-axis form a container, such that the container holds the most water.

Return the maximum amount of water a container can store.

### Constraints:
- `n >= 2`
- `0 <= height[i] <= 10^4`

## Solution Approach
This solution implements a **two-pointer approach** to efficiently find the maximum water container area.

### Algorithm:
1. Initialize two pointers: `left` at the beginning (index `0`) and `right` at the end (index `n-1`) of the array.
2. Calculate the area using the formula:
   
   \[ \text{area} = (\text{right} - \text{left}) \times \min(\text{height}[\text{left}], \text{height}[\text{right}]) \]
   
3. Update `maxArea` if the computed area is greater.
4. Move the pointer pointing to the smaller height, as increasing the width won't help if the height is not improved.
5. Repeat until the two pointers meet.

## Code Implementation

```java
class Solution {
    public int maxArea(int[] height) {
        int maxarea = 0;
        int left = 0;
        int right = height.length - 1;
        
        while (left < right) {
            maxarea = Math.max(maxarea, (right - left) * Math.min(height[left], height[right]));
            
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        
        return maxarea;
    }
}
```

## Complexity Analysis
- **Time Complexity:** \(O(n)\), since each element is visited at most once.
- **Space Complexity:** \(O(1)\), as only a few extra variables are used.

## Example Walkthrough
**Input:** `[1,8,6,2,5,4,8,3,7]`

**Execution Steps:**
- Start with pointers at `0` and `8`.
- Compute the area and move the smaller height pointer.
- Repeat until the pointers meet.

**Output:** `49`

## Related Topics
- Two Pointers
- Greedy Algorithms
- Array Manipulation

## References
- [Leetcode Problem](https://leetcode.com/problems/container-with-most-water/)

