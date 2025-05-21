Given a **rotated sorted array with distinct elements**, find the index of the `target` element using **O(log n)** time.

---

### 🧠 Understanding Rotation

The array was originally sorted but rotated at some pivot `k`.  
For example:


`Original: [0, 1, 2, 4, 5, 6, 7] 
 Rotated:    [4, 5, 6, 7, 0, 1, 2]  // rotated at index 4`

The array is now a **combination of two sorted subarrays**.

---

### 🎯 Goal:

Find the index of a given `target`, or return `-1` if not found — in **logarithmic time**.

---

### ⚙️ Binary Search Strategy

#### Step-by-step:

1. **Use Binary Search** normally: compute `mid = (low + high) / 2`.
    
2. **Determine which half is sorted:**
    
    - If `nums[low] <= nums[mid]`: **Left part is sorted**.
        
    - Else: **Right part is sorted**.
        
3. Check if `target` lies within the **sorted half**:
    
    - If **yes**, move search to that half.
        
    - If **no**, search the other half.
        
4. Repeat until you find the target or `low > high`.