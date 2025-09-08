
Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

**Example 1:**

**Input:** s1 = "ab", s2 = "eidbaooo"
**Output:** true
**Explanation:** s2 contains one permutation of s1 ("ba").

**Example 2:**

**Input:** s1 = "ab", s2 = "eidboaoo"
**Output:** false

**Constraints:**

- `1 <= s1.length, s2.length <= 104`
- `s1` and `s2` consist of lowercase English letters.

----------------------------------------------------------------

## 🔴 Approach 1: Brute Force (Generate All Permutations)

### Algorithm

1. Generate all permutations of `s1`.
    
2. For each permutation, check if it’s a substring of `s2`.
    
3. If found → return `true`. Otherwise, return `false`.
    

### Dry Run

`s1 = "ab"`, `s2 = "eidbaooo"`

- Permutations of `ab` → `"ab"`, `"ba"`.
    
- Check substrings of `s2`: `"ei"`, `"id"`, `"db"`, `"ba"` ✅ match.
    
- Return `true`.
    

### Java Code
```java
// ❌ Not efficient, shown only for completeness
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        List<String> perms = new ArrayList<>();
        permute(s1.toCharArray(), 0, perms);
        for (String p : perms) {
            if (s2.contains(p)) return true;
        }
        return false;
    }

    private void permute(char[] arr, int l, List<String> res) {
        if (l == arr.length) {
            res.add(new String(arr));
            return;
        }
        for (int i = l; i < arr.length; i++) {
            swap(arr, l, i);
            permute(arr, l+1, res);
            swap(arr, l, i);
        }
    }

    private void swap(char[] arr, int i, int j) {
        char temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}

```


### Complexity

- Time: **O(n! * n)** (impractical for interviews)
    
- Space: O(n)
    

---

## 🟠 Approach 2: Sorting Substrings

### Algorithm

1. Sort `s1` → `sortedS1`.
    
2. Slide a window of length `s1.length()` over `s2`.
    
3. For each substring, sort it and compare with `sortedS1`.
    
4. If equal → return `true`.
    

### Dry Run

`s1 = "ab"`, `s2 = "eidbaooo"`

- `sortedS1 = "ab"`
    
- Substrings of length 2 → `"ei"` → `"ei"` (sorted) ≠ `"ab"`
    
- `"id"` → `"di"` ≠ `"ab"`
    
- `"db"` → `"bd"` ≠ `"ab"`
    
- `"ba"` → `"ab"` ✅ match → return `true`.
    

### Java Code

```java
import java.util.*;

class Solution {
    public boolean checkInclusion(String s1, String s2) {
        char[] arr1 = s1.toCharArray();
        Arrays.sort(arr1);
        String sortedS1 = new String(arr1);

        int m = s1.length();
        for (int i = 0; i <= s2.length() - m; i++) {
            char[] arr2 = s2.substring(i, i+m).toCharArray();
            Arrays.sort(arr2);
            if (sortedS1.equals(new String(arr2))) {
                return true;
            }
        }
        return false;
    }
}

```

### Complexity

- Time: O((n-m+1) * m log m)
    
- Space: O(m)
    

---

## 🟡 Approach 3: Frequency Count (Naive)

### Algorithm

1. Count frequency of characters in `s1` → `freq1[26]`.
    
2. For each substring of `s2` with length `m`:
    
    - Count frequency `freq2[26]`.
        
    - Compare with `freq1`.
        
3. If equal → return `true`.
    

### Dry Run

`s1 = "ab"`, `s2 = "eidbaooo"`

- `freq1 = {a:1, b:1}`
    
- Window `"ei"` → `{e:1, i:1}` ≠ `freq1`
    
- Window `"id"` → `{i:1, d:1}` ≠
    
- Window `"db"` → `{d:1, b:1}` ≠
    
- Window `"ba"` → `{b:1, a:1}` ✅ match → return `true`.
    

### Java Code

```java
import java.util.*;

class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        if (m > n) return false;

        int[] freq1 = new int[26];
        for (char c : s1.toCharArray()) freq1[c - 'a']++;

        for (int i = 0; i <= n - m; i++) {
            int[] freq2 = new int[26];
            for (int j = 0; j < m; j++) {
                freq2[s2.charAt(i+j) - 'a']++;
            }
            if (Arrays.equals(freq1, freq2)) return true;
        }
        return false;
    }
}

```

### Complexity

- Time: O((n-m+1) * 26) → O(26n)
    
- Space: O(26)
    

---

## 🟢 Approach 4: Sliding Window + Frequency Count (Optimal ✅)

### Algorithm

1. Count frequency of `s1` → `freq1[26]`.
    
2. Build frequency of first window of size `m` in `s2` → `freq2[26]`.
    
3. Compare `freq1` and `freq2`.
    
4. Slide the window across `s2`:
    
    - Add one char (right), remove one char (left).
        
    - Compare arrays at each step.
        
5. If match found → return `true`, else `false`.
    

### Dry Run

`s1 = "ab"`, `s2 = "eidbaooo"`

- `freq1 = {a:1, b:1}`
    
- Window `"ei"` → `{e:1, i:1}` ≠
    
- Window `"id"` → `{i:1, d:1}` ≠
    
- Window `"db"` → `{d:1, b:1}` ≠
    
- Window `"ba"` → `{b:1, a:1}` ✅ → return `true`.
    

### Java Code

```java
import java.util.*;

class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if (s1.length() > s2.length()) return false;

        int[] freq1 = new int[26];
        int[] freq2 = new int[26];

        for (char c : s1.toCharArray()) freq1[c - 'a']++;

        int m = s1.length();
        for (int i = 0; i < m; i++) {
            freq2[s2.charAt(i) - 'a']++;
        }

        if (Arrays.equals(freq1, freq2)) return true;

        for (int i = m; i < s2.length(); i++) {
            freq2[s2.charAt(i) - 'a']++; // add right char
            freq2[s2.charAt(i - m) - 'a']--; // remove left char
            if (Arrays.equals(freq1, freq2)) return true;
        }

        return false;
    }
}


```

### Complexity

- Time: O(n)
    
- Space: O(26) → O(1)
    

---

# 📊 Approach Comparison

|Approach|Time Complexity|Space|Interview Worth|
|---|---|---|---|
|Brute Force|O(n! * n)|O(n)|❌ Too slow|
|Sorting Substr|O((n-m+1) * m log m)|O(m)|❌ Inefficient|
|Freq Naive|O((n-m+1) * 26) ~ O(n)|O(26)|✅ Good attempt|
|Sliding Window|O(n)|O(26)|✅ Best choice|

---

# 🎯 Interview Notes

- **Pattern:** Sliding Window + Frequency Count.
    
- **Key Trick:** Permutation = Anagram. Problem reduces to finding an anagram of `s1` inside `s2`.
    
- **Strategy in Interview:**
    
    1. Start by explaining brute force (permutations).
        
    2. Improve to sorting substrings.
        
    3. Then to frequency arrays.
        
    4. Finally present sliding window as optimal.