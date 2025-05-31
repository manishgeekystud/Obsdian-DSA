Given an array containing 0s and 1s. Find the number of subarrays having equal number of 0s and 1s.

**Example 1:**

**Input:**
n = 7
A[] = {1,0,0,1,0,1,1}
**Output:** 8
**Explanation:** The index range for the 8 
sub-arrays are: (0, 1), (2, 3), (0, 3), (3, 4), 
(4, 5) ,(2, 5), (0, 5), (1, 6)

**Example 2:**

**Input:**
n = 5
A[] = {1,1,1,1,0}
**Output:** 1
**Explanation:** The index range for the 
subarray is (3,4).

**Your Task:**  
You don't need to read input or print anything. Your task is to complete the function **countSubarrWithEqualZeroAndOne()** which takes the array arr[] and the size of the array as inputs and returns the number of subarrays with equal number of 0s and 1s.

----------------------------------------------------------------------------
## 🧠 **Key Insight**

The problem becomes easier if we **convert all 0s to -1s**.

### 🔁 Why?

After converting:

- A subarray with **equal number of 0s and 1s** will have a total sum of **0**.
    

---

## 🔧 **Steps to Solve**

### 1. **Convert**:

Replace every `0` in the array with `-1`.

### 2. **Prefix Sum**:

Calculate running prefix sums of the array.

### 3. **HashMap**:

Use a `HashMap` to store the frequency of each prefix sum.

### 4. **Logic**:

If a prefix sum is repeated, it means the subarray between the repeated indices has sum `0` ⇒ **equal 0s and 1s**.

---

## ✅ **Efficient Java Code**
```java
public int countSubarrWithEqualZeroAndOne(int[] arr, int n) {
    // Step 1: Convert 0s to -1s
    for (int i = 0; i < n; i++) {
        if (arr[i] == 0) arr[i] = -1;
    }

    // Step 2: HashMap to store prefix sum frequencies
    HashMap<Integer, Integer> map = new HashMap<>();
    int preSum = 0, count = 0;

    map.put(0, 1);  // Base case: prefix sum 0 has one occurrence

    // Step 3: Iterate and calculate prefix sums
    for (int i = 0; i < n; i++) {
        preSum += arr[i];

        // Step 4: If prefix sum seen before, add its frequency to count
        count += map.getOrDefault(preSum, 0);

        // Step 5: Update the frequency of current prefix sum
        map.put(preSum, map.getOrDefault(preSum, 0) + 1);
    }

    return count;
}

```
## 🔍 **Example**

### Input:

`arr = [1, 0, 0, 1, 0, 1, 1]`

### After conversion:

`[1, -1, -1, 1, -1, 1, 1]`

### Prefix Sums:

`[1, 0, -1, 0, -1, 0, 1]`

### Matching prefix sums (same values at different indices) show where subarrays with sum = 0 exist.

Total subarrays with equal number of 0s and 1s = **8**

---

## 📝 Recap Table

|Concept|Description|
|---|---|
|Convert `0` → `-1`|So we can treat the problem as sum = 0|
|Use `prefix sum`|Track cumulative sums|
|HashMap of prefix sum freq|Detect & count zero-sum subarrays|
|Time Complexity|`O(n)`|
|Space Complexity|`O(n)`|