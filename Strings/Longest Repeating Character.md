You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return _the length of the longest substring containing the same letter you can get after performing the above operations_.

**Example 1:**

**Input:** s = "ABAB", k = 2
**Output:** 4
**Explanation:** Replace the two 'A's with two 'B's or vice versa.

**Example 2:**

**Input:** s = "AABABBA", k = 1
**Output:** 4
**Explanation:** Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may exists other ways to achieve this answer too.

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of only uppercase English letters.
- `0 <= k <= s.length`
------------------------------------------------------
## 1️⃣ Problem Statement

Given a string `s` consisting of only **uppercase English letters** and an integer `k`.  
You can change at most `k` characters in the string.

👉 Find the **length of the longest substring** where all characters are the same after at most `k` replacements.

**Example:**

- Input: `s = "AABABBA"`, `k = 1`
    
- Output: `4` (change one `'B'` → `"AAAA"`)
    

---

## 2️⃣ Approaches

---

### 🔴 Brute Force (Naive)

**Idea:**

- Check every substring.
    
- For each substring, count how many replacements are needed.
    
- If replacements ≤ `k`, update answer.
    

**Steps:**

1. Generate all substrings (`O(n²)` loops).
    
2. For each substring:
    
    - Count frequency of each character.
        
    - Find the max frequency char (`maxCount`).
        
    - Replacements needed = substring length − `maxCount`.
        
3. If replacements ≤ `k`, update max length.
    

**Complexity:**

- Time → `O(n³)` (substring generation + frequency count).
    
- Space → `O(26)` for frequency.
    
- ✅ Easy to understand.
    
- ❌ Too slow for large inputs.
    

---

### 🟡 Optimized Brute Force

- Instead of recomputing frequencies from scratch for each substring, maintain them as window grows.
    
- Still `O(n²)`, but faster in practice.
    

---

### 🟢 Optimized Sliding Window (Best Approach)

**Key Intuition:**

- Use a window `[left, right]`.
- Inside the window, we want to know if we can make all characters equal by replacing at most `k`.
- Formula:
    
    `replacements = (window size - count of most frequent char)`
    
- If `replacements ≤ k` → valid window.
- Else, shrink window from the left.
    

**Steps:**

1. Expand `right` pointer, add character frequency.
2. Track `maxCount` = frequency of most common char in the window.
3. If window is invalid (`window size - maxCount > k`), move `left` forward (shrink).
4. Track maximum valid window size.
    

**Complexity:**

- Time → `O(n)` (each char enters & exits window once).
- Space → `O(26)` for frequency array (constant).
    
- ✅ Efficient and elegant.
- ✅ Standard interview solution.
    

---

## 3️⃣ Java Code

### 🔴 Brute Force
```java
public int characterReplacementBruteForce(String s, int k) {
    int n = s.length();
    int maxLen = 0;

    for (int i = 0; i < n; i++) {
        int[] freq = new int[26];
        for (int j = i; j < n; j++) {
            freq[s.charAt(j) - 'A']++;
            int maxCount = 0;
            for (int f : freq) maxCount = Math.max(maxCount, f);

            int windowSize = j - i + 1;
            if (windowSize - maxCount <= k) {
                maxLen = Math.max(maxLen, windowSize);
            }
        }
    }
    return maxLen;
}

```
---

### 🟢 Sliding Window (Optimized)

```java
public int characterReplacement(String s, int k) {
    int[] freq = new int[26];
    int left = 0, maxCount = 0, maxLength = 0;

    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        freq[c - 'A']++;
        maxCount = Math.max(maxCount, freq[c - 'A']);

        while ((right - left + 1) - maxCount > k) {
            freq[s.charAt(left) - 'A']--;
            left++;
        }

        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}

```

---

## 4️⃣ Dry Run Example

`s = "AABABBA"`, `k = 1`

👉 Goal: longest substring we can turn into repeating letters with ≤ 1 replacement.

---

### Step-by-step:

- **Window:** expand right, track freq + maxCount.
    

1. `right=0 → 'A'`
    
    - freq[A]=1, maxCount=1
        
    - window="A" → valid (size=1)
        
    - maxLen=1
        
2. `right=1 → 'A'`
    
    - freq[A]=2, maxCount=2
        
    - window="AA" → valid (size=2)
        
    - maxLen=2
        
3. `right=2 → 'B'`
    
    - freq[B]=1, maxCount=2
        
    - window="AAB" → valid (size=3, since 3−2=1 ≤ k)
        
    - maxLen=3
        
4. `right=3 → 'A'`
    
    - freq[A]=3, maxCount=3
        
    - window="AABA" → valid (size=4, since 4−3=1 ≤ k)
        
    - maxLen=4
        
5. `right=4 → 'B'`
    
    - freq[B]=2, maxCount=3
        
    - window="AABAB" → invalid (size=5, since 5−3=2 > k)
        
    - shrink: left=1 → window="ABAB" (size=4, valid)
        
    - maxLen=4
        
6. `right=5 → 'B'`
    
    - freq[B]=3, maxCount=3
        
    - window="ABABB" → valid (size=5−1+1=5, but 5−3=2 > k)
        
    - shrink: left=2 → window="BABB" (size=4, valid)
        
    - maxLen=4
        
7. `right=6 → 'A'`
    
    - freq[A]=2, freq[B]=3, maxCount=3
        
    - window="BABBA" → valid (size=5, 5−3=2 > k → shrink)
        
    - shrink left=3 → window="ABBA" (size=4, valid)
        
    - maxLen=4
        

✅ Final Answer = `4`

---

## 5️⃣ Key Things to Remember

- Formula: `window size - maxCount` = replacements needed.
    
- Only shrink window if replacements > k.
    
- `maxCount` does **not need to decrease** when shrinking (keeps code efficient).
    
- Use **array of size 26** for frequency (faster than HashMap).
    
- **Brute force = only for understanding**, sliding window is the real solution.
    

---

📌 **Interview tip:** If interviewer asks you brute force first → explain it, then move to sliding window as optimization.