# Find Elements in a Contaminated Binary Tree  

## Problem Statement  
This repository contains a Python solution for **Leetcode 1261: Find Elements in a Contaminated Binary Tree**.  
The problem involves recovering a binary tree where all node values were changed to `-1` and providing a function to check if a given target value exists in the recovered tree.

## Solution Approach  
- The tree is reconstructed by following the rules:
  - The root is set to `0`.
  - For each node with value `x`:  
    - The left child is assigned `2 * x + 1`.  
    - The right child is assigned `2 * x + 2`.  
- The values of all nodes are stored in a **set** for efficient lookup in `O(1)` time.

## Implementation  
### Class: `FindElements`  
- **`__init__(root: Optional[TreeNode])`**  
  - Recovers the tree and stores node values in a set.  
- **`recover(node: TreeNode, val: int)`**  
  - Recursively assigns correct values to nodes.  
- **`find(target: int) -> bool`**  
  - Checks if `target` exists in the recovered tree.  

## Code  
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class FindElements:

    def __init__(self, root: Optional[TreeNode]):
        self.values = set()
        self.recover(root, 0)

    def recover(self, node, val):
        if not node:
            return
        node.val = val
        self.values.add(val)
        self.recover(node.left, 2 * val + 1)
        self.recover(node.right, 2 * val + 2)

    def find(self, target: int) -> bool:
        return target in self.values

# Usage Example:
# obj = FindElements(root)
# result = obj.find(target)
```

## Complexity Analysis  
- **Tree Recovery (`__init__` and `recover`)**:  
  - **Time Complexity**: `O(N)`, where `N` is the number of nodes.  
  - **Space Complexity**: `O(N)`, as we store node values in a set.  
- **Find Operation (`find`)**:  
  - **Time Complexity**: `O(1)`, as set lookups are constant time.  

## Example Usage  
```python
from typing import Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# Constructing a contaminated tree
root = TreeNode(-1)
root.left = TreeNode(-1)
root.right = TreeNode(-1)

# Recovering and searching
obj = FindElements(root)
print(obj.find(1))  # Output: True or False depending on the tree structure
```

## License  
This project is open-source and available under the **MIT License**.

