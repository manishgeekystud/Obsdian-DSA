### Merge Without Extra Space

Difficulty: **Medium**

Given two sorted arrays **a[]** and **b[]** of size **n** and **m** respectively, the task is to merge them in sorted order without using any **extra space**. Modify **a[]** so that it contains the first **n** elements and modify **b[]** so that it contains the last **m** elements.

**Examples:**

**Input**: a[] = [2, 4, 7, 10], b[] = [2, 3]
**Output**:  
2 2 3 4  
7 10
**Explanation**: After merging the two non-decreasing arrays, we get, 2 2 3 4 7 10

**Input**: a[] = [1, 5, 9, 10, 15, 20], b[] = [2, 3, 8, 13]
**Output**:  
1 2 3 5 8 9  
10 13 15 20
**Explanation**: After merging two sorted arrays we get 1 2 3 5 8 9 10 13 15 20.

**Input**: a[] = [0, 1], b[] = [2, 3]
**Output**:  
0 1  
2 3
**Explanation**: After merging two sorted arrays we get 0 1 2 3.


-----------------------------------------
## 🧮 Approach

### 🔹 Step-by-step Logic:

1. Start from the **end of array `a`** and the **start of array `b`**.
    
2. Compare elements from both:
    
    - If `a[i] > b[j]`, **swap** them.
        
    - Move `i--` and `j++`.
        
3. After all swaps are done, **sort both arrays** individually.
    

---

## ✅ Java Code
```java
public void mergeArrays(int a[], int b[]) {
    int n = a.length;
    int m = b.length;

    // Pointers from the end of a and beginning of b
    int i = n - 1;
    int j = 0;

    // Compare and swap logic
    while (i >= 0 && j < m) {
        if (a[i] > b[j]) {
            // Swap larger a[i] with smaller b[j]
            int temp = a[i];
            a[i] = b[j];
            b[j] = temp;
        }
        i--; // Move backward in a
        j++; // Move forward in b
    }

    // Final step: sort both arrays to maintain sorted order
    Arrays.sort(a);
    Arrays.sort(b);
}

```