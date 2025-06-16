```java


// Function to locate the first occurrence of the pattern in the text using brute force
int firstOccurence(String txt, String pat) {
    int patLen = pat.length(); // Length of pattern
    int strLen = txt.length(); // Length of text
    int flag = -1; // Flag to track if match is found in current window

    // Loop through each possible starting index where pattern can fit
    for (int i = 0; i <= strLen - patLen; i++) { // FIXED: <= instead of <
        
        // For each starting index, check if the substring matches the pattern
        for (int j = 0; j < patLen; j++) {
            if (txt.charAt(i + j) != pat.charAt(j)) {
                // If any character does not match, break and mark flag as -1
                flag = -1;
                break;
            } else {
                // If current character matches, mark flag as 0
                flag = 0;
            }
        }

        // If flag is 0 after checking full pattern, it means full match found
        if (flag == 0)
            return i; // Return starting index of first occurrence
    }

    // If no match found in the entire text
    return -1;
}

```

## ⚡ **Better (optimized) approach**

**Brute force** has **time complexity O(N*M)** where:

- `N` = length of text
    
- `M` = length of pattern
    

**Better algorithms** reduce it to **O(N)** in most cases. The most famous is **KMP (Knuth-Morris-Pratt)**.

✅ **Idea of KMP:**

- Preprocess pattern to build a **Longest Prefix Suffix (LPS)** array.
    
- When a mismatch happens, instead of rechecking from scratch, reuse info in LPS to skip redundant comparisons.


**Java code for KMP:**
```java
// Function to find first occurrence using KMP algorithm
int firstOccurrenceKMP(String txt, String pat) {
    int N = txt.length();
    int M = pat.length();

    // Step 1: Build LPS array for the pattern
    int[] lps = new int[M];
    int len = 0;
    lps[0] = 0; // LPS[0] is always 0

    int i = 1;
    while (i < M) {
        if (pat.charAt(i) == pat.charAt(len)) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) {
                len = lps[len - 1];
                // Do not increment i here
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }

    // Step 2: Use LPS to search the pattern in text
    i = 0; // index for txt
    int j = 0; // index for pat

    while (i < N) {
        if (pat.charAt(j) == txt.charAt(i)) {
            i++;
            j++;
        }
        if (j == M) {
            return i - j; // Found pattern at i - j
        } else if (i < N && pat.charAt(j) != txt.charAt(i)) {
            if (j != 0) {
                j = lps[j - 1];
            } else {
                i++;
            }
        }
    }

    return -1; // Not found
}

```
