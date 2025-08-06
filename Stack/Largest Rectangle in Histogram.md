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

```

```