Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return _the area of the largest rectangle in the histogram_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

**Input:** heights = [2,1,5,6,2,3]
**Output:** 10
**Explanation:** The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

**Input:** heights = [2,4]
**Output:** 4

**Constraints:**

- `1 <= heights.length <= 105`
- `0 <= heights[i] <= 104`
-----------------------------------------------------------------------

Solution

## 🔄 Brute Force Steps:

1. For every bar `i` from `0` to `n-1`:
    
    - Expand to the **left** until you find a bar smaller than `heights[i]`
        
    - Expand to the **right** until you find a bar smaller than `heights[i]`
        
    - Calculate:  
        `width = right - left + 1 area = width * heights[i]`
        
    - Keep track of the **maximum area**
        

---

## ✅ Java Code (Brute Force)

```java
public class LargestRectangleBruteForce {

    public static int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int maxArea = 0;

        for (int i = 0; i < n; i++) {
            int height = heights[i];

            // Expand to the left
            int left = i;
            while (left > 0 && heights[left - 1] >= height) {
                left--;
            }

            // Expand to the right
            int right = i;
            while (right < n - 1 && heights[right + 1] >= height) {
                right++;
            }

            // Calculate area
            int width = right - left + 1;
            int area = width * height;
            maxArea = Math.max(maxArea, area);
        }

        return maxArea;
    }

    public static void main(String[] args) {
        int[] heights = {2, 1, 5, 6, 2, 3};
        System.out.println("Largest Area: " + largestRectangleArea(heights));  // Output: 10
    }
}

```

**Optimal solution**
## Intuition

To find the largest rectangle area, we need to determine for each bar **how far it can extend to the left and right** without encountering a shorter bar.  
Using **monotonic stacks**, we can compute the **Nearest Smaller to Left (NSL)** and **Nearest Smaller to Right (NSR)** efficiently.

## Approach

1️⃣ Use a stack to compute `left[i]` → index of the **nearest smaller element to the left**.  
2️⃣ Clear stack and compute `right[i]` → index of the **nearest smaller element to the right**.  
3️⃣ For each bar, calculate `width[i] = right[i] - left[i] - 1`.  
4️⃣ Compute `area = heights[i] * width[i]` and track `maxArea`.  
5️⃣ Return `maxArea`.

## Complexity

- **Time complexity:** O(n) – Each element is pushed and popped at most once.
- **Space complexity:** O(n) – Arrays `left`, `right`, and stack storage.

**CODE**

```java


```

