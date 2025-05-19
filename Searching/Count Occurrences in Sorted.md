
---

Given a sorted array arr[] and a number x, write a function that counts the occurrences of x in arr[]. Expected time complexity is O(Logn) 

**Examples:** 

  **Input:** arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 2
  **Output:** 4 // x (or 2) occurs 4 times in arr[]

 ** Input:** arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 3
  **Output:** 1 

  **Input:** arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 1
  **Output:** 2 

 ** Input:** arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 4
 ** Output:** -1 // 4 doesn't occur in arr[] 
-------------------------------------------------------------------------------------------------------


To **count the number of occurrences of a given number** (say `x`) in a **sorted array**, you can use **binary search** to:

1. Find the **first occurrence** of `x`.
    
2. Find the **last occurrence** of `x`.
    
3. The count is then:
    
    count=(last index−first index)+1\text{count} = (\text{last index} - \text{first index}) + 1count=(last index−first index)+1
**Method: Binary Search**
```

```