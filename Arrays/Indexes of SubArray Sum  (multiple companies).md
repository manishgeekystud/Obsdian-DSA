

Given an array of non-negative integers `arr[]` and a value `target`, find the **starting and ending indexes (1-based)** of a **continuous subarray** that adds up to the `target`.

If no such subarray is found, return `[-1]`.

**Examples:**

**Input:** arr[] = [1, 2, 3, 7, 5], target = 12
**Output:** [2, 4]
**Explanation:** The sum of elements from 2nd to 4th position is 12.

**Input:** arr[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], target = 15
**Output:** [1, 5]
**Explanation:** The sum of elements from 1st to 5th position is 15.

**Input:** arr[] = [5, 3, 4], target = 2
**Output:** [-1]
There is no subarray with sum 2.

**Explanation:** 
---

## ✅1 .🔍 Approach: Two Pointer / Sliding Window

### 💡 Intuition:
- For **non-negative integers**, the sum of a subarray will **only increase** when we move the right pointer forward.
- If the sum exceeds the target, move the **left** pointer to shrink the window.
- Efficient because we never reprocess the same elements (O(n) time).

---

## 🛠️ Steps:

1. Initialize:
   - `left = 0`, `currentSum = 0`
2. Iterate `right` from 0 to end of array:
   - Add `arr[right]` to `currentSum`
   - While `currentSum > target`, subtract `arr[left]` and move `left++`
   - If `currentSum == target`, return `[left+1, right+1]`
3. If no match is found, return `[-1]`

---

## ✅ Java Code

```java
static ArrayList<Integer> subarraySum(int[] arr, int target) {
    int left = 0;
    int right = 0;
    int n = arr.length;
    int currentSum = 0;
    ArrayList<Integer> ans = new ArrayList<>();

    for (right = 0; right < n; right++) {
        currentSum += arr[right];

        // Shrink window from left if sum exceeds target
        while (currentSum > target && left <= right) {
            currentSum -= arr[left++];
        }

        // Match found
        if (currentSum == target) {
            ans.add(left + 1);   // 1-based indexing
            ans.add(right + 1);
            return ans;
        }
    }

    ans.add(-1);
    return ans;
}
```


## 🧪 Dry Run Example

Input: `arr = [1, 2, 3, 7, 5]`, `target = 12`

### Steps:

```
left = 0, right = 0, currentSum = 0

right = 0 → currentSum = 1
right = 1 → currentSum = 3
right = 2 → currentSum = 6
right = 3 → currentSum = 13 (too much)
    → currentSum -= arr[0] (1) → currentSum = 12
Match found → left = 1, right = 3 → return [2, 4]

```
---

## 🧠 Notes:

- This algorithm works **only when elements are non-negative**.
    
- Time complexity: `O(n)`
    
- Space complexity: `O(1)`
    
- For arrays with negative numbers, use **prefix sum with HashMap**.
    

---

## 🧩 Related Variations

- Count number of subarrays with sum `k` → use HashMap + Prefix Sum
    
- Longest subarray with given sum
    
- Smallest subarray with sum ≥ k (uses similar logic)
    
## ✅ 2. **Prefix Sum + HashMap** – `O(n)`

> **Works with negative numbers also**

## ✅ Problem Statement
Given an array `arr[]`, find the **starting and ending index (1-based)** of a subarray whose sum is equal to a given `target`.

> The array may contain **negative numbers**, so sliding window won't always work.

---

## 🔍 Core Idea (Prefix Sum + HashMap)

- Maintain a **running prefix sum**.
- Store the **first occurrence** of each prefix sum in a HashMap.
- If `prefixSum - target` is found in the map, the subarray between those indexes adds up to `target`.

---

## 🧮 Mathematical Insight

Let:
- `prefixSum[i]` be the sum of all elements from index `0` to `i`.
- If there's a previous prefix sum `prefixSum[j]` such that:

prefixSum[i] - prefixSum[j] == target  
⇒ subarray from j+1 to i adds to target


So, check if `prefixSum - target` exists in the map.

---

## 🧪 Dry Run Example

```text
Input: arr = [10, 2, -2, -20, 10], target = -10

Step-by-step:
- i = 0 → prefixSum = 10   → map: {10: 0}
- i = 1 → prefixSum = 12   → map: {10: 0, 12: 1}
- i = 2 → prefixSum = 10   → already exists, skip
- i = 3 → prefixSum = -10  → prefixSum == target → return [1, 4]


---

## 🧠 Comparison of Two `O(n)` Approaches

|Approach|Handles Negatives|Space|Extra Structure|
|---|---|---|---|
|Sliding Window|❌|`O(1)`|None|
|Prefix Sum + HashMap|✅|`O(n)`|HashMap|

---

## ⚡ When to Use Which:

- **Non-negative elements only** → use **Sliding Window**
    
- **Possible negative numbers** → use **Prefix Sum + HashMap**
###### 

 CODE
 
static ArrayList<Integer> subarraySum(int[] arr, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    int prefixSum = 0;
    ArrayList<Integer> ans = new ArrayList<>();

    for (int i = 0; i < arr.length; i++) {
        prefixSum += arr[i];

        if (prefixSum == target) {
            ans.add(1);           // 1-based indexing
            ans.add(i + 1);
            return ans;
        }

        if (map.containsKey(prefixSum - target)) {
            ans.add(map.get(prefixSum - target) + 2); // +2 for 1-based
            ans.add(i + 1);
            return ans;
        }

        map.putIfAbsent(prefixSum, i);
    }

    ans.add(-1);
    return ans;
}
