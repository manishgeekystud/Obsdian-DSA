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

---

## ✅ Final Answer:

java

CopyEdit

`Output: 15`

---

## 💻 Java Code with Comments

java

CopyEdit

`public class CircularSubarraySum {     static int circularSubarraySum(int[] arr) {         int n = arr.length;          // Initialize result with the first element         int res = arr[0];          // Loop over each index as a starting point         for (int i = 0; i < n; i++) {             int currSum = 0;              // Check subarray of length n starting at i             for (int j = 0; j < n; j++) {                 // Wrap around using modulo for circular index                 int idx = (i + j) % n;                  // Add current element to running sum                 currSum += arr[idx];                  // Update result if current sum is greater                 res = Math.max(res, currSum);             }         }          return res;     }      public static void main(String[] args) {         int[] arr = {8, -1, 3, 4};         System.out.println("Max Circular Subarray Sum: " + circularSubarraySum(arr));     } }`

---

## 📈 Time & Space Complexity

| Type  | Value |
| ----- | ----- |
| Time  | O(n²) |
| Space | O(1)  |