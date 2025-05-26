## 🔍 What is Insertion Sort?

**Insertion Sort** is a simple sorting algorithm that builds the sorted array one element at a time by **comparing each new element to the already sorted part** and inserting it at the correct position.

---

## ⚙️ Algorithm Explanation

- Start from index 1 and pick the element.
    
- Compare it with all elements before it.
    
- Shift all greater elements one position to the right.
    
- Insert the picked element at its correct position.
    
- Repeat until the array is sorted.
    

---

## 🧠 Pseudocode
```java
for (int i = 1; i < n; i++) {
    int key = arr[i];
    int j = i - 1;

    // Shift elements of arr[0..i-1], that are greater than key
    while (j >= 0 && arr[j] > key) {
        arr[j + 1] = arr[j];
        j = j - 1;
    }
    arr[j + 1] = key;
}

```

---

## ✅ Dry Run Example

Input: `arr = [5, 3, 4, 1, 2]`
```
i = 1, key = 3 -> [3, 5, 4, 1, 2]
i = 2, key = 4 -> [3, 4, 5, 1, 2]
i = 3, key = 1 -> [1, 3, 4, 5, 2]
i = 4, key = 2 -> [1, 2, 3, 4, 5]

```

---

## ⏱️ Time and Space Complexity

|Case|Time Complexity|
|---|---|
|Best|O(n)|
|Average|O(n²)|
|Worst|O(n²)|

- **Space Complexity**: O(1) (in-place)
    

---

## 📌 Characteristics

- **Stable**: ✅ Yes
    
- **In-Place**: ✅ Yes
    
- **Adaptive**: ✅ Yes (efficient for nearly sorted data)
    

---

## 🟢 When to Use

- For **small datasets**
    
- When the **array is nearly sorted**
    
- When **stability** is important
    

---

## 🚫 When Not to Use

- On **large datasets** due to O(n²) time complexity