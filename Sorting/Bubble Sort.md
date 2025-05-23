## 🔍 What is Bubble Sort?

Bubble Sort is a **simple comparison-based sorting algorithm** that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This process is repeated until the array is sorted.

---

## ⚙️ Algorithm Explanation

- Repeatedly swap adjacent elements if they are in the wrong order.
    
- In each pass, the largest unsorted element "bubbles" to the end of the list.
    
- After every iteration, one less element (from the end) needs to be checked.
    

---

## 🧠 Pseudocode

```java
for (int i = 0; i < n - 1; i++) {
    for (int j = 0; j < n - i - 1; j++) {
        if (arr[j] > arr[j + 1]) {
            // swap arr[j] and arr[j+1]
        }
    }
}

```
## ✅ Dry Run Example

Input: `arr = [5, 1, 4, 2, 8]`

```
Pass 1: [1, 4, 2, 5, 8]
Pass 2: [1, 2, 4, 5, 8]
Pass 3: [1, 2, 4, 5, 8]
Pass 4: [1, 2, 4, 5, 8] (no swaps)

```

Code
```java
void bubbleSort(int arr[])
    {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++)
            for (int j = 0; j < n - i - 1; j++)
                if (arr[j] > arr[j + 1]) {
                    // swap arr[j+1] and arr[j]
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
    }
```
## ⏱️ Time and Space Complexity

|Case|Time Complexity|
|---|---|
|Best (sorted array)|O(n) – with optimized version|
|Average|O(n²)|
|Worst|O(n²)|

- **Space Complexity**: O(1) (in-place)

## 📌 Characteristics

- **Stable**: Yes
    
- **In-Place**: Yes
    
- **Adaptive**: Yes (with optimization)
    

---

## 🚫 When Not to Use

- For large datasets (inefficient)
    
- When optimal performance is needed
    

---

## 🟢 When to Use

- Learning basic sorting
    
- Small datasets
    
- Situations where simplicity matters more than performance