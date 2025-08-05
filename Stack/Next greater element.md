**Examples  
**

**Input**: arr[] = [1, 3, 2, 4]
**Output**: [3, 4, 4, -1]
**Explanation**: The next larger element to 1 is 3, 3 is 4, 2 is 4 and for 4, since it doesn't exist, it is -1.

**Input**: arr[] = [6, 8, 0, 1, 3]
**Output**: [8, -1, 1, 3, -1]
**Explanation**: The next larger element to 6 is 8, for 8 there is no larger elements hence it is -1, for 0 it is 1 , for 1 it is 3 and then for 3 there is no larger element on right and hence -1.

**Input**: arr[] = [10, 20, 30, 50]
**Output**: [20, 30, 50, -1]
**Explanation**: For a sorted array, the next element is next greater element also except for the last element.

-----------------------------------------------------------------------
## 🛠️ **Brute-Force Approach**

### 🔸 Idea:

For each element, scan all elements to its right until a greater element is found.

### 🔁 Code (O(n²)):

```
public ArrayList<Integer> nextGreaterBrute(int[] arr) {
    ArrayList<Integer> result = new ArrayList<>();
    int n = arr.length;

    for (int i = 0; i < n; i++) {
        int next = -1;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] > arr[i]) {
                next = arr[j];
                break;
            }
        }
        result.add(next);
    }

    return result;
}

```

