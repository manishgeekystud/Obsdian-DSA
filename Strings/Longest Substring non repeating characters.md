**Example 1:**

**Input:** s = "abcabcbb"
**Output:** 3
**Explanation:** The answer is "abc", with the length of 3.

**Example 2:**

**Input:** s = "bbbbb"
**Output:** 1
**Explanation:** The answer is "b", with the length of 1.

**Example 3:**

**Input:** s = "pwwkew"
**Output:** 3
**Explanation:** The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

-----------------------------------------------------------------------

## 1️⃣ Brute Force (Generate All Substrings)

### Algorithm:

1. Generate all substrings `s[i..j]`.
    
2. For each substring, check if it has duplicates (using HashSet).
    
3. Track max length.
    

### Complexity:

- O(N³) time (generate + check)
    
- O(N) space
    

### Java Code:
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int maxLen = 0;

        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                if (allUnique(s, i, j)) {
                    maxLen = Math.max(maxLen, j - i + 1);
                }
            }
        }
        return maxLen;
    }

    private boolean allUnique(String s, int start, int end) {
        Set<Character> set = new HashSet<>();
        for (int i = start; i <= end; i++) {
            char ch = s.charAt(i);
            if (set.contains(ch)) return false;
            set.add(ch);
        }
        return true;
    }
}


```

## 2️⃣ Better Brute Force (Fix Start, Expand End)

### Algorithm:

1. Loop `i` from 0 to n-1 (start of substring).
    
2. Use a HashSet while expanding `j` forward.
    
3. Stop expansion when duplicate found.
    
4. Track max length.
    

### Complexity:

- O(N²) time
    
- O(N) space
    

### Java Code:
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int maxLen = 0;

        for (int i = 0; i < n; i++) {
            Set<Character> set = new HashSet<>();
            for (int j = i; j < n; j++) {
                if (set.contains(s.charAt(j))) break;
                set.add(s.charAt(j));
                maxLen = Math.max(maxLen, j - i + 1);
            }
        }
        return maxLen;
    }
}


```

## 3️⃣ Sliding Window with HashSet (Good)

### Algorithm:

1. Maintain a window `[i..j]` using two pointers.
    
2. Expand `j` if `s[j]` not in set.
    
3. If duplicate → remove `s[i]` and move `i`.
    
4. Update max length.
    

### Complexity:

- O(N) time
    
- O(N) space
    

### Java Code:
```java


```