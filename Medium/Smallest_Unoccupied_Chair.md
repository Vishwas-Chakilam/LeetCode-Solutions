# 1942. The Number of the Smallest Unoccupied Chair

## 1. Problem Statement

You are given a 2D integer array `times` where `times[i] = [arrival_i, leaving_i]` indicates the arrival and leaving times of the i-th friend. All friends are initially standing in a queue, sorted by their arrival times.

There are `n` chairs arranged in a line and all chairs are initially empty. When a friend arrives, they sit on the closest available chair. When a friend leaves, their chair becomes available again.

You are also given an integer `targetFriend`, and your task is to find the chair that the target friend will sit on.

### Example 1:
```python
Input: times = [[1,4],[2,3],[4,6]], targetFriend = 1
Output: 1
Explanation:
- Friend 0 arrives at time 1 and sits on chair 0.
- Friend 1 arrives at time 2 and sits on chair 1.
- Friend 1 leaves at time 3, and chair 1 becomes free.
- Friend 2 arrives at time 4 and sits on chair 1, as it’s the closest to the entrance.
Thus, friend 1 sits on chair 1.
```

### Example 2:
```python
Input: times = [[3,10],[1,5],[2,6]], targetFriend = 0
Output: 0
Explanation:
Friend 0 sits on chair 0.
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: times = [[1,4],[2,3],[4,6]], targetFriend = 1
Output: 1
```

### Test Case 2:
```python
Input: times = [[3,10],[1,5],[2,6]], targetFriend = 0
Output: 0
```

### Test Case 3:
```python
Input: times = [[1,2],[2,3],[3,4]], targetFriend = 2
Output: 0
Explanation: The first friend leaves before the second arrives, making chair 0 available again.
```

---

## 3. Approach

### 3a. Brute Force with Time and Space Complexity

- **Brute force**: We can iterate through each friend’s arrival time and check all available chairs to assign the smallest numbered chair. After a friend leaves, their chair becomes available again.
- **Time Complexity**: O(n^2), where n is the number of friends. This is because for each friend, we check all available chairs.
- **Space Complexity**: O(n), where n is the number of friends, for storing chair status.

### 3b. Optimized Approach with Priority Queues

We can use a **priority queue (min-heap)** to efficiently manage the allocation of chairs:

- Sort friends by their arrival time.
- Use a heap to track empty chairs.
- Use another heap to track chairs that will be freed when a friend leaves.
- For each arriving friend, assign the smallest available chair.
- When a friend leaves, the chair they occupied becomes available and is pushed back to the heap.

#### Time Complexity:
- **O(n log n)** due to sorting the friends by arrival time and managing the priority queues.

#### Space Complexity:
- **O(n)** for maintaining the priority queues.

---

## 4. Code Implementation

### Python Implementation:
```python
import heapq

class Solution:
    def smallestChair(self, times: List[List[int]], targetFriend: int) -> int:

        order = sorted(range(len(times)), key = lambda x: times[x][0])  # Sort friends by arrival time
        emptySeats, takenSeats = list(range(len(times))), []            # Initialize seats and heap for tracking available and taken seats

        for i in order:                                                 # Loop over sorted friends
            ar, lv = times[i]

            # Free up seats from friends who have already left
            while takenSeats and takenSeats[0][0] <= ar:
                heapq.heappush(emptySeats, heapq.heappop(takenSeats)[1])

            # Assign the next smallest available seat
            seat = heapq.heappop(emptySeats)                            

            # If this is the target friend, return their seat number
            if i == targetFriend: return seat

            # Add the seat to the heap of taken seats with the friend's leaving time
            heapq.heappush(takenSeats,(lv, seat))                             
```

### Java Implementation:
```java
import java.util.*;

public class Solution {
    public int smallestChair(int[][] times, int targetFriend) {
        int n = times.length;
        List<int[]> events = new ArrayList<>();

        // Collect arrival and leaving events
        for (int i = 0; i < n; i++) {
            events.add(new int[] {times[i][0], i, 1}); // 1 for arrival
            events.add(new int[] {times[i][1], i, -1}); // -1 for leaving
        }

        Collections.sort(events, (a, b) -> a[0] - b[0]); // Sort events by time

        PriorityQueue<Integer> freeChairs = new PriorityQueue<>();
        for (int i = 0; i < n; i++) freeChairs.add(i);
        int[] chairAssignment = new int[n];

        for (int[] event : events) {
            int time = event[0], friend = event[1], type = event[2];

            if (type == 1) { // Arrival
                int chair = freeChairs.poll();
                chairAssignment[friend] = chair;
                if (friend == targetFriend) return chair;
            } else { // Leaving
                freeChairs.add(chairAssignment[friend]);
            }
        }

        return -1;
    }
}
```

---

## 5. Edge Cases

- **Single friend**: The result will always be `0` because there is only one chair.
- **All friends arrive and leave at different times**: Each friend will sit in order of arrival on the smallest chair.
- **Multiple friends arriving at the same time**: The closest available chairs will be assigned in order of their index.

---

## 6. References

- **LeetCode Problem**: [1942. The Number of the Smallest Unoccupied Chair](https://leetcode.com/problems/the-smallest-chair/)

---
