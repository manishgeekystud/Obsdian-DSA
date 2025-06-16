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