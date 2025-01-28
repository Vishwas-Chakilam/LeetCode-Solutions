# Maximum Depth of Binary Tree

## Problem Description
The **Maximum Depth of Binary Tree** is a common problem in tree traversal algorithms. The goal is to determine the maximum depth (or height) of a binary tree, which is defined as the number of nodes along the longest path from the root node to the farthest leaf node.

### Problem Statement
Given the `root` of a binary tree, return its maximum depth.

---

### Example

#### Input:
```
       3
      / \
     9  20
        /  \
       15   7
```

#### Output:
```
3
```

#### Explanation:
- The longest path is `3 -> 20 -> 15` or `3 -> 20 -> 7`.
- Both paths have 3 nodes, so the maximum depth is `3`.

---

## Solution Explanation

### Approach
We use **recursion** to solve this problem. The maximum depth of a binary tree can be calculated using the following logic:
1. If the tree is empty (`root == None`), the depth is `0`.
2. Otherwise:
   - Recursively find the maximum depth of the left and right subtrees.
   - The depth of the tree is the greater of the two depths, plus 1 (to account for the current node).

### Algorithm (Recursive):
1. Base case: If the node is `None`, return `0`.
2. Recursive case:
   - Compute the depth of the left and right subtrees.
   - Return `max(left_depth, right_depth) + 1`.

### Time Complexity:
- **O(n)**: We visit each node exactly once.

### Space Complexity:
- **O(h)**: The recursive call stack can go as deep as the height of the tree (`h`), which can be `O(n)` in the worst case for a skewed tree or `O(log n)` for a balanced tree.

---

## Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 0
        else:
            # Recursively calculate the depth of the left and right subtrees
            left_depth = self.maxDepth(root.left)
            right_depth = self.maxDepth(root.right)
            # Return the maximum depth plus one for the root
            return max(left_depth, right_depth) + 1
```

---

## Example Walkthrough

Consider the tree:

```
       1
      / \
     2   3
    / \
   4   5
```

1. Start at the root node (`1`).
2. Recursively calculate the depth of the left subtree (`2`):
   - Depth of subtree rooted at `4` = `1` (leaf node).
   - Depth of subtree rooted at `5` = `1` (leaf node).
   - Depth of subtree rooted at `2` = `1 + max(1, 1) = 2`.
3. Recursively calculate the depth of the right subtree (`3`) = `1` (leaf node).
4. Depth of the entire tree = `1 + max(2, 1) = 3`.

---

## Alternative Approaches

### Iterative Approach (Using BFS):
We can use a level-order traversal (BFS) to calculate the depth. In each iteration, we process all nodes at the current level and increment the depth counter.

```python
from collections import deque

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        queue = deque([root])
        depth = 0
        
        while queue:
            depth += 1
            for _ in range(len(queue)):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return depth
```
---

## Resources
- [LeetCode Problem #104 - Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [Binary Tree Basics](https://en.wikipedia.org/wiki/Binary_tree)

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for more details.

---

## Author
[Vishwas Chakilam](https://github.com/Vishwas-Chakilam)  
Transforming Data into Actionable Insights and Innovative Solutions 🚀

---
