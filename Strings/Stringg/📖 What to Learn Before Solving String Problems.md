

### **1. Basics of Strings in Java**

- How strings are stored (`String`, `StringBuilder`, `StringBuffer`).
    
- Immutability of `String`.
    
- Common functions: `.charAt()`, `.substring()`, `.length()`, `.toCharArray()`, `.equals()`, `.contains()`.
    
- Why use `StringBuilder` for modifications.
    

👉 Small exercise: reverse a string using `StringBuilder` vs without it.

---

### **2. Frequency & Counting**

- Use **arrays** (`int[26]` for lowercase, `int[256]` for ASCII).
    
- Use **HashMap<Character,Integer>** when characters are not fixed.
    
- Build muscle memory for **count frequency, compare frequency**.


---------------------------------------------------------------------
# 2.Count Frequency & Compare Frequency

## 1. What it Means

- Count Frequency → track how many times each character (or number) appears.
    
- Compare Frequency → check if two strings/arrays have the same distribution of characters.
    

---

## 2. Ways to Count

### Fixed Character Set (lowercase a–z)

```java
int[] freq = new int[26]; 
for (char c : s.toCharArray())
{     freq[c - 'a']++;   // map 'a' → 0, 'b' → 1, etc. }
```

### Full ASCII / Unicode
```java
int[] freq = new int[256];
for (char c : s.toCharArray()) {
    freq[c]++;   // direct indexing
}

```

### Using HashMap (when input not fixed size)

```java
Map<Character, Integer> freq = new HashMap<>();
for (char c : s.toCharArray()) {
    freq.put(c, freq.getOrDefault(c, 0) + 1);
}

```

---

## 3. Comparing Frequencies

### Two Strings Anagram Check (array)

`if (Arrays.equals(freq1, freq2)) {     return true; }`

### HashMap Comparison

`if (map1.equals(map2)) {     return true; }`

---

## 4. Example Problems

1. Valid Anagram (LeetCode 242)  
    Count frequencies of both strings → compare.
    
2. Ransom Note (LeetCode 383)  
    Count letters in magazine → check if ransomNote letters can be satisfied.
    
3. First Unique Character (LeetCode 387)  
    Count frequency → find first index with freq = 1.
    

---

## 5. Interview Tips

- Use array when possible → O(1) access, less overhead.
    
- Use HashMap when input domain is unknown/large (Unicode, words).
    
- Avoid sorting (O(n log n)) → prefer frequency counting (O(n)).
    

---

## 6. Complexity

- Counting → O(n)
    
- Comparing → O(1) for fixed array (26/256), O(k) for HashMap (k = unique chars)
    
- Space → O(1) for array, O(k) for HashMap
    

---

## Key Idea

Convert problem into count arrays/maps → then compare.  

---

### **3. Sliding Window Pattern**

Many string problems = **substring with some property** → use sliding window.

- Fixed size window: Maximum vowels in a substring of length `k`.
    
- Variable size window: Longest substring without repeating characters.
    

👉 Learn: expand `right`, shrink `left` while maintaining condition.

## 1. Why Sliding Window for Strings?

- Many string problems deal with **substrings (contiguous parts of a string)**.
    
- Often need to find:
    
    - Longest/shortest substring with certain property.
        
    - Count substrings satisfying a condition.
        
- Brute force = O(n²) → Sliding Window reduces to **O(n)**.
    

---

## 2. Identifying Sliding Window in Strings

Look for problems with these keywords:

- **Substring / subarray**
    
- **Longest / shortest**
    
- **At most K distinct characters**
    
- **Exactly K distinct characters**
    
- **No repeating characters**
    
- **Minimum window covering all characters**
    

If problem asks for _contiguous substring_ → almost always **Sliding Window**.


---

## 3. Types of Sliding Window in Strings

### Fixed Size Window

- Substring length `k` given.
    
- Maintain frequency map/array.

**Example:** Count distinct characters in every substring of length `k`
```java
for (int i = 0; i < k; i++) {
    freq[s.charAt(i)]++;
}
for (int i = k; i < n; i++) {
    freq[s.charAt(i)]++;
    freq[s.charAt(i - k)]--;
}
```

### Variable Size Window

- Window expands/contracts based on condition.
    
- Use **two pointers (left, right)**.
    
- Track character frequencies with **HashMap or array**.
    

#### Example: Longest Substring Without Repeating Characters (LeetCode 3)

- Expand `right`.
    
- If char repeats → shrink `left` until valid.
```java
Map<Character, Integer> map = new HashMap<>();
int left = 0, maxLen = 0;

for (int right = 0; right < s.length(); right++) {
    char c = s.charAt(right);
    if (map.containsKey(c) && map.get(c) >= left) {
        left = map.get(c) + 1;
    }
    map.put(c, right);
    maxLen = Math.max(maxLen, right - left + 1);
}

```

## 4. Common Sliding Window String Problems

### Frequency/Character Tracking

- **Valid Anagram Window** (LeetCode 438) → check substring anagrams.
- **Minimum Window Substring** (LeetCode 76).
- **Permutation in String** (LeetCode 567).
    

### Distinct / Unique Characters

- **Longest substring without repeating characters** (LeetCode 3).
- **Longest substring with at most K distinct characters** (LeetCode 340).

### Count / Length Problems

- **Smallest substring with all distinct characters** (GFG).
- **Longest repeating character replacement** (LeetCode 424).

5. General Template (Variable Size)
```java
int left = 0;
for (int right = 0; right < s.length(); right++) {
    // include s.charAt(right) into window
    
    while (condition violated) {
        // remove s.charAt(left) from window
        left++;
    }
    
    // check/update answer
}

```
## 6. Interview Tips

- **Fixed window** → size `k` is explicitly mentioned.
    
- **Variable window** → condition depends on content (distinct chars, matching pattern).
    
- Use `HashMap<Character, Integer>` for general problems.
    
- Use `int[26]` if only lowercase letters → faster.
    
- Practice dry runs to avoid off-by-one errors.
---

### **4. Two Pointer Technique**

- Works when you need to shrink/grow substring.
    
- Palindrome check.
    
- Minimum Window Substring.
    

👉 Key = left & right pointers moving over the string.

---

### **5. Hashing & Sets in Strings**

- Detect duplicates → `HashSet`.
    
- Store frequencies → `HashMap`.
    
- Pattern problems: Group Anagrams, Isomorphic Strings.

# Hashing & Sets in String Problems

## 1. Why Hashing/Sets in Strings?

- Strings involve characters and substrings.
    
- Need to check:
    
    - Duplicates (seen before?).
        
    - Frequency counts (anagrams, subsequences).
        
    - Fast lookups (membership in O(1)).
        
- **Hashing (HashMap/HashSet)** helps achieve O(1) average time.
    

---

## 2. Common Uses

### A. HashSet

- Stores unique characters/substrings.
    
- Helps with **duplicate detection** or **uniqueness constraints**.
    

#### Example: Longest Substring Without Repeating Characters (LeetCode 3)
    

---

### **6. Sorting & String Manipulation**

- Sort characters inside string (`Arrays.sort(charArray)`).
    
- Helps with Anagram & grouping problems.
    

---

### **7. Advanced Concepts (after above basics)**

- **KMP Algorithm** → efficient substring search.
    
- **Rabin Karp / Rolling Hash** → plagiarism detection, substring search.
    
- **Trie (Prefix Tree)** → autocomplete, word search in dictionary.
    
- **Dynamic Programming** on strings:
    
    - Longest Common Subsequence (LCS).
        
    - Edit Distance.
        
    - Word Break.