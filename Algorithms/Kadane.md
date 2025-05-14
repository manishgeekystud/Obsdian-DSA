Given an array of integers (can include negatives), find the **maximum sum of a contiguous subarray**.

---

## ✅ Core Logic (Kadane’s Algorithm)

java
```
public class Solution {
public int maxSubArray(int[] A) {
    int max = Integer.MIN_VALUE, sum = 0;
    for (int i = 0; i < A.length; i++) {
        if (sum < 0) 
            sum = A[i];
        else 
            sum += A[i];
        if (sum > max)
            max = sum;
    }
    return max;
}
```


---

## 🔥Remember

> (_If life becomes negative, start fresh from the next day._)

Keep living, track your best stretch — that's your **max subarray sum**.

---

## 🧠 Key Points to Remember

- **sum < 0?** Toss it! Start new.
    
- **sum >= 0?** Keep adding!
    
- **max?** Always store the best stretch.
    

---

## 💥 Example

Input: `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`  
Max Sum = `6` (from subarray `[4, -1, 2, 1]`)

---

## ❗ Special Case – All Negative Elements

Input: `[-3, -2, -6]`  
Kadane still gives you the **least negative element** → `-2`.

Because:

> "Zindagi buri ho to bhi, jo sabse kam dard de, wahi best samjho."

Step-by-step with `A = [-8, -3, -6, -2, -5, -4]`:
i	A[i]	sum	max
0	-8	-8	-8
1	-3	-3 (reset)	-3 ✅
2	-6	-6 (reset)	-3
3	-2	-2 (reset)	-2 ✅
4	-5	-5 (reset)	-2
5	-4	-4 (reset)	-2



---

## ⏱️ Complexity

- **Time:** `O(n)` (single pass)
    
- **Space:** `O(1)` (no extra space)
    

---

## 🧷 Interview Tagline (to say & remember)

> **"Kadane is about hope – drop the negativity, carry the positivity, and remember your best moment."**

---
uses
Certainly! Here’s a list of **problems** based on **Kadane’s Algorithm**. These problems can help you practice and master Kadane’s algorithm, and also explore its variations.

---

### **List of Problems Based on Kadane's Algorithm**

---

#### 1. **Maximum Subarray (LeetCode 53)**

- **Problem**: Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
    
- **Difficulty**: Easy
    
