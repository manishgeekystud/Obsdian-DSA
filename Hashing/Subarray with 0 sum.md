Given an array of integers, **arr[]**. Find if there is a **subarray** (of size at least one) with **0 sum**. Return true/false depending upon whether there is a subarray present with 0-sum or not. 

**Examples:**

**Input:** arr[] = [4, 2, -3, 1, 6]
**Output:** true
**Explanation:** 2, -3, 1 is the subarray with a sum of 0.

**Input:** arr = [4, 2, 0, 1, 6]
**Output:** true
**Explanation:** 0 is one of the element in the array so there exist a subarray with sum 0.

**Input:** arr = [1, 2, -1]
**Output:** false

------------------------------------------------------------------------
```java
class Solution {
    // Function to check whether there is a subarray present with 0-sum or not.
    static boolean findsum(int arr[]) {
        // Create a HashSet to store prefix sums
        HashSet<Integer> hs = new HashSet<>();
        int preSum = 0;

        // Add 0 initially to handle case where subarray starts from index 0
        hs.add(preSum);

        // Traverse the array
        for (int n : arr) {
            preSum += n;

            // 🔑 KEY LINE:
            // If preSum already exists in the set,
            // it means there is a subarray with sum = 0
            if (!hs.add(preSum))
                return true;
        }

        // No zero-sum subarray found
        return false;
    }
}

```

### 🧠 **How It Works (Core Idea)**

- **Prefix sum**: Sum of elements from start to current index.
    
- If **any prefix sum repeats**, then the subarray between those two indices has **sum = 0**.
    
- Example:
    
    - If prefix sum is `6` at index `i` and again `6` at index `j`, then elements from `i+1` to `j` sum to `0`.
        

---

### 🔑 **Key Line Explanation:**


`if (!hs.add(preSum))     return true;`

- `hs.add(preSum)` tries to add the current prefix sum.
    
- If it **fails** (returns `false`), the prefix sum **already existed**.
    
- This means:
    
    > **A subarray with sum = 0 exists**, between two indices with the same prefix sum.

### ✅ Core Rule:

`preSum[i] == preSum[j], i < j`

Then:
`sum(i+1 to j) == 0`

So when you do:

`if (!hs.add(preSum)) return true;`

You're asking:

> Have I seen this exact sum **before**?

- If yes → the values between those two positions **must sum to zero**.
    

---

### 🧠 Visual Summary:

`[4, 2, -3, 1, 6]    
     ↑          ↑      |    
 |     same preSum → subarray between these is zero`

---

### 🧾 Notes Summary:

- ✅ Uses prefix sum and `HashSet` to detect duplicates.
    
- ✅ Efficient: **O(n)** time, **O(n)** space.