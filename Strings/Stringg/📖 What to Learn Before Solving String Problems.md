

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
    

👉 Example:

- Check Anagram (`listen`, `silent`).
    
- First Unique Character in a String.
    

---

### **3. Sliding Window Pattern**

Many string problems = **substring with some property** → use sliding window.

- Fixed size window: Maximum vowels in a substring of length `k`.
    
- Variable size window: Longest substring without repeating characters.
    

👉 Learn: expand `right`, shrink `left` while maintaining condition.

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