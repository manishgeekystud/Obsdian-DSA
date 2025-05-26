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

**Psedo** **Code**
```
mergeSort(arr):
    if size of arr > 1:
        mid = size of arr / 2
        left = first half of arr
        right = second half of arr
        
        mergeSort(left)
        mergeSort(right)

        merge(left, right, arr)

```

### **4. Time Complexity**

- **Worst-case:** O(nlog⁡n)O(n \log n)
    
- **Best-case:** O(nlog⁡n)O(n \log n)
    
- **Average-case:** O(nlog⁡n)O(n \log n)
    

### **5. Space Complexity**

- O(n)O(n) (Requires extra memory for merging)

**CODE**

```java
import java.util.Arrays;

public class MergeSort {
    public static void mergeSort(int[] arr) {
        if (arr.length < 2) return;

        int mid = arr.length / 2;
        int[] left = Arrays.copyOfRange(arr, 0, mid);
        int[] right = Arrays.copyOfRange(arr, mid, arr.length);

        mergeSort(left);
        mergeSort(right);

        merge(left, right, arr);
    }

    public static void merge(int[] left, int[] right, int[] arr) {
        int i = 0, j = 0, k = 0;

        while (i < left.length && j < right.length) {
            if (left[i] <= right[j]) {
                arr[k++] = left[i++];
            } else {
                arr[k++] = right[j++];
            }
        }
        while (i < left.length) arr[k++] = left[i++];
        while (j < right.length) arr[k++] = right[j++];
    }

    public static void main(String[] args) {
        int[] arr = {38, 27, 43, 3, 9, 82, 10};
        System.out.println("Original array: " + Arrays.toString(arr));
        mergeSort(arr);
        System.out.println("Sorted array: " + Arrays.toString(arr));
    }
}

```