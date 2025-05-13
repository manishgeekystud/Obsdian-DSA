You are given an array **`arr[]`** containing positive integers. The elements in the array `arr[]` range from `1` to `n` (where `n` is the size of the array), and some numbers may be repeated or absent. Your task is to count the frequency of all numbers in the range `1` to `n` and return an array of size `n` such that `result[i]` represents the frequency of the number `i` (1-based indexing).

**Examples**

**Input:** arr[] = [2, 3, 2, 3, 5]
**Output:** [0, 2, 2, 0, 1]  
**Explanation:** We have: `1` occurring 0 times, `2` occurring 2 times, `3` occurring 2 times, `4` occurring 0 times, and `5` occurring 1 time.

**Input:** arr[] = [3, 3, 3, 3]
**Output:** [0, 0, 4, 0]
**Explanation:** We have: `1` occurring 0 times, `2` occurring 0 times, `3` occurring 4 times, and `4` occurring 0 times.

**Input:** arr[] = [1]
**Output:** [1]
**Explanation:** We have: `1` occurring 1 time, and there are no other numbers between `1` and the size of the array.

**Constraints:**  
1 ≤ arr.size() ≤ 106  
1 ≤ arr[i] ≤ arr.size()

**Brute Force** -O(n* n)
```
 public List<Integer> frequencyCount(int[] arr) {
        // do modify in the given array
        
        ArrayList<Integer> ans =new ArrayList<>();
        int n=arr.length;
        for(int i=1;i<=n;i++)
        {
            int count =0;
            for(int j=0;j<n;j++)
            {
                if(arr[j]==i)
                   count++;
            }
            ans.add(count);
            
        }
    return ans;
    }
```

**Optimized solution**


### ✅ Core Idea:

Use the original array as a **bucket for frequency counts**. Here’s the plan:

1. Since the array has numbers from `1` to `n`, we can **rearrange and repurpose the array to count frequencies**.
    
2. We'll do the counting by **placing the count of each number at its correct index** (i.e., `number - 1`) and **marking visited elements** in a way that doesn't require extra space.
    

---

### 🔧 Step-by-Step Approach:

1. Traverse the array.
    
2. For each element `x`, place it at its correct index `x - 1`, but instead of keeping the value, **increment a counter at that index**.
    
3. To avoid infinite loops or overwriting, **we use negative values** to mark how many times each number has occurred (using negation of the count).
    
4. At the end, convert negative counts to positive frequency values.

```
public static void countFrequencies(int[] arr) {
        int n = arr.length;

        for (int i = 0; i < n; i++) {
            while (arr[i] > 0) {
                int elementIndex = arr[i] - 1;

                if (arr[elementIndex] > 0) {
                    // Swap and start counting at that position
                    int temp = arr[elementIndex];
                    arr[elementIndex] = -1;
                    arr[i] = temp;
                } else {
                    // Already counting, just decrement
                    arr[elementIndex]--;
                    arr[i] = 0;
                }
            }
        }

        // Final pass: convert negative counts to positive frequencies
        for (int i = 0; i < n; i++) {
            arr[i] = -arr[i];
        }
    }

```

Let's dry run the code using the input:
```
arr = [2, 3, 2, 3, 5]
```
### 🔄 Step-by-step Execution:

We'll follow the `countFrequencies` function. The goal is to use **negatives** to track counts at the corresponding positions (`arr[val - 1]--`).

Initial state:
`arr = [2, 3, 2, 3, 5] n = 5`

#### Pass 1: Frequency counting

**i = 0**  
`arr[0] = 2`  
→ `elementIndex = 1`  
→ `arr[1] = 3` (positive)  
→ Swap: store `temp = 3`, set `arr[1] = -1`, set `arr[0] = 3`

Now:
`arr = [3, -1, 2, 3, 5]`

**i = 0 again**  
`arr[0] = 3`  
→ `elementIndex = 2`  
→ `arr[2] = 2` (positive)  
→ Swap: `temp = 2`, set `arr[2] = -1`, set `arr[0] = 2`

Now:
`arr = [2, -1, -1, 3, 5]`

**i = 0 again**  
`arr[0] = 2`  
→ `elementIndex = 1`  
→ `arr[1] = -1` (already counting)  
→ Decrement `arr[1]--` → becomes `-2`  
→ Set `arr[0] = 0`

Now:
`arr = [0, -2, -1, 3, 5]`

**i = 1**  
`arr[1] = -2` → skip (already processed)

**i = 2**  
`arr[2] = -1` → skip (already processed)

**i = 3**  
`arr[3] = 3`  
→ `elementIndex = 2`  
→ `arr[2] = -1`  
→ Decrement `arr[2]--` → becomes `-2`  
→ Set `arr[3] = 0`

Now:
`arr = [0, -2, -2, 0, 5]`

**i = 4**  
`arr[4] = 5`  
→ `elementIndex = 4`  
→ `arr[4] = 5` (positive)  
→ Swap: `temp = 5`, `arr[4] = -1`, `arr[4] = 5` → both same, so set `arr[4] = -1`

Now:
`arr = [0, -2, -2, 0, -1]`

---

#### Pass 2: Convert negative counts to positive

`arr = [0, -2, -2, 0, -1]  →  [0, 2, 2, 0, 1]`

---

### ✅ Final Output:

`[0, 2, 2, 0, 1]`

Which means:

- 1 appears 0 times
    
- 2 appears 2 times
    
- 3 appears 2 times
    
- 4 appears 0 times
    
- 5 appears 1 time