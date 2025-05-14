## 📘 Problem: Maximum Circular Subarray Sum (Brute Force)

### 🔹 Statement:

Given an array `arr[]` of size `n`, return the **maximum sum of a subarray**, allowing the subarray to be **circular** (wrap around from end to beginning).

---

### 🧠 Idea (Brute Force Approach):

- Try every possible subarray **starting at index `i`**.
    
- For each start index, go through **all `n` elements** (wrapping around using modulo).
    
- Keep updating the maximum subarray sum found so far.
    
- This checks all `n^2` subarrays, including circular ones.
    

---

## 💡 Dry Run: `arr = [8, -1, 3, 4]`

|i|Subarray (circular from i)|Sum|
|---|---|---|
|0|[8, -1, 3, 4]|14|
|1|[-1, 3, 4, 8]|14|
|2|[3, 4, 8, -1]|**15** ✅|
|3|[4, 8, -1, 3]|14|

🔚 **Maximum circular subarray sum = 15**

### 🧪 Dry Run Example: `arr = [8, -1, 3, 4]`

- n=4n = 4n=4
    
- Start with: `res = arr[0] = 8`
    

---

#### 🔁 Outer Loop: `i = 0 to 3`

---

### ▶ i = 0

- currSum = 0
    

|j|idx = (i + j) % n|arr[idx]|currSum|res (max)|
|---|---|---|---|---|
|0|(0 + 0) % 4 = 0|8|8|8|
|1|(0 + 1) % 4 = 1|-1|7|8|
|2|(0 + 2) % 4 = 2|3|10|**10**|
|3|(0 + 3) % 4 = 3|4|14|**14**|

---

### ▶ i = 1

- currSum = 0
    

|j|idx = (1 + j) % 4|arr[idx]|currSum|res (max)|
|---|---|---|---|---|
|0|1|-1|-1|14|
|1|2|3|2|14|
|2|3|4|6|14|
|3|0|8|14|14|

---

### ▶ i = 2

- currSum = 0
    

|j|idx = (2 + j) % 4|arr[idx]|currSum|res (max)|
|---|---|---|---|---|
|0|2|3|3|14|
|1|3|4|7|14|
|2|0|8|15|**15**|
|3|1|-1|14|15|

---

### ▶ i = 3

- currSum = 0
    

|j|idx = (3 + j) % 4|arr[idx]|currSum|res (max)|
|---|---|---|---|---|
|0|3|4|4|15|
|1|0|8|12|15|
|2|1|-1|11|15|
|3|2|3|14|15|

---

### ✅ Final Answer:

`return res = 15;`

---

### 💡 Explanation:

The code checks **all possible circular subarrays** using brute force. It handles circular indexing using:

**`int idx = (i + j) % n;`**

---

## 💻 Java Code

```java
public class CircularSubarraySum {
    static int circularSubarraySum(int[] arr) {
        int n = arr.length;

        // Initialize result with the first element
        int res = arr[0];

        // Loop over each index as a starting point
        for (int i = 0; i < n; i++) {
            int currSum = 0;

            for (int j = 0; j < n; j++) {
                // Wrap around using modulo for circular index
                int idx = (i + j) % n;

                // Add current element to running sum
                currSum += arr[idx];

                // Update result if current sum is greater
                res = Math.max(res, currSum);
            }
        }

        return res;
    }
```
---

## 📈 Time & Space Complexity

| Type  | Value |
| ----- | ----- |
| Time  | O(n²) |
| Space | O(1)  |
>

**Efficient Approach**

# Intuition

I guess you know how to solve max subarray sum (without circular).  
If not, you can have a reference here: 53. Maximum Subarray  
  
# Explanation

So there are two case.  
**Case 1**. The first is that the subarray take only a middle part, and we know how to find the max subarray sum.  
**Case2**. The second is that the subarray take a part of head array and a part of tail array.  
We can transfer this case to the first one.  
The maximum result equals to the total sum minus the minimum subarray sum.  

![image](https://assets.leetcode.com/users/motorix/image_1538888300.png)

So the max subarray circular sum equals to  
circularMax=totalSum-minSubArraySum;
  
# Corner case

When all elements in the array are negative, the total sum (`tSum`) and the minimum subarray sum (`kadaneMin(nums)`) are equal. This causes `circularMax = tSum - minSubArraySum` to become `0`, which is incorrect since a non-empty subarray must be chosen.

#### **Example Case:**

Given `nums = [-3, -2, -3]`:

- `kadaneMax(nums) = -2` (best non-circular subarray)
    
- `kadaneMin(nums) = -8` (entire array)
    
- `tSum = -8`
    
- `circularMax = tSum - kadaneMin = -8 - (-8) = 0` → **Incorrect!**
    

#### **Fix:**

Instead of blindly taking `Math.max(normalMax, circularMax)`, 
ensure circularMax is valid:
```
return (circularMax == 0) ? normalMax : Math.max(normalMax, circularMax);

```

**code**

```java
class Solution {
    public int maxSubarraySumCircular(int[] nums) {
        int n = nums.length;

        // Step 1: Find max subarray sum using standard Kadane's algorithm
        int normalMax = kadaneMax(nums);

        // Step 2: Find min subarray sum (to calculate circular max)
        int minSubArraySum = kadaneMin(nums);

        // Step 3: Total sum of the array
        int tSum = 0;
        for (int i = 0; i < n; i++)
            tSum += nums[i];

        // Step 4: Max circular subarray sum = total sum - min subarray sum
        int circularMax = tSum - minSubArraySum;

        // Step 5: If all elements are negative, circularMax becomes 0 (invalid)
        return (circularMax == 0) ? normalMax : Math.max(normalMax, circularMax);
    }

    // Standard Kadane's algorithm to find maximum subarray sum
    public int kadaneMax(int[] nums) {
        int maxSum = Integer.MIN_VALUE;
        int sum = 0;

        for (int i = 0; i < nums.length; i++) {
            if (sum < 0)
                sum = nums[i];
            else
                sum += nums[i];

            maxSum = Math.max(sum, maxSum);
        }

        return maxSum;
    }

    // Modified Kadane's algorithm to find minimum subarray sum
    public int kadaneMin(int[] nums) {
        int minSum = Integer.MAX_VALUE;
        int sum = 0;

        for (int i = 0; i < nums.length; i++) {
            if (sum > 0)
                sum = nums[i];     // start new subarray
            else
                sum += nums[i];    // extend previous subarray

            minSum = Math.min(sum, minSum);
        }

        return minSum;
    }
}

```

