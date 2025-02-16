# **Subrectangle Queries**  

## **Problem Statement**  
The problem requires implementing a class `SubrectangleQueries`, which allows performing the following operations on a 2D grid (rectangle):  

1. **Update a subrectangle**: Modify all elements within a given subrectangle to a new value.  
2. **Retrieve a value**: Get the value of an element at a specific row and column.  

## **Solution Explanation**  
The solution efficiently modifies and queries a given 2D grid using a straightforward approach.  

### **Approach**  
- **Initialization**: Store the given rectangle in `self.s`.  
- **Updating Subrectangle**:
  - Iterate over the specified subrectangle and update all elements to `newValue`.  
- **Retrieving a Value**:
  - Simply return the value at the specified row and column.  

---

## **Code Implementation**  
```python
from typing import List

class SubrectangleQueries:
    def __init__(self, rectangle: List[List[int]]):
        self.s = rectangle  # Store the rectangle

    def updateSubrectangle(self, row1: int, col1: int, row2: int, col2: int, newValue: int) -> None:
        """Updates all elements in the given subrectangle to newValue."""
        for i in range(row1, row2 + 1):
            for j in range(col1, col2 + 1):
                self.s[i][j] = newValue

    def getValue(self, row: int, col: int) -> int:
        """Returns the value at the given row and column."""
        return self.s[row][col]

# Example Usage:
# obj = SubrectangleQueries(rectangle)
# obj.updateSubrectangle(row1, col1, row2, col2, newValue)
# param_2 = obj.getValue(row, col)
```

---

## **Complexity Analysis**  
- **Initialization (`__init__`)**: \( O(1) \) (just storing a reference).  
- **Updating Subrectangle (`updateSubrectangle`)**: \( O((row2 - row1 + 1) \times (col2 - col1 + 1)) \) (modifies each element in the range).  
- **Retrieving Value (`getValue`)**: \( O(1) \) (direct access).  

---

## **Example Usage**  
```python
rectangle = [
    [1, 2, 1],
    [4, 3, 4],
    [3, 2, 1],
    [1, 1, 1]
]

obj = SubrectangleQueries(rectangle)

# Update subrectangle (1,1) to (2,2) with value 5
obj.updateSubrectangle(1, 1, 2, 2, 5)

# Retrieve values
print(obj.getValue(1, 1))  # Output: 5
print(obj.getValue(2, 2))  # Output: 5
print(obj.getValue(0, 2))  # Output: 1 (unchanged)
```

---

## **Edge Cases Considered**  
- Updating an entire rectangle  
- Updating a single cell  
- Checking unchanged values after an update  
- Retrieving values at boundary indices  



## **Why This Solution Works Well?**  
✅ **Simple & Intuitive**: Uses basic loops for updates and direct indexing for retrieval.  
✅ **Efficient for Queries**: `getValue()` runs in \( O(1) \), making frequent queries fast.  
✅ **Easy to Understand & Implement**  

---
