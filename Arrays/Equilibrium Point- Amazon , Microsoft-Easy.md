Given an array ****arr[]**** of size ****n****, the task is to return an ****equilibrium**** ****index**** (if any) or ****-1**** if no equilibrium index exists. The ****equilibrium index of an array**** is an index such that the sum of all elements at lower indexes equals the sum of all elements at higher indexes.

****Note:**** When the index is at the start of the array, the left sum is 0, and when it's at the end, the right sum is 0.

****Examples:****

> ****Input:**** arr[] = [1, 2, 0, 3]  
> ****Output:**** 2  
> ****Explanation:**** The sum of left of index 2 is 1 + 2 = 3 and sum on right of index 2 is 3.
> 
> ****Input:**** arr[] = [1, 1, 1, 1]  
> ****Output****: -1  
> ****Explanation:**** There is no equilibrium index in the array.
> 
> ****Input****: arr[] = [-7, 1, 5, 2, -4, 3, 0]  
> ****Output****: 3  
> ****Explanation:**** The sum of left of index 3 is -7 + 1 + 5 = -1 and sum on right of index 3 is -4 + 3 + 0 = -1.

-------------------------------------------------
**Solution**

precompute the [prefix sum array](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) and [suffix sum array](https://www.geeksforgeeks.org/suffix-sum-array/), and simply access this in O(1) time.

So for each index i, we can check if prefixSum[i - 1] = suffixSum[i + 1] but to avoid unnecessary boundary checks we can also check if prefixSum[i] = suffixSum[i].

```java
  static int findEquilibrium(int[] arr) {
        int n = arr.length;

        int[] pref = new int[n];
        int[] suff = new int[n];

        // Initialize the ends of prefix and suffix array
        pref[0] = arr[0];
        suff[n - 1] = arr[n - 1];

        // Calculate prefix sum for all indices
        for (int i = 1; i < n; i++) 
            pref[i] = pref[i - 1] + arr[i];

        // Calculating suffix sum for all indices
        for (int i = n - 2; i >= 0; i--) 
            suff[i] = suff[i + 1] + arr[i];

        // Checking if prefix sum is equal to suffix sum
        for (int i = 0; i < n; i++) {
            if (pref[i] == suff[i]) 
                return i;
        }

        // if equilibrium index doesn't exist
        return -1;
    }
```