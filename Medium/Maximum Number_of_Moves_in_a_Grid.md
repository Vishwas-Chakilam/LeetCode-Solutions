# 2684. Maximum Number of Moves in a Grid

## Problem Statement
You are given an `m x n` integer grid where each cell contains an integer. From any cell `(i, j)`, you can move to any of the following cells:
- Right: `(i, j + 1)`
- Right-up: `(i - 1, j + 1)`
- Right-down: `(i + 1, j + 1)`

You can only move if the value in the next cell is **strictly greater** than the current cell. The goal is to determine the maximum number of moves you can make in the grid starting from any cell in the first column.

Return the maximum number of moves you can make.

### Example
#### Input:
```plaintext
grid = [
    [2,4,3,5],
    [5,4,9,3],
    [3,4,2,11],
    [10,9,13,15]
]
```
#### Output:
```plaintext
3
```

## Approach

### 1. Dynamic Programming Approach (Optimized Solution)
This approach uses **Dynamic Programming (DP)** to compute the maximum number of moves from each cell.

1. **DP Table**: Initialize a 2D array `dp` of the same size as `grid`. Each cell `dp[i][j]` represents the maximum number of moves from `grid[i][j]`.
2. **Reverse Column Traversal**: Start from the second-last column and calculate the moves backward towards the first column.
3. **Move Validation**: For each cell, check the following cells only if they exist and are strictly greater:
   - Right cell
   - Right-up cell
   - Right-down cell
4. **Result Calculation**: The answer is the maximum value in the first column of the `dp` table, representing the longest path from any starting cell in the first column.

### Code Implementation

#### Python Code
```python
from typing import List

class Solution:
    def maxMoves(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        
        # DP table to store max moves for each cell
        dp = [[0] * n for _ in range(m)]
        
        # Start from the last column and work backwards
        for j in range(n - 2, -1, -1):  # start from the second-last column
            for i in range(m):
                # Check right, right-up, and right-down cells if they are strictly greater
                if i > 0 and grid[i][j] < grid[i - 1][j + 1]:
                    dp[i][j] = max(dp[i][j], 1 + dp[i - 1][j + 1])
                if grid[i][j] < grid[i][j + 1]:
                    dp[i][j] = max(dp[i][j], 1 + dp[i][j + 1])
                if i < m - 1 and grid[i][j] < grid[i + 1][j + 1]:
                    dp[i][j] = max(dp[i][j], 1 + dp[i + 1][j + 1])
        
        # The answer is the maximum value in the first column
        return max(dp[i][0] for i in range(m))
```

#### Java Code
```java
class Solution {
    public int maxMoves(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp = new int[m][n];

        for (int j = n - 2; j >= 0; j--) {
            for (int i = 0; i < m; i++) {
                if (i > 0 && grid[i][j] < grid[i - 1][j + 1]) {
                    dp[i][j] = Math.max(dp[i][j], 1 + dp[i - 1][j + 1]);
                }
                if (grid[i][j] < grid[i][j + 1]) {
                    dp[i][j] = Math.max(dp[i][j], 1 + dp[i][j + 1]);
                }
                if (i < m - 1 && grid[i][j] < grid[i + 1][j + 1]) {
                    dp[i][j] = Math.max(dp[i][j], 1 + dp[i + 1][j + 1]);
                }
            }
        }
        int maxMoves = 0;
        for (int i = 0; i < m; i++) {
            maxMoves = Math.max(maxMoves, dp[i][0]);
        }
        return maxMoves;
    }
}
```

### Complexity Analysis
- **Time Complexity**: \(O(m \times n)\), where `m` is the number of rows and `n` is the number of columns, as each cell is processed once.
- **Space Complexity**: \(O(m \times n)\) for the DP table.

## Edge Cases
1. **Single Row or Column**: If there’s only one row or one column, the maximum moves are limited to adjacent cells.
2. **No Valid Moves**: If all values in each row are equal or decrease, no moves are possible.
3. **Uniform Grid**: If all cells contain the same number, the function should return `0` as no strictly increasing moves are possible.

## References
- [LeetCode Problem Discussion](https://leetcode.com/problems/maximum-number-of-moves-in-a-grid/)
  
--- 
