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

