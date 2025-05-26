### Problem Statement:

> Given an array `arr[]`, check if there exists a triplet `(i, j, k)` such that `arr[i] + arr[j] + arr[k] == 0`.

---

## 🧠 Intuition

- Sort the array.
    
- Fix one element at a time (say `arr[i]`) and use **two pointers** to find the remaining two elements such that their sum is `-arr[i]`.
    
## 🔍 Approach

### 🔧 Technique: Sorting + Two-Pointer

1. **Sort the array** to use the two-pointer technique efficiently.
    
2. Fix one element `arr[i]` in the outer loop.
    
3. Use two pointers:
    
    - `l = i + 1` (immediately after `i`)
        
    - `r = n - 1` (end of the array)
        
4. Check the sum of the triplet:
    
    - If `sum == 0` → Triplet found.
        
    - If `sum < 0` → Move `l` to the right to increase the sum.
        
    - If `sum > 0` → Move `r` to the left to decrease the sum.
---

## ✅ Java Code

```java
public boolean findTriplets(int[] arr) {
    int n = arr.length;

    // Step 1: Sort the array
    Arrays.sort(arr);

    // Step 2: Iterate through the array
    for (int i = 0; i < n - 2; i++) {
        int l = i + 1;
        int r = n - 1;

        // Step 3: Two-pointer traversal
        while (l < r) {
            int sum = arr[i] + arr[l] + arr[r];

            if (sum == 0) {
                // Triplet found
                return true;
            } else if (sum < 0) {
                // Increase sum by moving left pointer to the right
                l++;
            } else {
                // Decrease sum by moving right pointer to the left
                r--;
            }
        }
    }

    // No triplet found with zero sum
    return false;
}

```