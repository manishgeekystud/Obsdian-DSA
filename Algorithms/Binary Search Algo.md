**Binary Search** is an efficient algorithm for finding an item from a sorted list of elements by repeatedly dividing the search interval in half.

### ✅ Prerequisite:

- **The array must be sorted** (either ascending or descending).
### 🧠 Intuition:

- Pick the middle element.
- If it matches the target → done.
- If the target is smaller → search in the left half.
- If the target is greater → search in the right half.
### ⏱️ Time Complexity:

- **Best Case:** `O(1)` (when the element is in the middle)
- **Average Case:** `O(log n)`
- **Worst Case:** `O(log n)`
![[Pasted image 20250518223632.png]]