- **Link**: [LeetCode Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
    

---

#### 2. **Maximum Sum Circular Subarray (LeetCode 918)**

- **Problem**: Given a circular integer array `nums`, find the maximum sum of a subarray.
    
- **Difficulty**: Medium
    
- **Link**: [LeetCode Maximum Sum Circular Subarray](https://leetcode.com/problems/maximum-sum-circular-subarray/)
    

---

#### 3. **Maximum Product Subarray (LeetCode 152)**

- **Problem**: Find the contiguous subarray within an array (containing at least one number) which has the largest product.
    
- **Difficulty**: Medium
    
- **Link**: [LeetCode Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
    

---

#### 4. **Minimum Subarray (LeetCode 918)**

- **Problem**: Similar to the Maximum Subarray, but you need to find the subarray that results in the **minimum sum**.
    
- **Difficulty**: Medium
    
- **Link**: [LeetCode Minimum Subarray](https://leetcode.com/problems/minimum-subarray/)
    

---

#### 5. **Maximum Subarray Sum with One Deletion (LeetCode 1186)**

- **Problem**: Given an array `A` of integers, you can delete at most one element. Find the **maximum sum** of the contiguous subarray after at most one deletion.
    
- **Difficulty**: Hard
    
- **Link**: [LeetCode Maximum Subarray Sum with One Deletion](https://leetcode.com/problems/maximum-subarray-sum-with-one-deletion/)
    

---

#### 6. **Find the Largest Sum of Non-Adjacent Numbers**

- **Problem**: Given a list of integers, find the largest sum that you can obtain by adding non-adjacent numbers from the list.
    
- **Difficulty**: Medium
    
- **Concept**: Can be solved using Kadane’s modification where adjacent numbers are skipped.
    
- **Link**: [Find the Largest Sum of Non-Adjacent Numbers](https://www.codingame.com/training/medium/find-the-largest-sum-of-non-adjacent-numbers)
    

---

#### 7. **Kadanes’ Algorithm: Finding Maximum Subarray with Length Constraints**

- **Problem**: Given an array, find the maximum sum subarray of length `k`.
    
- **Difficulty**: Medium
    
- **Concept**: Kadane’s algorithm with a sliding window constraint (fixed subarray length).
    

---

#### 8. **Maximum Sum Increasing Subarray**

- **Problem**: Given an array, find the maximum sum subarray that is **strictly increasing**.
    
- **Difficulty**: Medium
    
- **Concept**: Modified Kadane’s algorithm with a check to ensure subarray elements are increasing.
    

---

#### 9. **Stock Buy and Sell (Kadane's Modified)**

- **Problem**: Given an array where each element represents the stock price on a given day, find the **maximum profit** you can make by buying and selling once.
    
- **Difficulty**: Easy
    
- **Link**: [LeetCode Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
    

---

#### 10. **Largest Sum Contiguous Subarray**

- **Problem**: This is essentially the **Kadane’s Algorithm** problem, where you need to find the largest sum of a contiguous subarray.
    
- **Difficulty**: Easy
    
- **Concept**: Classic Kadane’s problem (LeetCode 53).
    

---

#### 11. **Maximum Sum of Three Non-Overlapping Subarrays**

- **Problem**: Given an array, find the maximum sum of **three non-overlapping subarrays**.
    
- **Difficulty**: Hard
    
- **Concept**: This problem can be solved using a **dynamic programming approach** combined with Kadane’s for the subarrays.
    
- **Link**: [LeetCode Maximum Sum of Three Non-Overlapping Subarrays](https://leetcode.com/problems/maximum-sum-of-Three-non-overlapping-subarrays/)
    

---

#### 12. **Longest Subarray with Sum at Most K**

- **Problem**: Given an array of integers, find the length of the **longest subarray** whose sum is at most `k`.
    
- **Difficulty**: Medium
    
- **Concept**: Use Kadane’s algorithm with a **sliding window** to manage the sum.
    

---

#### 13. **Largest Rectangle in Histogram (LeetCode 84)**

- **Problem**: Find the largest rectangular area possible in a given histogram.
    
- **Difficulty**: Hard
    
- **Link**: [LeetCode Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)
    

---

#### 14. **Maximum Sum Subarray with a Fixed Size (Fixed Length Subarray Sum)**

- **Problem**: Given an array and a fixed length `k`, find the maximum sum of any subarray of size `k`.
    
- **Difficulty**: Medium
    
- **Concept**: Kadane’s algorithm combined with a **sliding window** approach.
    

---

#### 15. **Maximum Subarray Sum After One Removal**

- **Problem**: Given an array, you can **remove one element**. Find the **maximum sum** of the subarray after removing at most one element.
    
- **Difficulty**: Medium to Hard
    
- **Link**: [LeetCode Maximum Subarray Sum After One Removal](https://leetcode.com/problems/maximum-subarray-sum-after-one-removal/)
    

---

### **Bonus**: **Competitive Programming**:

Kadane's algorithm can be found in several **competitive programming** problems on platforms like:

- **Codeforces**
    
- **Codechef**
    
- **AtCoder**
    

Look for terms like **"maximum sum subarray," "circular subarray," or "non-overlapping subarrays"** in these contests.

---

### **Key Takeaways**:

Kadane's Algorithm is one of the **most efficient algorithms** for finding maximum subarray sums in **linear time** (`O(n)`), and it can be adapted for various types of problems by modifying the base algorithm (e.g., with constraints like circular subarrays, deletions, non-adjacency).

Would you like me to dive deeper into any of these problems with an example or solution walkthrough?