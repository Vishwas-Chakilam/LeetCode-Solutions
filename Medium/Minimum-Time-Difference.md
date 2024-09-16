# Minimum Time Difference

## Description

Given a list of `timePoints` in the format "HH:MM", find the minimum difference in minutes between any two time points in the list.

**Example:**

**Input:**
```python
timePoints = ["23:59", "00:00"]
```

**Output:**
```python
1
```

**Explanation:**
The difference between "23:59" and "00:00" is exactly 1 minute.

---

## Solution

### Approach

The key to solving this problem efficiently is recognizing that there are only **1440 minutes** in a day (24 hours * 60 minutes). Therefore, a brute-force comparison between all pairs can be avoided by:

1. **Convert all time points to minutes:** First, we convert each time from "HH:MM" format into the total number of minutes from `00:00`.
2. **Sort the time points:** Sorting helps easily compare consecutive time points.
3. **Handle the circular nature of the clock:** To handle the difference between the smallest and largest times (e.g., `23:59` and `00:00`), compute the circular difference.

### Code

```python
def findMinDifference(timePoints):
    def time_to_minutes(time):
        hours, minutes = map(int, time.split(":"))
        return hours * 60 + minutes

    # Convert all time points to minutes
    minutes_list = [time_to_minutes(time) for time in timePoints]
    
    # Sort the list of times in minutes
    minutes_list.sort()

    # Initialize the minimum difference as large as possible
    min_diff = float('inf')

    # Compute the differences between consecutive times
    for i in range(1, len(minutes_list)):
        min_diff = min(min_diff, minutes_list[i] - minutes_list[i - 1])

    # Circular difference between the last and first time
    min_diff = min(min_diff, 1440 + minutes_list[0] - minutes_list[-1])

    return min_diff
```

### Complexity Analysis

- **Time Complexity:** O(n log n), where `n` is the number of time points. Sorting takes O(n log n), and comparing consecutive times takes O(n).
- **Space Complexity:** O(n), since we store all the time points converted to minutes.

---

## Edge Cases

- **Duplicate Times:** If the same time appears twice, the minimum difference is `0`.
- **Handling Midnight:** The solution correctly handles cases where times like `23:59` and `00:00` are compared by considering the circular difference.

---

## Additional Notes

- The problem becomes straightforward after converting times to minutes and sorting. The key challenge is efficiently handling the circular nature of the clock, which is addressed by computing the difference between the last and first times.

---

## References

**LeetCode Problem Link:** [Minimum Time Difference](https://leetcode.com/problems/minimum-time-difference/)
