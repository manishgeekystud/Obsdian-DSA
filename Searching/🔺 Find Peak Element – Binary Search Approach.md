## 

### ✅ Problem Statement

Given an integer array `nums`, find a **peak element**, and return its **index**.  
A **peak** is an element that is **strictly greater** than its neighbors.

- For corner elements, we consider only one neighbor.
    
- You **can return any** peak if multiple exist.
    
- Must solve in **O(log n)** time.
    

---

### 🤔 Intuition

- A peak is an element where `nums[i] > nums[i - 1]` and `nums[i] > nums[i + 1]`.
    
- Think of array like a mountain range:  
    We're trying to find a **local maximum**.
    
💡 **Key Insight**:  
If an element `nums[mid]` is **less than `nums[mid+1]`**,  
➡ the slope is **ascending** → Peak lies on **right**.  
Else,  
➡ the slope is **descending** → Peak lies on **left or at mid**.

---

### 🔍 Binary Search Logic

We keep narrowing the search space based on slope:

1. **Initialize** `low = 0`, `high = nums.length - 1`.
    
2. While `low < high`:
    
    - Compute `mid = (low + high) / 2`.
        
    - If `nums[mid] < nums[mid+1]`:  
        ➤ Peak lies on **right**, set `low = mid + 1`.
        
    - Else:  
        ➤ Peak lies on **left or at mid**, set `high = mid`.
        
3. When loop ends, `low == high` → pointing to a peak.
    

---

### ✅ Dry Run Example

`Input: nums = [1, 2, 3, 1]`

- Iteration 1: `mid = 1`, `nums[mid] = 2`, `nums[mid+1] = 3`  
    ➤ `2 < 3` → Peak lies on right → `low = 2`
    
- Iteration 2: `mid = 2`, `nums[mid] = 3`, `nums[mid+1] = 1`  
    ➤ `3 > 1` → Peak is on left or mid → `high = 2`
    
- Now `low == high == 2` → Return 2 ✅

**Code**
```java
public int findPeakElement(int[] nums) {
    int low = 0;
    int high = nums.length - 1;

    while (low < high) {
        int mid = low + (high - low) / 2;

        // Compare mid with next element to decide the slope
        if (nums[mid] < nums[mid + 1]) {
            // Ascending slope → peak is to the right
            low = mid + 1;
        } else {
            // Descending slope → peak is to the left or at mid
            high = mid;
        }
    }

    // At this point low == high and is the peak
    return low;
}

```
