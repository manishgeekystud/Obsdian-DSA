
Given a string `s`, rearrange the characters of `s` so that any two adjacent characters are not the same.

Return _any possible rearrangement of_ `s` _or return_ `""` _if not possible_.

**Example 1:**

**Input:** s = "aab"
**Output:** "aba"

**Example 2:**

**Input:** s = "aaab"
**Output:** ""

**Constraints:**

- `1 <= s.length <= 500`

---------------------------------------------------------


## Approach 1: Priority Queue Approach

### Objective

To solve the "767. Reorganize String" problem, the priority queue approach leverages a max heap to maintain the frequency of each character. By doing so, we can alternate the most frequent characters with the remaining ones to ensure no adjacent characters are the same.

### Key Data Structures

- **Max Heap**: Used for storing characters sorted by their frequency in descending order.

### Enhanced Breakdown

1. **Initialization**:
    
    - Count the frequency of each character in the string.
    - Populate the max heap with these frequencies.
2. **Processing Each Character**:
    
    - Pop the top two characters from the max heap (i.e., the ones with the highest frequency).
    - Append these two characters to the result string.
    - Decrement their frequencies and re-insert them back into the max heap.
    - If only one character remains in the heap, make sure it doesn't exceed half of the string length, otherwise, return an empty string.
3. **Wrap-up**:
    
    - If there's a single remaining character with a frequency of 1, append it to the result.
    - Join all the characters to return the final reorganized string.

## Example:

Given the input "aab":

- Max heap after initialization: `[(-2, 'a'), (-1, 'b')]`
- Result after first iteration: "ab"
- Wrap-up: Result is "aba"

**CODE**
```java
public class Solution {
    public String reorganizeString(String s) {
        HashMap<Character, Integer> freqMap = new HashMap<>();
        for (char c : s.toCharArray()) {
            freqMap.put(c, freqMap.getOrDefault(c, 0) + 1);
        }

        PriorityQueue<Character> maxHeap = new PriorityQueue<>((a, b) -> freqMap.get(b) - freqMap.get(a));
        maxHeap.addAll(freqMap.keySet());

        StringBuilder res = new StringBuilder();
        while (maxHeap.size() >= 2) {
            char char1 = maxHeap.poll();
            char char2 = maxHeap.poll();

            res.append(char1);
            res.append(char2);

            freqMap.put(char1, freqMap.get(char1) - 1);
            freqMap.put(char2, freqMap.get(char2) - 1);

            if (freqMap.get(char1) > 0) maxHeap.add(char1);
            if (freqMap.get(char2) > 0) maxHeap.add(char2);
        }

        if (!maxHeap.isEmpty()) {
            char ch = maxHeap.poll();
            if (freqMap.get(ch) > 1) return "";
            res.append(ch);
        }

        return res.toString();
    }
}
```

# 🔹 Code Explanation

```
public String reorganizeString(String s) {
    // Step 1: Count frequency of each character
    HashMap<Character, Integer> freqMap = new HashMap<>();
    for (char c : s.toCharArray()) {
        freqMap.put(c, freqMap.getOrDefault(c, 0) + 1);
    }

```

👉 Here we build a frequency map.  
Example `s = "aab"` →  
`freqMap = {a=2, b=1}`

---
```
    // Step 2: Create a max-heap based on frequency
    PriorityQueue<Character> maxHeap = new PriorityQueue<>(
        (a, b) -> freqMap.get(b) - freqMap.get(a) // higher freq first
    );
    maxHeap.addAll(freqMap.keySet());


```


👉 `PriorityQueue` stores characters sorted by **frequency (highest first)**.  
For `"aab"`, heap = `[a, b]` (`a` before `b` since a=2, b=1).

---
```
    // Step 3: Greedily build result by picking 2 most frequent chars
    StringBuilder res = new StringBuilder();
    while (maxHeap.size() >= 2) {
        char char1 = maxHeap.poll();
        char char2 = maxHeap.poll();

        res.append(char1);
        res.append(char2);

        freqMap.put(char1, freqMap.get(char1) - 1);
        freqMap.put(char2, freqMap.get(char2) - 1);

        if (freqMap.get(char1) > 0) maxHeap.add(char1);
        if (freqMap.get(char2) > 0) maxHeap.add(char2);
    }

```
   

👉 Here’s the greedy trick:

- Always take **top 2 most frequent characters** → prevents same letters from being adjacent.
    
- Append them → decrease count → push back if still > 0.
    

**Dry Run `s = "aab"`:**

- Heap = `[a(2), b(1)]`
    
- Poll: `a, b` → append `"ab"`
    
    - New freq: `a=1, b=0` → push back `a`.
        
- Heap = `[a(1)]`
    

---
```
    // Step 4: Handle leftover
    if (!maxHeap.isEmpty()) {
        char ch = maxHeap.poll();
        if (freqMap.get(ch) > 1) return ""; // cannot place safely
        res.append(ch);
    }

```
   

👉 If one char remains:

- If freq = 1 → safe → append.
    
- If freq > 1 → impossible (adjacent duplicate).
    

For `"aab"` → `a` left with count 1 → result `"aba"`. ✅

---

    `return res.toString(); }`

---

# 🔹 Dry Run Examples

### Example 1: `"aab"`

- freqMap = `{a=2, b=1}`
    
- Heap = `[a, b]`
    
- Poll `a, b` → res = `"ab"`
    
    - freq = `{a=1, b=0}` → push back `a`
        
- Heap = `[a]` → append `"a"` → result `"aba"` ✅
    

---

### Example 2: `"aaab"`

- freqMap = `{a=3, b=1}`
    
- Heap = `[a, b]`
    
- Poll `a, b` → res = `"ab"`, freq = `{a=2, b=0}` → push back `a`
    
- Heap = `[a]` → but freq[a]=2 → cannot place safely → return `""` ❌
    

---

# 🔹 Complexity

- **Time:** O(n log k)
    
    - n = length of string
        
    - k = unique characters
        
- **Space:** O(k) for map + heap