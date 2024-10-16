# Problem: Longest Happy String

## 1. Problem Statement

A string is called **happy** if it does not contain any of the substrings `"aa"`, `"bb"`, or `"cc"`. 

Given three integers `a`, `b`, and `c`, representing the number of letters `'a'`, `'b'`, and `'c'` you have, return **any longest possible happy string**. If there is no such string, return the empty string `""`.

---

## 2. Test Cases

### Test Case 1:
```python
Input: a = 1, b = 1, c = 7
Output: "ccbccacc"
```

### Test Case 2:
```python
Input: a = 2, b = 2, c = 1
Output: "aabbc"
```

### Test Case 3:
```python
Input: a = 7, b = 1, c = 0
Output: "aabaa"
```

### Test Case 4:
```python
Input: a = 0, b = 0, c = 0
Output: ""
```

### Test Case 5:
```python
Input: a = 5, b = 5, c = 5
Output: "aabbcc"
```

---

## 3. Approach

### 3a. Greedy Approach with Max-Heap (Priority Queue)

The key idea is to greedily add the character with the highest frequency to the string. However, we must avoid adding more than two consecutive identical characters, so after adding two of the most frequent character, we switch to the next most frequent one.

#### Steps:
1. **Heap Construction**: Use a max-heap to store character frequencies in decreasing order.
2. **Greedy Construction**: At each step, pick the most frequent character from the heap and add it to the result string.
3. **Avoid Overuse**: Ensure that no three consecutive characters are the same by switching between the most frequent characters.

#### Time Complexity:
- **O(n log 3)** where `n` is the total number of characters (`a + b + c`) since for each character, we perform a log operation on the heap with a maximum size of 3.

#### Space Complexity:
- **O(1)** extra space apart from the input.

#### Python Code:
```python
import heapq

def longestHappyString(a, b, c):
    heap = []
    if a > 0: heapq.heappush(heap, (-a, 'a'))
    if b > 0: heapq.heappush(heap, (-b, 'b'))
    if c > 0: heapq.heappush(heap, (-c, 'c'))
    
    result = []
    
    while heap:
        freq1, char1 = heapq.heappop(heap)
        
        if len(result) >= 2 and result[-1] == result[-2] == char1:
            if not heap:
                break
            freq2, char2 = heapq.heappop(heap)
            result.append(char2)
            freq2 += 1
            if freq2 != 0:
                heapq.heappush(heap, (freq2, char2))
            heapq.heappush(heap, (freq1, char1))
        else:
            result.append(char1)
            freq1 += 1
            if freq1 != 0:
                heapq.heappush(heap, (freq1, char1))
    
    return ''.join(result)
```

---

### 3b. Greedy Approach with Sorting

This approach involves sorting the counts of the characters dynamically after each addition. We keep track of the three character counts (`a`, `b`, and `c`) and repeatedly add the character with the highest remaining count, ensuring no three consecutive characters are the same.

#### Steps:
1. **Sorting the Characters**: At each step, sort the counts dynamically to find the character with the highest remaining count.
2. **Check for Consecutive Characters**: If the most frequent character has already been used twice consecutively, choose the second most frequent character.

#### Time Complexity:
- **O(n log 3)**, as we need to sort the characters dynamically at each step, which results in log operations.

#### Space Complexity:
- **O(1)** extra space apart from the input.

#### Python Code:
```python
def longestHappyString(a, b, c):
    result = []
    while True:
        chars = [('a', a), ('b', b), ('c', c)]
        chars.sort(key=lambda x: -x[1])
        
        if len(result) >= 2 and result[-1] == result[-2] == chars[0][0]:
            if chars[1][1] == 0:
                break
            result.append(chars[1][0])
            if chars[1][0] == 'a': a -= 1
            elif chars[1][0] == 'b': b -= 1
            else: c -= 1
        else:
            if chars[0][1] == 0:
                break
            result.append(chars[0][0])
            if chars[0][0] == 'a': a -= 1
            elif chars[0][0] == 'b': b -= 1
            else: c -= 1
            
    return ''.join(result)
```

---

## 4. Edge Cases

- **Zero counts for all characters**: The algorithm should return an empty string.
- **One count significantly larger**: If one count is much larger than the others, the solution must still maintain a happy string by limiting consecutive identical characters.
- **One or more characters missing**: Handle cases where `a`, `b`, or `c` is zero.

---

## 5. Code Implementation in Other Languages

### Java Implementation (Greedy + Priority Queue):
```java
import java.util.PriorityQueue;

public class Solution {
    public String longestDiverseString(int a, int b, int c) {
        PriorityQueue<Pair> pq = new PriorityQueue<>((x, y) -> y.count - x.count);
        if (a > 0) pq.offer(new Pair('a', a));
        if (b > 0) pq.offer(new Pair('b', b));
        if (c > 0) pq.offer(new Pair('c', c));
        
        StringBuilder sb = new StringBuilder();
        
        while (!pq.isEmpty()) {
            Pair first = pq.poll();
            
            if (sb.length() >= 2 && sb.charAt(sb.length() - 1) == first.ch && sb.charAt(sb.length() - 2) == first.ch) {
                if (pq.isEmpty()) break;
                
                Pair second = pq.poll();
                sb.append(second.ch);
                second.count--;
                
                if (second.count > 0) {
                    pq.offer(second);
                }
                pq.offer(first);
            } else {
                sb.append(first.ch);
                first.count--;
                
                if (first.count > 0) {
                    pq.offer(first);
                }
            }
        }
        
        return sb.toString();
    }
    
    class Pair {
        char ch;
        int count;
        Pair(char ch, int count) {
            this.ch = ch;
            this.count = count;
        }
    }
}
```

---

## 6. References

- [LeetCode Problem](https://leetcode.com/problems/longest-happy-string/)
  
---
