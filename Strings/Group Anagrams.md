Given an array of strings `strs`, group the anagrams together. You can return the answer in **any order**.

**Example 1:**

**Input:** strs = ["eat","tea","tan","ate","nat","bat"]

**Output:** [["bat"],["nat","tan"],["ate","eat","tea"]]

**Explanation:**

- There is no string in strs that can be rearranged to form `"bat"`.
- The strings `"nat"` and `"tan"` are anagrams as they can be rearranged to form each other.
- The strings `"ate"`, `"eat"`, and `"tea"` are anagrams as they can be rearranged to form each other.

**Example 2:**

**Input:** strs = [""]

**Output:** [[""]]

**Example 3:**

**Input:** strs = ["a"]

**Output:** [["a"]]

---------------------------------------
## 🐌 Brute Force Approach

### Idea

- For each word, compare with every other word to check if they are anagrams.
    
- Two strings are anagrams if their **sorted versions are the same**.
    
- Group them manually.
    

### Steps

1. Maintain a boolean visited array.
    
2. For each word not yet visited:
    
    - Create a new group.
        
    - Compare with remaining words → if they are anagrams, mark visited and add to group.
        
3. Collect all groups.
    

### Complexity

- Sorting each string = O(L log L) (where L = average string length).
    
- Comparing every pair = O(n²).
    
- **Time: O(n² · L log L)** → very slow for large input.

![[Pasted image 20250910234203.png]]

---

## ⚡ Optimized Approach (Using HashMap)

### Idea

- All anagrams share the same sorted string.  
    Example: `"eat"`, `"tea"`, `"ate"` → sorted form = `"aet"`.
    
- Use this sorted string as a **key** in a HashMap.
    
- Store all original words with the same key in a list.
    

---

### Code ()
```java
import java.util.*;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if (strs == null || strs.length == 0) return new ArrayList<>();

        Map<String, List<String>> map = new HashMap<>();

        for (String word : strs) {
            char[] temp = word.toCharArray();
            Arrays.sort(temp);              // sort characters
            String key = new String(temp);  // create key from sorted chars

            if (!map.containsKey(key)) {
                map.put(key, new ArrayList<>());
            }
            map.get(key).add(word);         // add word to group
        }

        return new ArrayList<>(map.values());
    }
}


```



---

### Dry Run (Input = `["eat","tea","tan","ate","nat","bat"]`)

1. `eat` → sorted `"aet"`  
    → map = { `"aet"` → ["eat"] }
    
2. `tea` → sorted `"aet"`  
    → map = { `"aet"` → ["eat","tea"] }
    
3. `tan` → sorted `"ant"`  
    → map = { `"aet"` → ["eat","tea"], `"ant"` → ["tan"] }
    
4. `ate` → sorted `"aet"`  
    → map = { `"aet"` → ["eat","tea","ate"], `"ant"` → ["tan"] }
    
5. `nat` → sorted `"ant"`  
    → map = { `"aet"` → ["eat","tea","ate"], `"ant"` → ["tan","nat"] }
    
6. `bat` → sorted `"abt"`  
    → map = { `"aet"` → ["eat","tea","ate"], `"ant"` → ["tan","nat"], `"abt"` → ["bat"] }
    

Final result:

`[["eat","tea","ate"], ["tan","nat"], ["bat"]]`

---

## 🔑 Key Things to Remember

1. **Sorting as a key** → simplest and most common approach.
    
2. `Map<String, List<String>>` stores groups efficiently.
    
3. `map.values()` gives the grouped lists.
    
4. Time Complexity:
    
    - Sorting each string: O(L log L)
        
    - Doing it for `n` strings: O(n · L log L)
        
    - Much better than brute force.
        
5. Space Complexity: O(n · L) (to store all strings in the map).
    

---

## 🚀 Alternate Optimization

Instead of sorting, we can use a **character frequency count (26 letters)** as the key.

- Build a key like `"a1b0c0...z0"`.
    
- Faster because counting is O(L), while sorting is O(L log L).
    
- But sorting-based approach is easier to write & understand.
    

---

✅ **Final Tip:** In interviews, always start with the **sorting key HashMap approach** → it’s clean, easy, and efficient enough.  
If asked for optimization, explain the **character frequency key** approach