# Problem Statement

Given a `m x n` binary matrix `matrix`, count the number of square submatrices that have all ones. A square submatrix is a submatrix where the number of rows is equal to the number of columns, and all elements within the square are `1`.

**Example:**

Input:
```
matrix = [
  [0,1,1,1],
  [1,1,1,1],
  [0,1,1,1]
]
```
Output:
```
15
```

### Test Cases

1. **Example Case**:
   ```python
   Input: matrix = [[0,1,1,1],[1,1,1,1],[0,1,1,1]]
   Output: 15
   ```
   
2. **Single Row with All Ones**:
   ```python
   Input: matrix = [[1,1,1,1]]
   Output: 4
   ```
   
3. **Single Column with All Ones**:
   ```python
   Input: matrix = [[1],[1],[1]]
   Output: 3
   ```
   
4. **Matrix with All Zeros**:
   ```python
   Input: matrix = [[0,0],[0,0]]
   Output: 0
   ```
   
5. **Single Element Matrix**:
   ```python
   Input: matrix = [[1]]
   Output: 1
   ```
   
6. **Mixed Zeros and Ones**:
   ```python
   Input: matrix = [[1,0],[1,1]]
   Output: 3
   ```

### Approach

1. **Dynamic Programming (DP)**:
   - Define a DP matrix `dp` where `dp[i][j]` represents the side length of the largest square submatrix with all ones that ends at position `(i, j)`.
   - If `matrix[i][j]` is `1`, then `dp[i][j]` is the minimum of the values directly above, to the left, and diagonally up-left, plus one.
   - This relationship works because for a square to end at `(i, j)`, all squares above, left, and top-left must also form squares.
   
2. **Time Complexity**:
   - The solution iterates over each cell, so the time complexity is **O(m * n)**, where `m` is the number of rows and `n` is the number of columns.

3. **Space Complexity**:
   - We can use the `matrix` itself to store `dp` values, reducing space complexity to **O(1)**, or alternatively, use an **O(m * n)** auxiliary `dp` matrix.

### Code Implementation

#### Python Solution

```python
from typing import List

class Solution:
    def countSquares(self, matrix: List[List[int]]) -> int:
        m, n = len(matrix), len(matrix[0])
        total_squares = 0
        
        # Use the input matrix as DP table to save space
        for i in range(m):
            for j in range(n):
                # Update DP value if matrix[i][j] is 1 and it is not on the top row or left column
                if matrix[i][j] == 1 and i > 0 and j > 0:
                    matrix[i][j] = min(matrix[i-1][j], matrix[i][j-1], matrix[i-1][j-1]) + 1
                total_squares += matrix[i][j]
                
        return total_squares
```

### Explanation:

- **Initialize** `total_squares` as `0`.
- **Iterate through each cell**:
  - If the current cell `matrix[i][j]` is `1`, and it’s not on the first row or column, apply the DP formula.
  - Add `matrix[i][j]` to `total_squares` since it represents the count of squares ending at `(i, j)`.
  
- **Return** the `total_squares` as the result.

### Edge Cases

1. **All Zeros Matrix**: Should return `0` as there are no squares with ones.
2. **All Ones Matrix**: Should return a high count as each cell can form multiple squares.
3. **Matrix with a Single Row or Column**: The answer should be the count of `1`s since each represents a 1x1 square.
4. **Mixed Values**: The solution must handle both `0`s and `1`s, recognizing when to reset the potential for a square at a given cell.

### References

- Dynamic Programming fundamentals.
- Problem's [LeetCode page](https://leetcode.com/problems/count-square-submatrices-with-all-ones/) for additional insights and variations.

---
