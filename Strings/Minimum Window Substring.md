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

