# 432. All O` one Data Structure

## 1. Problem Statement

Design a data structure that supports the following operations in **O(1)** time:
1. `inc(String key)`: Increments the count of the string `key` by 1. If the `key` does not exist, insert it with count 1.
2. `dec(String key)`: Decrements the count of the string `key` by 1. If the count of `key` becomes 0, remove it.
3. `getMaxKey()`: Returns one of the keys with the maximum count.
4. `getMinKey()`: Returns one of the keys with the minimum count.

### Example:
```python
allOne = AllOne()
allOne.inc("apple")
allOne.inc("apple")
print(allOne.getMaxKey())  # Output: "apple"
print(allOne.getMinKey())  # Output: "apple"
allOne.inc("banana")
print(allOne.getMinKey())  # Output: "banana"
```

---

## 2. Test Cases

### Test Case 1:
```python
allOne = AllOne()
allOne.inc("key1")
allOne.inc("key2")
assert allOne.getMaxKey() == "key2" or "key1"
assert allOne.getMinKey() == "key2" or "key1"
allOne.dec("key1")
assert allOne.getMinKey() == "key1"
```

### Test Case 2:
```python
allOne = AllOne()
assert allOne.getMaxKey() == ""
assert allOne.getMinKey() == ""
allOne.inc("test")
assert allOne.getMaxKey() == "test"
assert allOne.getMinKey() == "test"
```

---

## 3. Approach

### 3a. Brute Force Approach
- Use a dictionary to store counts for each key.
- `inc` and `dec` can be done in O(1) by directly modifying the dictionary.
- `getMaxKey` and `getMinKey` will require iterating through the dictionary to find the max and min values, resulting in O(n) time.

#### Time Complexity:
- **inc() and dec()**: O(1)
- **getMaxKey() and getMinKey()**: O(n) because we need to traverse the dictionary.

#### Space Complexity:
- O(n), where n is the number of distinct keys stored in the dictionary.

---

## 4. Code Implementation

### Python Implementation:
```python
class AllOne:
    def __init__(self):
        self.myDict = {}

    def inc(self, key: str) -> None:
        if key in self.myDict:
            self.myDict[key] += 1
        else:
            self.myDict[key] = 1

    def dec(self, key: str) -> None:
        if key in self.myDict:
            if self.myDict[key] > 1:
                self.myDict[key] -= 1
            else:
                self.myDict.pop(key)

    def getMaxKey(self) -> str:
        if not self.myDict:
            return ""
        maxVal = max(self.myDict.values())
        for key in self.myDict.keys():
            if self.myDict[key] == maxVal:
                return key

    def getMinKey(self) -> str:
        if not self.myDict:
            return ""
        minVal = min(self.myDict.values())
        for key in self.myDict.keys():
            if self.myDict[key] == minVal:
                return key
```

---

### Java Implementation:
```java
import java.util.HashMap;
import java.util.Map;

class AllOne {
    private Map<String, Integer> map;

    public AllOne() {
        map = new HashMap<>();
    }

    public void inc(String key) {
        map.put(key, map.getOrDefault(key, 0) + 1);
    }

    public void dec(String key) {
        if (!map.containsKey(key)) return;
        if (map.get(key) == 1) {
            map.remove(key);
        } else {
            map.put(key, map.get(key) - 1);
        }
    }

    public String getMaxKey() {
        if (map.isEmpty()) return "";
        int maxVal = Integer.MIN_VALUE;
        String maxKey = "";
        for (String key : map.keySet()) {
            if (map.get(key) > maxVal) {
                maxVal = map.get(key);
                maxKey = key;
            }
        }
        return maxKey;
    }

    public String getMinKey() {
        if (map.isEmpty()) return "";
        int minVal = Integer.MAX_VALUE;
        String minKey = "";
        for (String key : map.keySet()) {
            if (map.get(key) < minVal) {
                minVal = map.get(key);
                minKey = key;
            }
        }
        return minKey;
    }
}
```

---

## 5. Edge Cases
- **Empty Data Structure**: Both `getMaxKey` and `getMinKey` should return `""` when no keys exist.
- **Single Key**: The same key should be returned for both `getMaxKey` and `getMinKey`.
- **Keys with same frequency**: Handle ties by returning any one of the keys with max/min counts.

---

## 6. References
- **LeetCode Problem**: [432. All O` one Data Structure](https://leetcode.com/problems/all-oone-data-structure/)
- **Python Dictionary Documentation**: [Python dict](https://docs.python.org/3/library/stdtypes.html#typesmapping)
