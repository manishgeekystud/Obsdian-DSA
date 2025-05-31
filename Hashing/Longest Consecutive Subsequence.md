## ✅ Problem Statement

> Given an **unsorted array of integers**, find the **length of the longest sequence of consecutive elements** (not necessarily contiguous).

### Example:

Input:  [100, 4, 200, 1, 3, 2] 
Output: 4  
Explanation: The longest consecutive sequence is [1, 2, 3, 4]`

## ❌ Brute Force Approach

### 🔹 Idea:

- Sort the array → O(n log n)
    
- Traverse and count streaks
    

### 🔻 Drawback:

- Not O(n) — may TLE for large inputs
    

---

## ✅ Optimal Approach (Using HashSet, O(n) Time)

### 🔍 Key Insight:

Only start building a sequence **if the current number is the beginning** (i.e., `num - 1` is not in the array).

---

### ✅ Steps:

1. **Add all elements to a `HashSet`** for O(1) lookup.
    
2. **Loop through each number**:
    
    - If `num - 1` is **not** in the set, it’s a potential start of a sequence.
        
    - Then, keep checking for `num + 1`, `num + 2`, ... in the set.
        
3. Track the **maximum length** encountered.
    

---

### ✅ Java Code
