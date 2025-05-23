The ****selection sort algorithm**** sorts an array by repeatedly finding the minimum element (considering ascending order) from unsorted part and putting it at the beginning. The algorithm maintains two subarrays in a given array.

- The subarray which is already sorted. 
- Remaining subarray which is unsorted.

In every iteration of selection sort, the minimum element (considering ascending order) from the unsorted subarray is picked and moved to the sorted subarray.

refer
(https://www.geeksforgeeks.org/batch/dsa-4/track/DSASP-Sorting/article/Nzc1Nw%3D%3D)

### Approach:

> - Initialize minimum value(min_idx) to location 0
> - Traverse the array to find the minimum element in the array
> - While traversing if any element smaller than ****min_idx**** is found then swap both the values.
> - Then, increment min_idx to point to next element
> - Repeat until array is sorted

Below is the implementation of the above approach:
```java
// Java program for implementation of Selection Sort
class SelectionSort
{
    void sort(int arr[])
    {
        int n = arr.length;

        // One by one move boundary of unsorted subarray
        for (int i = 0; i < n-1; i++)
        {
            // Find the minimum element in unsorted array
            int min_idx = i;
            for (int j = i+1; j < n; j++)
                if (arr[j] < arr[min_idx])
                    min_idx = j;

            // Swap the found minimum element with the first
            // element
            int temp = arr[min_idx];
            arr[min_idx] = arr[i];
            arr[i] = temp;
        }
    }
```
## ⏱️ Time and Space Complexity

|Case|Time Complexity|
|---|---|
|Best|O(n²)|
|Average|O(n²)|
|Worst|O(n²)|

- **Space Complexity**: O(1) (In-place)
    

---

## 📌 Characteristics

- **Stable**: ❌ Not stable (can be made stable with extra steps)
    
- **In-Place**: ✅ Yes
    
- **Adaptive**: ❌ No (doesn’t benefit from a sorted array)
    

---

## 🚫 When Not to Use

- When stability is required
    
- For large datasets (inefficient)
    

---

## 🟢 When to Use

- When memory space is extremely limited
    
- For small or almost-sorted datasets
    
- When number of swaps must be minimal (Selection Sort does fewer swaps compared to Bubble Sort)