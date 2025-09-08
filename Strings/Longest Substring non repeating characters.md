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


```