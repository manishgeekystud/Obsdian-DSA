## What’s This Sliding Window Pattern All About?

Now, let’s talk about when to pull out this technique from your programming toolbox. You’d want to consider using the sliding window pattern in situations like these:

**1. Subarray or Substring Problems:** Imagine you need to find the longest or shortest subarray or substring that meets certain criteria (like having the maximum sum or distinct elements). Well, that’s the sliding window’s sweet spot.

**2. Fixed-Size Data Extraction:** Sometimes, you need to process data within a fixed-size window or subarray. Think of it as extracting insights from a particular chunk of data. This pattern makes it a breeze.

**3. Two-Pointer Approach:** In some cases, you can think of the sliding window as a two-pointer approach, where two pointers (usually the left and right) roam through your data while maintaining a specific window size.

------------------------------------------------------------------
## How Do You Actually Use It?

So, you’re sold on trying out the sliding window pattern? Awesome! Here’s a quick guide on how to implement it:

**Step 1:** Define Your Window: First things first, you define the window size or boundaries. Most of the time, you’ll have two pointers, one marking the start and the other the end of the window. Set them up accordingly.

**Step 2:** Slide the Window: Now comes the fun part! Start moving your window by incrementing the end pointer. While you do this, keep track of any relevant data within that window.

**Step 3:** Check the Constraints: At each step, give a look-see to check if the current window satisfies your problem’s constraints or requirements. If it does, update your result or do whatever needs to be done.

**Step 4:** Adjust the Window: If the window no longer meets the constraints, don’t fret. Simply adjust it by incrementing the start pointer while ensuring the window’s size stays constant.

**Step 5:** Rinse and Repeat: Keep sliding and adjusting that window until you’ve worked through the entire array or list. Eventually, you’ll get the result you’re aiming for.

## Are there any types?

Yes, the sliding window pattern can be categorized into two main types: fixed-size windows and dynamic-size windows.

Let’s explore each type with examples:

**1. Fixed-Size Window:** In a fixed-size window, the size of the window remains constant as it slides through the data. This type of sliding window is particularly useful when you need to process data within a fixed range or for a specific length of elements.

_Example: Maximum Sum Subarray (Fixed-Size Window)_
### Example Problem - Maximum Sum of a Subarray with K Elements

Given an array and an integer k, we need to calculate the maximum sum of a subarray having size exactly k****.****

> ****Input  :**** arr[] = {100, 200, 300, 400}, k = 2  
> ****Output :**** 700  
> We get maximum sum by considering the subarray [300, 400]
> 
> ****Input  :**** arr[] = {1, 4, 2, 10, 23, 3, 1, 0, 20}, k = 4   
> ****Output :**** 39  
> We get maximum sum by adding subarray {4, 2, 10, 23} of size 4.
> 
> ****Input  :**** arr[] = {2, 3}, k = 3  
> ****Output :**** Invalid  
> There is no subarray of size 3 as size of whole array is 2.

-------------------------------------------------------
The below representation will make it clear how the window slides over the array.

