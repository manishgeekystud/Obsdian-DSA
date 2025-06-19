
# 📌 **KMP (Knuth-Morris-Pratt) String Matching — Complete Cheat Sheet**

---

## ✅ **Goal**

Find all occurrences of a **pattern** inside a **text** efficiently, in **linear time O(N + M)**.

---

## ⚙️ **Core Idea**

- When a mismatch happens, don’t restart from scratch.
    
- Use what you know about the pattern itself:  
    **Reuse previous matches!**
    
- This is done using the **LPS array**.
    

---

## 🔑 **Key Term: LPS (Longest Prefix Suffix)**

**Definition:**  
For every position in the pattern, store the length of the **longest proper prefix** that is also a suffix **up to that point**.

**Example:**  
Pattern: `A B A B A C`  
Index: `0 1 2 3 4 5`  
LPS: `[0 0 1 2 3 0]`

**Meaning:**

- At index 4 (`ABABA`): the longest prefix that is also suffix is `ABA` → length = 3.
    

---

## 📑 **Why LPS works**

Imagine matching `ABABA` with text:

- You’ve matched `ABAB`, next is `C` vs `A`. Mismatch!
    
- Instead of starting over, LPS tells you:
    
    - You already know the prefix `ABA` repeats — so slide back only to `A` instead of starting from 0.
        

This skips redundant checks!

---

## ⚡ **KMP in Two Steps**

---

## ✅ **Step 1 — Build LPS Array**

### 👉 **How**

1. Start with first character: `lps[0] = 0`.
    
2. For each next character:
    
    - If it matches the current prefix, extend prefix length.
        
    - If not, shorten prefix to previous best and try again.
        

### 📌 **Java Code — LPS**

```java
void computeLPS(String pat, int[] lps) {
    int len = 0; // current longest prefix which is also suffix
    lps[0] = 0;  // always 0 for first char

    int i = 1; // start from second char
    while (i < pat.length()) {
        if (pat.charAt(i) == pat.charAt(len)) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) {
                // Try shorter prefix
                len = lps[len - 1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
}

```

---

## ✅ **Step 2 — Search Pattern in Text Using LPS**

### 👉 **How**

- Compare text and pattern:
    
    - If match → move both indices.
        
    - If complete match → record match, use LPS to continue.
        
    - If mismatch → use LPS to know where to continue in the pattern.
        
- **NEVER backtrack in the text!**
    

### 📌 **Java Code — Search**
```java
void KMPSearch(String pat, String txt) {
    int M = pat.length();
    int N = txt.length();

    int[] lps = new int[M];
    computeLPS(pat, lps);

    int i = 0; // index for text
    int j = 0; // index for pattern

    while (i < N) {
        if (pat.charAt(j) == txt.charAt(i)) {
            i++;
            j++;
        }

        if (j == M) {
            // Found pattern at i - j
            System.out.println("Pattern found at index " + (i - j));
            // Check for next match
            j = lps[j - 1];
        } else if (i < N && pat.charAt(j) != txt.charAt(i)) {
            if (j != 0) {
                j = lps[j - 1]; // use LPS to skip
            } else {
                i++; // move in text only
            }
        }
    }
}

```

## 📊 **Time Complexity**

|Step|Time|
|---|---|
|Build LPS|O(M)|
|Search|O(N)|
|**Total**|**O(N + M)**|

---

## ✅ **When to Use KMP**

- To search for a substring in a big text efficiently.
    
- DNA sequence matching.
    
- Plagiarism detection.
    
- Search engines.
    
- Efficient “areRotations” check.
    

---

## 🔑 **Quick Recap**

1️⃣ **Build LPS:**

- Stores for each position: longest prefix = suffix.
    
- Helps you skip re-checking.
    

2️⃣ **Search:**

- Compare pattern and text.
    
- On mismatch → jump back in pattern using LPS.
    
- No backtracking in text!
    

---

## 📌 **Example**

| Text: | A B A B A B C A B A B A B |  
| Pattern: | A B A B |

**You find matches at positions:**  
0, 2, 8.

---

## 🔗 **Related**

- KMP vs Naive: Naive is O(NM), KMP is O(N + M)
    
- Other fast algorithms: Rabin-Karp, Z-algorithm, Boyer-Moore.
    

---

## 🚀 **One-liner to remember**

**KMP = Preprocess pattern → reuse matches → linear time!**

---

If you want, I can also share:  
✅ A step-by-step dry run,  
✅ A full Java program with input & output,  
✅ Or a practice problem.

**Just say “Yes!”** 🔥

##### You said:

make it markdown format

###### ChatGPT said:

Absolutely! Here’s your detailed **KMP Algorithm Guide** rewritten in clean **Markdown** — copy this and you’ll always have a clear reference.

---

