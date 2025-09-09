Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window**_ **_substring_** _of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window_. If there is no such substring, return _the empty string_ `""`.

The testcases will be generated such that the answer is **unique**.

**Example 1:**

**Input:** s = "ADOBECODEBANC", t = "ABC"
**Output:** "BANC"
**Explanation:** The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

**Example 2:**

**Input:** s = "a", t = "a"
**Output:** "a"
**Explanation:** The entire string s is the minimum window.

**Example 3:**

**Input:** s = "a", t = "aa"
**Output:** ""
**Explanation:** Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string

--------------------------------------------------------------------
**Brute Force** ----TLE n3
```java
class Solution {
    // Function to find the minimum window substring
    public String minWindow(String s, String t) {
        String result = "";                   // Final answer
        int minLen = Integer.MAX_VALUE;       // Track minimum length found

        // Generate all substrings of s
        for (int i = 0; i < s.length(); i++) {
            for (int j = i + 1; j <= s.length(); j++) {
                String sub = s.substring(i, j);

                // Check if this substring contains all characters of t
                if (containsAll(sub, t)) {
                    // Update result if this is smaller than previous
                    if (sub.length() < minLen) {
                        minLen = sub.length();
                        result = sub;
                    }
                }
            }
        }

        return result; // If not found, result will remain empty
    }

    // Helper function to check if substring "sub" contains all chars of "t"
    static boolean containsAll(String sub, String t) {
        int[] freqSub = new int[128]; // Frequency array for substring
        int[] freqT = new int[128];   // Frequency array for t

        // Count characters in substring
        for (char c : sub.toCharArray()) {
            freqSub[c]++;
        }

        // Count characters in t
        for (char c : t.toCharArray()) {
            freqT[c]++;
        }

        // Check if substring covers all requirements of t
        for (int i = 0; i < 128; i++) {
            if (freqSub[i] < freqT[i]) {
                return false; // Missing required characters
            }
        }
        return true;
    }
}


```

--------------------------------------------
### ALGO-- O(N)

**Step 1: Build `need` map**

- Count frequency of characters in `t`.
    
- Example: `t = "ABC"` → `need = {A=1, B=1, C=1}`
    

---

### Step 2: Expand window with `right`

- Add characters one by one into `window` map.
    
- If a character’s count in `window` matches the required count in `need`, we increase `formed`.
    
- When `formed == required`, it means **all required characters are inside the window**.
    

---

### Step 3: Shrink window with `left`

- Try to shrink from the left while window is still valid.
    
- Every time we shrink, if the window is smaller than the previous minimum, update the result.
    
- If removing a character breaks the condition, stop shrinking and move `right` again.
    

---

### Step 4: Return result

- Keep track of the smallest valid window.
    
- If none found, return `""`.

**CODE**
```java
import java.util.HashMap;

public class Solution {
    public String minWindow(String s, String t) {
        if (s == null || s.length() == 0 || t == null || t.length() == 0) {
            return "";
        }

        // Step 1: Build frequency map for string t
        HashMap<Character, Integer> need = new HashMap<>();
        for (char c : t.toCharArray()) {
            need.put(c, need.getOrDefault(c, 0) + 1);
        }

        // Step 2: Sliding window variables
        HashMap<Character, Integer> window = new HashMap<>();
        int left = 0, right = 0;  // window boundaries
        int formed = 0;           // number of chars that meet the requirement
        int required = need.size(); // unique characters needed

        int minLen = Integer.MAX_VALUE;
        int start = 0; // track starting index of result

        // Step 3: Expand the window
        while (right < s.length()) {
            char c = s.charAt(right);
            window.put(c, window.getOrDefault(c, 0) + 1);

            // if character matches frequency in t
            if (need.containsKey(c) && window.get(c).intValue() ==                                                                 need.get(c).intValue()) {
                formed++;
            }

            // Step 4: Try to shrink from left while window is valid
            while (left <= right && formed == required) {
                if (right - left + 1 < minLen) {
                    minLen = right - left + 1;
                    start = left;
                }

                char leftChar = s.charAt(left);
                window.put(leftChar, window.get(leftChar) - 1);

                if (need.containsKey(leftChar) && window.get(leftChar) <                                                                  need.get(leftChar)) {
                    formed--;
                }
                left++;
            }

            // Move right pointer forward
            right++;
        }

        return (minLen == Integer.MAX_VALUE) ? "" : s.substring(start, start + minLen);
    }

    // Quick test
    public static void main(String[] args) {
        Solution sol = new Solution();
        String s = "ADOBECODEBANC";
        String t = "ABC";
        System.out.println(sol.minWindow(s, t)); // Output: "BANC"
    }
}


```

---

# 🏃 Dry Run Example

Input:  
`s = "ADOBECODEBANC"`  
`t = "ABC"`

👉 `need = {A=1, B=1, C=1}`, `required = 3`

---

### Window movement

1. **right=0 → 'A'**
    
    - window = {A=1}
        
    - `A` requirement met → `formed=1`
        
    - Not valid yet (`formed=1 < 3`)
        

---

2. **right=1 → 'D'**
    
    - window = {A=1, D=1}
        
    - Not needed → ignore
        
    - `formed=1`
        

---

3. **right=2 → 'O'**
    
    - window = {A=1, D=1, O=1}
        
    - Not needed
        
    - `formed=1`
        

---

4. **right=3 → 'B'**
    
    - window = {A=1, D=1, O=1, B=1}
        
    - `B` matches → `formed=2`
        

---

5. **right=5 → 'C'**
    
    - window = {A=1, D=1, O=1, B=1, E=1, C=1}
        
    - `C` matches → `formed=3`
        
    - ✅ Now window has all (A,B,C) → valid!
        

---

6. **Shrink from left** (`left=0`)
    
    - Window = "ADOBEC" (len=6) → minLen=6, start=0
        
    - Remove 'A' → window no longer valid (`formed=2`)
        
    - Stop shrinking
        

---

7. **Continue expanding** until `right=9 → 'A'`
    
    - window regains 'A' → `formed=3` again
        
    - Window = "BECODEBA"
        
    
    Shrink again:
    
    - Remove 'B' (left=3) → still valid
        
    - Remove 'E' (left=4) → still valid
        
    - Remove 'C' (left=5) → breaks condition (`formed=2`)
        
    
    Minimum updated to "CODEBA" (len=6, but same as before).
    

---

8. **right=11 → 'N'** → doesn’t help.
    

---

9. **right=12 → 'C'**
    
    - window = "...BANC"
        
    - Valid again (`formed=3`)
        
    
    Shrink:
    
    - Remove extras until smallest valid window = `"BANC"` (len=4)
        
    - Update minLen=4, start=9
        

---

✅ Final Answer = `"BANC"`

---

# 🎯 Final Notes

- **Brute force** = easy but slow.
    
- **Sliding window with HashMap** = efficient (O(n)), standard interview answer.
    
- **Dry run** shows how window expands/shrinks until the minimum substring `"BANC"` is found.