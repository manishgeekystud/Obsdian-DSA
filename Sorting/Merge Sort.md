## 🔍 What is Merge Sort?

Merge Sort works by breaking down a problem into smaller subproblems, solving them individually, and then combining the results to form the final solution.
    

It is **stable**, **efficient**, and guarantees **O(n log n)** time complexity in all cases.

---

### **2. How Merge Sort Works**

1. **Divide:** Split the array into two halves until single-element subarrays are obtained.
    
2. **Conquer:** Recursively sort each half.
    
3. **Merge:** Combine the sorted subarrays into a single sorted array.
    

#### **Example Step-by-Step**

Sorting `[38, 27, 43, 3, 9, 82, 10]` using Merge Sort:

1. Split into two halves: `[38, 27, 43, 3]` and `[9, 82, 10]`
    
2. Recursively divide until individual elements remain.
    
3. Merge pairs into sorted order → `[27, 38]`, `[3, 43]`, `[9, 10]`, `[82]`
    
4. Merge sorted groups → `[3, 27, 38, 43]` and `[9, 10, 82]`
    
5. Merge final halves → `[3, 9, 10, 27, 38, 43, 82]`