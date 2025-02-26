# Nim Game Problem (LeetCode 292)

## Problem Statement
This repository contains a Java solution for solving the **Nim Game** problem from LeetCode.

## Solution Approach

### Problem Description
You are playing the Nim Game with the following rules:
- There is a heap of `n` stones.
- Each player takes turns to remove 1 to 3 stones.
- The player who removes the last stone wins the game.
- You play first and need to determine if you can win.

### Approach
- If `n` is a multiple of 4, you will always lose if your opponent plays optimally.
- Otherwise, you can force a win by choosing a move that leaves your opponent with a multiple of 4.

## Code Implementation
```java
class Solution {
    public boolean canWinNim(int n) {
        if (n % 4 == 0) return false;
        else return true;
    }
}
```

## Usage
1. Clone this repository:
   ```sh
   git clone https://github.com/Vishwas-Chakilam/LeetCode-Solutions.git
   ```
2. Run the function in a Java environment.

## Example
```java
Solution sol = new Solution();
System.out.println(sol.canWinNim(4));  // Output: false
System.out.println(sol.canWinNim(5));  // Output: true
```

## Contributions
Feel free to submit issues and pull requests to improve the implementation!

## License
This project is open-source and available under the MIT License.
