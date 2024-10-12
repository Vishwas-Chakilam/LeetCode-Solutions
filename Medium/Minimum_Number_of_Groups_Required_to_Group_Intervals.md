# Problem: Minimum Number of Groups Required to Group Intervals

## 1. Problem Statement

Given a list of intervals, where each interval represents a start time and an end time `[start, end]`, you need to find the minimum number of groups required so that no two intervals overlap in the same group. A group can have overlapping intervals, but no two intervals in a single group should overlap.

### Example 1:
```python
Input: intervals = [[1, 3], [2, 4], [6, 8], [5, 7]]
Output: 2
Explanation: 
- One group can contain intervals [1, 3] and [6, 8] (non-overlapping).
- Another group can contain intervals [2, 4] and [5, 7] (non-overlapping).
Thus, the minimum number of groups is 2.
```

### Example 2:
```python
Input: intervals = [[1, 5], [2, 6], [8, 10], [9, 12]]
Output: 2
Explanation: 
- One group can contain intervals [1, 5] and [8, 10].
- Another group can contain intervals [2, 6] and [9, 12].
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: intervals = [[1, 3], [2, 4], [6, 8], [5, 7]]
Output: 2
```

### Test Case 2:
```python
Input: intervals = [[1, 5], [2, 6], [8, 10], [9, 12]]
Output: 2
```

### Test Case 3:
```python
Input: intervals = [[1, 10], [2, 3], [4, 5], [6, 7], [8, 9]]
Output: 1
Explanation: All intervals can fit into one group without overlapping.
```

---

## 3. Approach

### 3a. Brute Force with Time and Space Complexity

- **Brute force**: One can check all possible ways to group intervals by trying every combination. However, this would be inefficient for larger inputs and would require checking each pair of intervals for overlap.
- **Time Complexity**: O(n^2) due to checking every pair of intervals for overlaps.
- **Space Complexity**: O(n) for storing intervals and groups.

### 3b. Optimized Approach with Events (Sweep Line Algorithm)

The optimal approach uses a **sweep line algorithm** where we break each interval into two events: a **start event** and an **end event**. We sort these events in time order, incrementing the count of active intervals when we encounter a start event and decrementing it when we encounter an end event. The maximum number of active intervals at any point gives the number of groups needed.

#### Time Complexity:
- **O(n log n)** due to sorting the events.

#### Space Complexity:
- **O(n)** for storing the events.

---

## 4. Code Implementation

### Python Implementation:
```python
def minGroups(intervals):
    events = []
    
    # Break intervals into start and end events
    for start, end in intervals:
        events.append((start, 'start'))
        events.append((end + 1, 'end'))  # We add 1 to the end time to handle non-overlapping intervals properly
    
    # Sort events: start events before end events when at the same time
    events.sort()
    
    active_intervals = 0
    max_active = 0
    
    # Sweep through the events
    for time, event_type in events:
        if event_type == 'start':
            active_intervals += 1
            max_active = max(max_active, active_intervals)  # Update max active intervals
        else:
            active_intervals -= 1
    
    return max_active
```

### Java Implementation:
```java
import java.util.*;

public class Solution {
    public int minGroups(int[][] intervals) {
        List<int[]> events = new ArrayList<>();

        // Break intervals into start and end events
        for (int[] interval : intervals) {
            events.add(new int[]{interval[0], 1}); // Start event
            events.add(new int[]{interval[1] + 1, -1}); // End event
        }

        // Sort events: start events before end events when at the same time
        Collections.sort(events, (a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);

        int activeIntervals = 0, maxActive = 0;

        // Sweep through the events
        for (int[] event : events) {
            activeIntervals += event[1]; // Increment or decrement based on event type
            maxActive = Math.max(maxActive, activeIntervals); // Update max active intervals
        }

        return maxActive;
    }
}
```

---

## 5. Edge Cases

- **All intervals overlap**: The output will be equal to the number of intervals, as each interval requires its own group.
- **No overlap between intervals**: The output will be `1`, as all intervals can fit into a single group.
- **Single interval**: The output will be `1`, as only one group is required.

---

## 6. References

- **LeetCode Problem**: [Minimum Number of Groups Required to Group Intervals](https://leetcode.com/problems/minimum-number-of-groups-required-to-group-intervals/)

---
