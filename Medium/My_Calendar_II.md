# 731. My Calendar II

## 1. Problem Statement

Implement a `MyCalendarTwo` class to manage calendar events with double bookings allowed. A **double booking** happens when two events have some non-empty intersection (i.e., some moment is common to both). You want to ensure that no triple booking occurs.

Your `MyCalendarTwo` class has two methods:

- `book(int start, int end)`: Adds a new event if it can be added without causing a **triple booking**.

Return `true` if the event can be added, otherwise return `false`.

### Example:

```python
MyCalendarTwo();
myCalendar.book(10, 20); // returns True
myCalendar.book(50, 60); // returns True
myCalendar.book(10, 40); // returns True
myCalendar.book(5, 15);  // returns False
myCalendar.book(5, 10);  // returns True
myCalendar.book(25, 55); // returns True
```

### Constraints:
- `0 <= start < end <= 10^9`
- At most 1000 calls will be made to `book`.

---

## 2. Test Cases

### Test Case 1:
```python
myCalendar = MyCalendarTwo()
assert myCalendar.book(10, 20) == True
assert myCalendar.book(50, 60) == True
assert myCalendar.book(10, 40) == True
assert myCalendar.book(5, 15) == False
assert myCalendar.book(5, 10) == True
assert myCalendar.book(25, 55) == True
```

### Test Case 2:
```python
myCalendar = MyCalendarTwo()
assert myCalendar.book(1, 10) == True
assert myCalendar.book(5, 15) == True
assert myCalendar.book(5, 10) == False
assert myCalendar.book(20, 30) == True
```

---

## 3. Approach

### 3a. Brute Force Approach

We can maintain a list of all booked events and iterate over them to check for intersections. If adding an event causes a triple booking (i.e., it intersects with more than one existing event at the same time), we reject the booking.

#### Time Complexity:
- **Time**: O(n^2), where `n` is the number of booked events.
- **Space**: O(n), where `n` is the number of events stored.

#### Code Implementation (Python):
```python
class MyCalendarTwo:

    def __init__(self):
        self.bookings = []
        self.overlaps = []

    def book(self, start: int, end: int) -> bool:
        for os, oe in self.overlaps:
            if start < oe and end > os:
                return False
        
        for bs, be in self.bookings:
            if start < be and end > bs:
                self.overlaps.append((max(start, bs), min(end, be)))
        
        self.bookings.append((start, end))
        return True
```

### 3b. Optimized Approach (Segment Tree Approach)

For an optimized approach, we can use a **Segment Tree** or **Balanced Binary Tree** to efficiently handle overlapping intervals. This structure allows us to keep track of event counts over time ranges and prevent triple bookings by keeping track of ranges where there are already two bookings.

#### Time Complexity:
- **Time**: O(n log n) for insertion and checking.
- **Space**: O(n) for storing event ranges.

---

## 4. Edge Cases

- **Events with no overlap**: Events that are non-overlapping should always return `true` and be successfully booked.
- **Events that cause triple bookings**: If adding an event would cause three events to overlap at the same time, return `false`.
- **Boundary events**: Events that end exactly when another starts should be handled correctly as non-overlapping.

---

## 5. References

- **Interval Trees**: [GeeksforGeeks - Segment Tree for Event Overlaps](https://www.geeksforgeeks.org/interval-tree/)
- **LeetCode Problem**: [My Calendar II](https://leetcode.com/problems/my-calendar-ii/)

---
