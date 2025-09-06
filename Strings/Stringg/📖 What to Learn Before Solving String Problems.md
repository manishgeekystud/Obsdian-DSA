

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
    

---------------------------------------------------------------------
# 📖 Notes – Count Frequency & Compare Frequency

---

## 🔹 1. What it Means

- **Count Frequency** → track how many times each character (or number) appears.
    
- **Compare Frequency** → check if two strings/arrays have the **same distribution** of characters.
    

---

## 🔹 2. Ways to Count

### ✅ Fixed Character Set (like lowercase `a–z`)

`int[] freq = new int[26]; for (char c : s.toCharArray()) {     freq[c - 'a']++;   // map 'a' → 0, 'b' → 1, etc. }`

### ✅ Full ASCII / Unicode

`int[] freq = new int[256]; for (char c : s.toCharArray()) {     freq[c]++;   // direct indexing }`

### ✅ Using HashMap (when input not fixed size)

`Map<Character, Integer> freq = new HashMap<>(); for (char c : s.toCharArray()) {     freq.put(c, freq.getOrDefault(c, 0) + 1); }`

---

## 🔹 3. Comparing Frequencies

- **Two Strings Anagram Check**
    

`if (Arrays.equals(freq1, freq2)) return true;`

- **HashMap comparison**
    

`if (map1.equals(map2)) return true;`

---

## 🔹 4. Example Problems

1. **Valid Anagram (LC 242)**
    
    - Count frequencies of both strings → compare.
        
2. **Ransom Note (LC 383)**
    
    - Count letters in magazine → check if ransomNote letters can be satisfied.
        
3. **First Unique Character (LC 387)**
    
    - Count frequency → find first index with freq = 1.
        

---

## 🔹 5. Interview Tips

- **Use array when possible** → O(1) access, less overhead than `HashMap`.
    
- **Use HashMap only if input domain is unknown/large** (e.g., Unicode, words).
    
- When comparing → avoid sorting strings (`O(n log n)`) → prefer frequency counting (`O(n)`).
    

---

## 🔹 6. Complexity

- **Counting** → O(n)
    
- **Comparing** → O(1) for fixed-size array (26/256), O(k) for HashMap (k = unique chars).
    
- **Space** → O(1) for array (constant 26/256), O(k) for HashMap.
    

---

✅ **Pattern Key Idea:**  
👉 Convert the problem into **count arrays/maps** and then **compare**.  
This avoids sorting and gives **linear-time solutions**.
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