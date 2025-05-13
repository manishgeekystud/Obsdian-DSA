Given an integer array `nums`, find the subarray with the largest sum, and return _its sum_.

**Example 1:**

**Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]
**Output:** 6
**Explanation:** The subarray [4,-1,2,1] has the largest sum 6.

**Example 2:**

**Input:** nums = [1]
**Output:** 1
**Explanation:** The subarray [1] has the largest sum 1.

**Example 3:**

**Input:** nums = [5,4,-1,7,8]
**Output:** 23
**Explanation:** The subarray [5,4,-1,7,8] has the largest sum 23.

**Brute Force**
1. **Try all possible subarrays**:
    - Start from every index `i`.
    - From each `i`, keep adding elements one by one (`j = i+1 to n`).
        
2. **Track the max sum**:
    - For every subarray sum, update `maxSum` if it's the biggest so far.
        
3. **Why `Integer.MIN_VALUE`?**
    - To make sure we catch the max even if **all numbers are negative**.
    -
```
public int maxSubArray(int[] nums){
 int maxSum = Integer.MIN_VALUE;
 for (int i = 0; i < n; i++) {
    int sum = nums[i];                // Start a new subarray from index i
    maxSum = Math.max(maxSum, sum);   // Fix single element (to add further)
    for (int j = i + 1; j < n; j++) {
        sum += nums[j];               // Extend subarray
        maxSum = Math.max(maxSum, sum); // Update max
    }
}
  return maxSum;
}
```

**Efficient Solution**

  refer Kadane ALgo
  
### 🧠 **Concept Breakdown (Kadane’s Algorithm)**

1. **Running Sum (sum)**:
    
    - **Accumulate** the sum as we iterate.
        
    - If the running sum is **negative**, **reset** it to the current element `A[i]`.
        
        - (Why? A negative sum will only reduce the sum of the next elements.)
            
2. **Update Max**:
    
    - At each step, **compare** the current sum with `max` and update `max` if needed.
        
3. **Final Answer**:
    
    - `max` will store the largest sum of any subarray found.
        

---

### 🪄 **Code Structure & Logic**

```
public class Solution {
    public int maxSubArray(int[] A) {
        int max = Integer.MIN_VALUE;  // To handle negative-only arrays
        int sum = 0;  // Running sum for the subarray

        for (int i = 0; i < A.length; i++) {
            if (sum < 0) 
                sum = A[i];  // If sum is negative, start fresh from current element
            else 
                sum += A[i]; // Otherwise, add current element to the sum

            if (sum > max)  // Update max if the current sum is larger
                max = sum;
        }
        return max;  // Return the largest sum found
    }
}

```

---

### 📌 **Key Points to Remember**

1. **`sum < 0` logic**:
    
    - If the **running sum** is negative, **discard** it (because continuing with a negative sum will lower the total). Start fresh with the current element.
        
2. **Efficient**:
    
    - **O(n)** time complexity — One loop to go through the array, making this solution efficient for large arrays.
        
3. **Why `max = Integer.MIN_VALUE`**?
    
    - This handles arrays that may contain only negative numbers and ensures the correct maximum sum is returned.
        
4. **Sum Tracking**:
    
    - **`sum`** keeps track of the current subarray sum. If it turns negative, it’s reset.
        
    - **`max`** holds the best (maximum) sum found.
        

---

### 🧩 **Remember the Flow Like This**:

- **Sum**: Add numbers together (unless the sum is negative, then restart).
- **Max**: Always check if the current sum is greater than the previous best sum.
    
---

### 📍 **Quick Tips**:

- Think: **"Reset the sum when it’s negative, and keep track of the maximum found."**
  - This solution works efficiently for both **positive** and **negative** numbers.
  - Ideal for problems requiring **maximum subarray sum** in linear time.




