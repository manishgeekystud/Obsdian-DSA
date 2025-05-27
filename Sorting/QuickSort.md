## 📌 **What is QuickSort?**

QuickSort is a **divide-and-conquer sorting algorithm** that:

1. Picks a **pivot element**.
    
2. Partitions the array such that:
    
    - Elements **less than** pivot go to the left.
        
    - Elements **greater than** pivot go to the right.
        
3. Recursively sorts the left and right subarrays.
    

---

## 🧱 Key Concept: Using **Last Element** as Pivot

- Choosing the last element simplifies partition logic.
    
- You loop from left to right and move elements less than the pivot to the front.
    

---

## 🧠 Algorithm Steps

Given `arr[]`, `low`, and `high`:

1. **Base Case:** If `low >= high`, return (already sorted).
    
2. **Partition the array** around the last element `arr[high]`:
    
    - Elements smaller than `pivot` go to the left.
        
    - Elements larger stay on the right.
        
3. **Place the pivot in its correct sorted position**.
    
4. **Recursively call** quicksort on left and right subarrays.
    

---

## 🔧 Partition Function

The **partitioning** is done using the **Lomuto partition scheme**.

### Logic:

- Choose the last element as the pivot.
    
- Initialize `i = low - 1`
    
- For each `j` from `low` to `high - 1`:
    
    - If `arr[j] <= pivot`: increment `i`, swap `arr[i]` and `arr[j]`
        
- After the loop, swap `arr[i+1]` with the pivot `arr[high]`
    
- Return `i + 1` as the **pivot index**
    

---

## ✅ Java Implementation

```

```