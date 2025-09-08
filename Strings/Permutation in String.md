


















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
```

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