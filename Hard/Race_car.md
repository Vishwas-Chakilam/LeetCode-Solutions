# 818. Race Car

## Problem Statement
You are driving a **race car** that has `3` possible commands:
- `'A'` (Accelerate): Moves the car forward by the current speed. The speed doubles after accelerating.
- `'R'` (Reverse): Reverses the direction and resets speed to `1` (if positive) or `-1` (if negative).

Given a target position `target`, return the **minimum number of instructions** needed to reach it.

## Example
### Input 1:
```plaintext
Input: target = 3
Output: 2
Explanation: "AA" (Accelerate twice to reach 3)
```

### Input 2:
```plaintext
Input: target = 6
Output: 5
Explanation: "AAARA"
1. "AA" -> Moves to 3
2. "R" -> Reverse direction
3. "A" -> Moves to 2
4. "R" -> Reverse direction
5. "A" -> Moves to 6
```

## Approach
### **Breadth-First Search (BFS)**
1. Start from position `0` with speed `1`.
2. Use a queue to track `(position, speed, moves)`, where:
   - `'A'` results in `(pos + speed, speed * 2, moves + 1)`.
   - `'R'` results in `(pos, -1 if speed > 0 else 1, moves + 1)`.
3. Use a set to track visited `(position, speed)` states to avoid redundant work.
4. Perform BFS until reaching `target`.

## Complexity Analysis
- **Time Complexity:** `O(log target)`, since each acceleration doubles speed, reducing the search space.
- **Space Complexity:** `O(log target)`, due to queue and visited set.

## Code Implementation
```python
from collections import deque

def racecar(target):
    queue = deque([(0, 1, 0)])  # (position, speed, moves)
    visited = set((0, 1))
    
    while queue:
        pos, speed, moves = queue.popleft()
        
        if pos == target:
            return moves
        
        # Accelerate
        next_pos, next_speed = pos + speed, speed * 2
        if (next_pos, next_speed) not in visited:
            visited.add((next_pos, next_speed))
            queue.append((next_pos, next_speed, moves + 1))
        
        # Reverse
        rev_speed = -1 if speed > 0 else 1
        if (pos, rev_speed) not in visited:
            visited.add((pos, rev_speed))
            queue.append((pos, rev_speed, moves + 1))
```

## Edge Cases Considered
- Target is `1` (minimal input).
- Large `target` values.
- Cases where reversing is necessary before accelerating.

## Alternative Approaches
### **Dynamic Programming (DP)**
- Store the minimum moves for each position up to `target`.
- Requires recursion and memoization but has `O(n log n)` complexity.

## Conclusion
This problem is best solved using **BFS** since it guarantees the shortest path to the target. Alternative DP solutions exist but are harder to implement efficiently.
