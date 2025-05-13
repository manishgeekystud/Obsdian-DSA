You are given an array **`arr`** of positive integers. Your task is to find all the leaders in the array. An element is considered a leader if it is greater than or equal to all elements to its right. The rightmost element is always a leader.

**Examples:  
**

**Input:** arr = [16, 17, 4, 3, 5, 2]
**Output:** [17, 5, 2]
**Explanation:** Note that there is nothing greater on the right side of 17, 5 and, 2.

**Input:** arr = [10, 4, 2, 4, 1]
**Output:** [10, 4, 4, 1]  
**Explanation:** Note that both of the 4s are in output, as to be a leader an equal element is also allowed on the right. side

**Input:** arr = [5, 10, 20, 40]  
**Output:** [40]  
**Explanation:** When an array is sorted in increasing order, only the rightmost element is leader.

**Input:** arr = [30, 10, 10, 5]  
**Output:** [30, 10, 10, 5]  
**Explanation:** When an array is sorted in non-increasing order, all elements are leaders.

**Constraints:**  
1 <= arr.size() <= 106  
0 <= arr[i] <= 106

.

---

## 🔨 Brute Force Approach

### ▶️ Logic:

- For each element `arr[i]`, compare with all elements to its right.
    
- If no greater element exists to the right, it's a leader.
    

### 🧾 Code:
```
static ArrayList<Integer> leadersBrute(int arr[], int n) {
    ArrayList<Integer> result = new ArrayList<>();

    for (int i = 0; i < n; i++) {
        boolean isLeader = true;

        for (int j = i + 1; j < n; j++) {
            if (arr[i] < arr[j]) {
                isLeader = false;
                break;
            }
        }

        if (isLeader)
            result.add(arr[i]);
    }

    return result;
}

```
## ⚡ Optimized Approach (Right to Left Scan)

### ▶️ Logic:

- Start from the **last element** (guaranteed leader).
- Keep track of **maxFromRight**
- If current element ≥ maxFromRight → it's a leader.
    
✅ Your Code (Improved & Cleaned):
```
static List<Integer> leaders(int[] arr) {
    List<Integer> result = new ArrayList<>();
    int n = arr.length;
    int maxFromRight = arr[n - 1];

    result.add(maxFromRight);

    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] >= maxFromRight) {
            maxFromRight = arr[i];
            result.add(maxFromRight);
        }
    }

    Collections.reverse(result);
    return result;
}
```

✨ Even Cleaner with Deque (Avoid Reverse)
```
static List<Integer> leaders(int[] arr) {
    Deque<Integer> deque = new ArrayDeque<>();
    int max = arr[arr.length - 1];
    deque.addFirst(max);

    for (int i = arr.length - 2; i >= 0; i--) {
        if (arr[i] >= max) {
            max = arr[i];
            deque.addFirst(max);
        }
    }

    return new ArrayList<>(deque);
}

```
## 🔥 Desi Tip to Remember

> "**Peeche waale se bada ya barabar hai, toh tu hi leader hai bhai!**"  
> Start from **right side** and just keep noting down bigger ya barabar wale.  
> "Jo sabse aage dikh raha hai, wahi toh asli leader hota hai!"