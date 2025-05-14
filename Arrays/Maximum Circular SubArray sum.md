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

```
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