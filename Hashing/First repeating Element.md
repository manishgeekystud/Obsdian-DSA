Given an array **arr[],** find the first repeating element. The element should occur more than once and the index of its first occurrence should be the smallest.

**Note:-** The position you return should be according to 1-based indexing. 

**Examples:**

**Input:** arr[] = [1, 5, 3, 4, 3, 5, 6]
**Output:** 2
**Explanation:** 5 appears twice and its first appearance is at index 2 which is less than 3 whose first the occurring index is 3.

**Input:** arr[] = [1, 2, 3, 4]
**Output:** -1
**Explanation:** All elements appear only once so answer is -1.

-------------------------------------------------------------------
```java
public static int firstRepeated(int[] arr) {
    // Create a HashMap to count the frequency of each element
    HashMap<Integer, Integer> hm = new HashMap<>();
    
    // First pass: Count the frequency of each element
    for (int num : arr) {
        hm.put(num, hm.getOrDefault(num, 0) + 1);
    }

    // Second pass: Find the first element whose frequency is more than 1
    int index = 1;  // 1-based index, as required
    for (int num : arr) {
        if (hm.get(num) > 1) {
            return index;  // First repeated element found
        }
        index++;
    }

    // If no repeated element found
    return -1;
}

```