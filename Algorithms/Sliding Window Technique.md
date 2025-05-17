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

-------------------