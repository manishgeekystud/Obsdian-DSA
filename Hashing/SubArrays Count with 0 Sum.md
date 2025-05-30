You are given an array **arr[]** of integers. Find the total count of subarrays with their sum equal to 0.

**Examples:**

**Input:** arr[] = [0, 0, 5, 5, 0, 0]
**Output:** 6
**Explanation:** The 6 subarrays are [0], [0], [0], [0], [0,0], and [0,0].

**Input:** arr[] = [6, -1, -3, 4, -2, 2, 4, 6, -12, -7]
**Output:** 4
**Explanation:** The 4 subarrays are [-1, -3, 4], [-2, 2], [2, 4, 6, -12], and [-1, -3, 4, -2, 2]

**Input:** arr[] = [0]
**Output:** 1
**Explanation:** The only subarray is [0].

```java
public int findSubarray(int[] arr) {
    // HashMap to store frequency of prefix sums
    HashMap<Integer, Integer> map = new HashMap<>();
    
    int preSum = 0, count = 0;

    // Add 0 to handle the case where a subarray starting from index 0 has sum = 0
    map.put(0, 1);

    for (int n : arr) {
        preSum += n;  // Compute the running sum (prefix sum)

        // If this sum has been seen before, it means some subarrays sum to 0
        count += map.getOrDefault(preSum, 0);

        // Update the frequency of the current prefix sum
        map.put(preSum, map.getOrDefault(preSum, 0) + 1);
    }

    return count;
}

```

### 🧠 Key Concepts

#### 1. **Prefix Sum (preSum)**

- `preSum` keeps track of the sum from index `0` to current element.
    
- Example: If `arr = [1, 2, -3]`, the prefix sums would be `[1, 3, 0]`.
    

#### 2. **How does it detect subarrays with sum = 0?**

- Suppose you have two indices `i` and `j` (`i < j`) where `preSum[i] == preSum[j]`.
    
- That means the **sum of the subarray from (i+1 to j)** is `0`.
    

#### 3. **Why use a HashMap?**

- The HashMap stores how many times each prefix sum has occurred.
    
- If a prefix sum occurs **k times**, there are **k** different subarrays that sum to `0` ending at the current index.
    

---

### 🔍 Line-by-Line Explanation

#### `HashMap<Integer, Integer> map = new HashMap<>();`

- Creates a map to store prefix sum → count of how many times it occurred.
    

#### `map.put(0, 1);`

- We add an initial entry so we can count subarrays starting from index 0.
    
    - For example, if `preSum == 0` at index `2`, that means `[0..2]` has sum 0.
        

#### `for (int n : arr)`

- Loop through the array elements.
    

#### `preSum += n;`

- Update the running sum.
    

#### `count += map.getOrDefault(preSum, 0);`

- If the `preSum` has been seen before, it means we found 1 or more subarrays ending here that sum to `0`.
    
- So we **add that count to the total answer**.
    

#### `map.put(preSum, map.getOrDefault(preSum, 0) + 1);`

- Record that we've seen this `preSum` one more time.
    

---

### 🧾 Example Walkthrough

Input:
`arr = [1, -1, 2, -2, 3]`

Prefix sums:


`[1, 0, 2, 0, 3]`

HashMap updates and counts:

ini

CopyEdit

`preSum = 1 → map = {0:1, 1:1} preSum = 0 → found! map.get(0) = 1 → count = 1 → map = {0:2, 1:1} preSum = 2 → map = {0:2, 1:1, 2:1} preSum = 0 → found! map.get(0) = 2 → count = 3 → map = {0:3, 1:1, 2:1} preSum = 3 → map = {0:3, 1:1, 2:1, 3:1}`

So total subarrays with sum = 0 = **3**

---

### ✅ Final Summary

|Feature|Description|
|---|---|
|Uses prefix sums|To track cumulative sum up to current index|
|Uses HashMap|To store frequency of each prefix sum|
|Key insight|Repeated prefix sum ⇒ zero-sum subarray|
|Time complexity|O(n)|
|Space complexity|O(n)|