

Given an array of non-negative integers `arr[]` and a value `target`, find the **starting and ending indexes (1-based)** of a **continuous subarray** that adds up to the `target`.

If no such subarray is found, return `[-1]`.

---

## 🔍 Approach: Two Pointer / Sliding Window

### 💡 Intuition:
- For **non-negative integers**, the sum of a subarray will **only increase** when we move the right pointer forward.
- If the sum exceeds the target, move the **left** pointer to shrink the window.
- Efficient because we never reprocess the same elements (O(n) time).

---

## 🛠️ Steps:

1. Initialize:
   - `left = 0`, `currentSum = 0`
2. Iterate `right` from 0 to end of array:
   - Add `arr[right]` to `currentSum`
   - While `currentSum > target`, subtract `arr[left]` and move `left++`
   - If `currentSum == target`, return `[left+1, right+1]`
3. If no match is found, return `[-1]`

---

## ✅ Java Code

```java
static ArrayList<Integer> subarraySum(int[] arr, int target) {
    int left = 0;
    int right = 0;
    int n = arr.length;
    int currentSum = 0;
    ArrayList<Integer> ans = new ArrayList<>();

    for (right = 0; right < n; right++) {
        currentSum += arr[right];

        // Shrink window from left if sum exceeds target
        while (currentSum > target && left <= right) {
            currentSum -= arr[left++];
        }

        // Match found
        if (currentSum == target) {
            ans.add(left + 1);   // 1-based indexing
            ans.add(right + 1);
            return ans;
        }
    }

    ans.add(-1);
    return ans;
}
