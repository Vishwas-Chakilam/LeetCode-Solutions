# 2491. Divide Players Into Teams of Equal Skill

## 1. Problem Statement

You are given a list of integers `skills`, where each integer represents the skill level of a player. Your task is to divide the players into teams of two such that the total skill of each team is equal.

If possible, return the total sum of all team chemistry. The chemistry of a team with skill levels `a` and `b` is `a * b`. If it is impossible to divide players in such a way, return `-1`.

### Example 1:
```python
Input: skills = [3,2,5,1,3,4]
Output: 22
Explanation: The players are divided into the teams: (1, 5), (2, 4), (3, 3). The chemistry of each team is 1 * 5 + 2 * 4 + 3 * 3 = 22.
```

### Example 2:
```python
Input: skills = [3,4,3,4]
Output: -1
Explanation: It is impossible to form teams such that each team has the same total skill.
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: skills = [1, 1, 2, 2]
Output: 2
Explanation: Teams can be formed as (1, 2) and (1, 2), giving a total chemistry of 1 * 2 + 1 * 2 = 2.
```

### Test Case 2:
```python
Input: skills = [10, 10, 20, 20, 30, 30]
Output: 1400
Explanation: Teams formed as (10, 30), (10, 30), (20, 20) give chemistry 10 * 30 + 10 * 30 + 20 * 20 = 1400.
```

### Test Case 3:
```python
Input: skills = [5, 3, 8, 3]
Output: -1
Explanation: It's impossible to form valid teams with equal skill.
```

---

## 3. Approach

### 3a. Brute Force Approach:
- Try all possible pairs of players and calculate their sum.
- For every possible pairing, check if all pairs have the same skill sum.
- If they do, compute the total chemistry; otherwise, return `-1`.

#### Time Complexity:
- **O(n^2)**, iterating through all pairs.

#### Space Complexity:
- **O(1)**, no extra data structures required.

### 3b. Optimized Approach (Sorting and Two Pointers):
- Sort the array of skills.
- Use two pointers: one starting at the beginning of the sorted array and the other at the end.
- Pair the players with the smallest and largest skills.
- If the sum of skills in any pair differs, return `-1`.
- Otherwise, compute the chemistry for each valid pair.

#### Time Complexity:
- **O(n log n)** for sorting the array.

#### Space Complexity:
- **O(1)** extra space used for variables.

---

## 4. Code Implementation

### Python Implementation:
```python
def dividePlayers(skills):
    skills.sort()
    n = len(skills)
    total_chemistry = 0
    expected_sum = skills[0] + skills[-1]

    for i in range(n // 2):
        if skills[i] + skills[n - 1 - i] != expected_sum:
            return -1
        total_chemistry += skills[i] * skills[n - 1 - i]

    return total_chemistry

# Example
skills = [3, 2, 5, 1, 3, 4]
print(dividePlayers(skills))  # Output: 22
```

### Java Implementation:
```java
import java.util.Arrays;

public class Solution {
    public int dividePlayers(int[] skills) {
        Arrays.sort(skills);
        int n = skills.length;
        int totalChemistry = 0;
        int expectedSum = skills[0] + skills[n - 1];

        for (int i = 0; i < n / 2; i++) {
            if (skills[i] + skills[n - 1 - i] != expectedSum) {
                return -1;
            }
            totalChemistry += skills[i] * skills[n - 1 - i];
        }

        return totalChemistry;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] skills = {3, 2, 5, 1, 3, 4};
        System.out.println(solution.dividePlayers(skills));  // Output: 22
    }
}
```

---

## 5. Edge Cases
- **Odd number of players**: Return `-1` because it is impossible to form teams.
- **Players with equal skill levels**: Check if all pairs sum up to the same value.
- **No valid teams**: Return `-1` if teams cannot be formed with equal skills.

---

## 6. References
- **LeetCode Problem**: [2491. Divide Players Into Teams of Equal Skill](https://leetcode.com/problems/divide-players-into-teams-of-equal-skill/)
---
