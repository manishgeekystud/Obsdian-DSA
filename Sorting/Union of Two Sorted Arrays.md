Given two **sorted** arrays **a[]** and **b[]**, where each array may contain **duplicate** elements , the task is to return the elements in the **union** of the two arrays in **sorted** order.

> Union of two arrays can be defined as the set containing distinct common elements that are present in either of the arrays.

**Examples:**

**Input**: a[] = [1, 2, 3, 4, 5], b[] = [1, 2, 3, 6, 7]  
**Output**: 1 2 3 4 5 6 7  
**Explanation**: Distinct elements including both the arrays are: 1 2 3 4 5 6 7.

**Input**: a[] = [2, 2, 3, 4, 5], b[] = [1, 1, 2, 3, 4]
**Output**: 1 2 3 4 5
**Explanation**: Distinct elements including both the arrays are: 1 2 3 4 5.

**Input**: a[] = [1, 1, 1, 1, 1], b[] = [2, 2, 2, 2, 2]
**Output**: 1 2

----------------------------------------------------------------------------------------------
### ✅ Problem:

Given two sorted arrays (which may contain duplicate elements), return the **sorted union** of both arrays **with distinct elements only**.

---

### ✅ Core Idea:

- Use **two pointers** to traverse both arrays.
    
- Skip over **duplicates** while traversing.
    
- Always pick the **smaller element**, or either if both are equal.
    
- After one array ends, **process remaining elements** in the other.
    

---

### ✅ Java Code with Explanation:

java

CopyEdit