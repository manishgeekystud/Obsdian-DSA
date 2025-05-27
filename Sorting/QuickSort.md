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

```java
public class QuickSort {

    // Main quicksort function
    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            // Find pivot index
            int pivotIndex = partition(arr, low, high);

            // Recursively sort elements before and after partition
            quickSort(arr, low, pivotIndex - 1);
            quickSort(arr, pivotIndex + 1, high);
        }
    }

    // Partition function using last element as pivot
    private static int partition(int[] arr, int low, int high) {
        int pivot = arr[high];
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;
                swap(arr, i, j);
            }
        }

        // Place pivot in the correct position
        swap(arr, i + 1, high);
        return i + 1;
    }

    // Swap helper function
    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Testing
    public static void main(String[] args) {
        int[] arr = {10, 7, 8, 9, 1, 5};
        quickSort(arr, 0, arr.length - 1);
        System.out.println("Sorted array:");
        for (int num : arr) System.out.print(num + " ");
    }
}

```