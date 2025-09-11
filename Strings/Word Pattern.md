Given a `pattern` and a string `s`, find if `s` follows the same pattern.

Here **follow** means a full match, such that there is a bijection between a letter in `pattern` and a **non-empty** word in `s`. Specifically:

- Each letter in `pattern` maps to **exactly** one unique word in `s`.
- Each unique word in `s` maps to **exactly** one letter in `pattern`.
- No two letters map to the same word, and no two words map to the same letter.

**Example 1:**

**Input:** pattern = "abba", s = "dog cat cat dog"

**Output:** true

**Explanation:**

The bijection can be established as:

- `'a'` maps to `"dog"`.
- `'b'` maps to `"cat"`.

**Example 2:**

**Input:** pattern = "abba", s = "dog cat cat fish"

**Output:** false

**Example 3:**

**Input:** pattern = "aaaa", s = "dog cat cat dog"

**Output:** false

--------------------------------------------------------------
# ✅ Approach Explanation

1. **Split words:**
    
    - Convert `s` into words using `s.split(" ")`.
        
2. **Length mismatch check:**
    
    - If `pattern.length() != words.length`, immediately return `false`.
        
3. **Use HashMap for mapping:**
    
    - Create a `HashMap<Character, String>` to map each `pattern` character to a word.
        
4. **Iterate through pattern and words:**
    
    - For each character–word pair:
        
        - If the character **already exists in the map**:
            
            - Ensure the mapped word equals the current word.
                
            - If not, return `false`.
                
        - Else:
            
            - If the word is already mapped to another character (`hm.containsValue(words[i])`), return `false`.
                
            - Otherwise, add the mapping `hm.put(ch, words[i])`.
                
5. **Return true:**
    
    - If all checks pass, return `true`.
        

---

# ⚡ Key Things to Remember

- **String comparison in Java:**  
    Use `.equals()` instead of `==` or `!=` (which compare memory addresses, not content).
    
- **Bijective mapping:**  
    Each character must map to one unique word, and each word must map to one unique character.
    
- **Edge cases:**
    
    - Pattern and words length mismatch → `false`.
        
    - Repeated words for different pattern chars → `false`.
        
    - Empty input cases (check constraints).
        
**Final Code**
```java
class Solution {
    public boolean wordPattern(String pattern, String s) {
        String[] words = s.split(" ");
        HashMap<Character, String> hm = new HashMap<>();

        if (pattern.length() != words.length) return false;

        for (int i = 0; i < pattern.length(); i++) {
            char ch = pattern.charAt(i);

            if (hm.containsKey(ch)) {
                if (!hm.get(ch).equals(words[i])) return false;
            } else if (hm.containsValue(words[i])) {
                return false;
            }

            hm.put(ch, words[i]);
        }

        return true;
    }
}

```
---

# 🔎 Dry Run Example

Input:  
`pattern = "abba"`, `s = "dog cat cat dog"`

|i|pattern[i]|word[i]|HashMap State|Action / Check|
|---|---|---|---|---|
|0|a|dog|{}|add {a=dog}|
|1|b|cat|{a=dog}|add {b=cat}|
|2|b|cat|{a=dog, b=cat}|b exists → word matches "cat" ✅|
|3|a|dog|{a=dog, b=cat}|a exists → word matches "dog" ✅|

✅ All checks passed → return `true`.