> Consider an array ****arr[]**** = {5, 2, -1, 0, 3} and value of ****k**** = 3 and ****n**** = 5
> 
> This is the initial phase where we have calculated the initial window sum starting from index 0 . At this stage the window sum is 6. Now, we set the maximum_sum as current_window i.e 6.   
>  
> 
> ![](https://media.geeksforgeeks.org/wp-content/uploads/sliding-window1.png)
> 
> Now, we slide our window by a unit index. Therefore, now it discards 5 from the window and adds 0 to the window. Hence, we will get our new window sum by subtracting 5 and then adding 0 to it. So, our window sum now becomes 1. Now, we will compare this window sum with the maximum_sum. As it is smaller, we won't change the maximum_sum.   
>  
> 
> ![](https://media.geeksforgeeks.org/wp-content/uploads/sliding-window2.png)
> 
>   
> Similarly, now once again we slide our window by a unit index and obtain the new window sum to be 2. Again we check if this current window sum is greater than the maximum_sum till now. Once, again it is smaller so we don't change the maximum_sum.  
> Therefore, for the above array our maximum_sum is 6.
> 
> ![](https://media.geeksforgeeks.org/wp-content/uploads/sliding-window3.png)
> 

code
```java
  static int maxSum(int arr[], int n, int k)
    {
        // n must be greater
        if (n <= k) {
            System.out.println("Invalid");
            return -1;
        }

        // Compute sum of first window of size k
        int max_sum = 0;
        for (int i = 0; i < k; i++)
            max_sum += arr[i];

        // Compute sums of remaining windows by
        // removing first element of previous
        // window and adding last element of
        // current window.
        int window_sum = max_sum;
        for (int i = k; i < n; i++) {
            window_sum += arr[i] - arr[i - k];
            max_sum = Math.max(max_sum, window_sum);
        }

        return max_sum;
    }
```

**2. Dynamic-Size Window:** In a dynamic-size window, the size of the window can change as it slides through the data. This type of sliding window is used when the problem requires adjusting the window size based on specific conditions or constraints.

_Example: Longest Subarray with Sum at Most K (Dynamic-Size Window)_

### 🔄 **What is a Dynamic-Size Sliding Window?**

A **sliding window** is a range (subarray) within the array that you adjust as you move through the data.

- In **fixed-size** window problems (e.g., max sum of size `k`), the window length stays the same.
    
- In **dynamic-size** windows, **the size of the window can grow or shrink** based on conditions—like the sum being too high, or constraints like at most `K` unique elements.
    

---

## 🧠 Problem Example:

### **Longest Subarray with Sum at Most K**

🧾 **Given:**

- An array: `arr = [1, 2, 1, 0, 1, 1, 0]`
    
- A sum limit: `K = 4`
    

🔍 **Goal:**  
Find the **maximum length** of a contiguous subarray whose elements sum to **at most K**.

---

### ✅ **Approach (Dynamic Window)**

We’ll use two pointers:

- `start` → Beginning of the window
    
- `end` → Expands the window by moving forward
    
- Track `sum` of the current window
    

If `sum > K`, shrink the window from the left (`start++`)  
If `sum <= K`, consider it as a valid window and possibly expand further.

---

### 🔄 Dry Run with Dynamic Window

|Step|Start|End|Subarray|Sum|Action|Max Length|
|---|---|---|---|---|---|---|
|1|0|0|[1]|1|Valid, expand|1|
|2|0|1|[1, 2]|3|Valid, expand|2|
|3|0|2|[1, 2, 1]|4|Valid, expand|3|
|4|0|3|[1, 2, 1, 0]|4|Valid, expand|4|
|5|0|4|[1, 2, 1, 0, 1]|5|Too much, shrink|4|
|6|1|4|[2, 1, 0, 1]|4|Valid, expand|4|
|7|1|5|[2, 1, 0, 1, 1]|5|Too much, shrink|4|
|8|2|5|[1, 0, 1, 1]|3|Valid, expand|4|
|9|2|6|[1, 0, 1, 1, 0]|3|Valid|**5** ✅|

---

### 🧮 Final Answer:

**Longest subarray with sum ≤ 4 is of length 5**  
Subarray: `[1, 0, 1, 1, 0]`

---
CODE

```java
public class LongestSubarraySumAtMostK {

    public static int longestSubarray(int[] arr, int k) {
        int start = 0;
        int sum = 0;
        int maxLen = 0;

        for (int end = 0; end < arr.length; end++) {
            sum += arr[end];  // expand the window

            // Shrink window if sum exceeds k
            while (sum > k && start <= end) {
                sum -= arr[start];
                start++;
            }

            // Check max length of valid window
            maxLen = Math.max(maxLen, end - start + 1);
        }

        return maxLen;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 1, 0, 1, 1, 0};
        int k = 4;

        int result = longestSubarray(arr, k);
        System.out.println("Longest subarray length with sum at most " + k + " is: " + result);
    }
}

```
### 💡 Summary

- The **window starts small**.
    
- As long as the **sum is under the limit**, we **expand** the window.
    
- If the **sum exceeds K**, we **shrink** from the left until valid.
    
- Track the **maximum valid window length** during this process.
    

This is the essence of **dynamic-size sliding window**: adjust window **size on the fly** based on logic.