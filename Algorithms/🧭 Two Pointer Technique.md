
### 📌 What is the Two Pointer Technique?

**Two Pointers** is an efficient algorithmic technique used to solve problems involving:

- Searching
    
- Sorting
    
- Traversing arrays or strings
    
- Finding pairs or subarrays with certain properties
    

✅ It involves maintaining **two indices** (pointers) that move through the data structure, often from opposite directions or in a sliding window fashion.

---

### 📦 Typical Use Cases

|Problem Type|Example|
|---|---|
|**Sorted arrays**|Pair with sum X, Remove duplicates|
|**Strings**|Palindrome check, Longest substring|
|**Linked lists**|Cycle detection, Find midpoint|
|**Subarrays/windows**|Maximum sum of subarray, Longest subarray with sum ≤ K|
|**Merging**|Merging two sorted arrays|

---

### 🧠 Variants of Two Pointer

#### 1. **Opposite Ends**

- One pointer starts at beginning, the other at end.
    
- Used when input is **sorted**.
    
- 🔄 Pointers move towards each other.
```java
int[] arr = {1, 2, 3, 4, 5};
int left = 0, right = arr.length - 1;
while (left < right) {
    int sum = arr[left] + arr[right];
    if (sum == target) return true;
    else if (sum < target) left++;
    else right--;
}

```

✅ Example:


---

#### 2. **Sliding Window (Same Direction)**

- Both pointers start at beginning and move forward.
    
- Used when dealing with **subarrays or substrings**.
    
- One pointer expands window, the other shrinks it based on conditions.
    

✅ Example:

```java
int left = 0, sum = 0;
for (int right = 0; right < arr.length; right++) {
    sum += arr[right];
    while (sum > target) {
        sum -= arr[left];
        left++;
    }
}

```

---

#### 3. **Slow & Fast Pointer**

- Common in **Linked List problems**.
    
- Slow moves one step, fast moves two.
    

✅ Use cases:

- Detecting a cycle
    
- Finding the middle of a linked list
    

---

### 🚀 Why Use Two Pointers?

|Benefit|Explanation|
|---|---|
|✅ Efficient|Often reduces time complexity from `O(n²)` to `O(n)`|
|✅ Space optimized|Typically uses constant space|
|✅ Elegant|Clean and readable code for sequence-based problems|

---

### 🔍 Common Problems to Practice

1. **Two Sum in sorted array** – Leetcode 167
    
2. **3Sum / 4Sum** – Leetcode 15, 18
    
3. **Container With Most Water** – Leetcode 11
    
4. **Move Zeroes** – Leetcode 283
    
5. **Remove Duplicates from Sorted Array** – Leetcode 26
    
6. **Trapping Rain Water** – Leetcode 42 (advanced two-pointer)
    
7. **Longest Substring Without Repeating Characters** – Leetcode 3
    
8. **Minimum Size Subarray Sum** – Leetcode 209
    
9. **Palindrome Check** – Left/right pointer approach
    

---

### 🧾 Template Snippet

#### Opposite ends (Sorted Array):
```
int left = 0, right = arr.length - 1;
while (left < right) {
    // do something
    if (condition) right--;
    else left++;
}

```


#### Sliding window:


---

### 💡 Tips

- Always check if the array/string is **sorted** – helps decide pointer strategy.
    
- Think of how the pointers interact:  
    → Expanding, shrinking, comparing, or merging?
    
- For strings, use `char[]` to avoid extra overhead when comparing characters.