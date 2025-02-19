# Jump Game Solution

## Problem Statement
The problem is to determine if you can reach the last index of the array starting from the first index. Each element in the array represents your maximum jump length at that position.

## Solution Approach
The algorithm works by iterating from right to left, maintaining a `goal` index that represents the last position that needs to be reached. If the current index can reach the `goal`, the `goal` is updated to the current index. If by the end of the loop, the `goal` is at index 0, the function returns `true`; otherwise, it returns `false`.

## Code Implementation
```java
class Solution {
    public boolean canJump(int[] nums) {
        int goal = nums.length - 1;
        for (int i = nums.length - 2; i >= 0; i--) {
            if (nums[i] + i >= goal) {
                goal = i;
            }
        }
        return goal == 0;
    }
}
```

## Complexity Analysis
- **Time Complexity**: O(n), as we traverse the array once.
- **Space Complexity**: O(1), since we use only a few integer variables.


## Example
```java
Input: [2,3,1,1,4]
Output: true

Input: [3,2,1,0,4]
Output: false
```

## Contributing
Feel free to submit a pull request if you have improvements or optimizations.

## License
This project is open-source and available under the MIT License.

