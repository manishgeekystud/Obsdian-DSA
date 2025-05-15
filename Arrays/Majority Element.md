Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** 3

**Example 2:**

**Input:** nums = [2,2,1,1,1,2,2]
**Output:** 2

Solution

__The basic solution is to have two loops and keep track of the__ _****maximum****_ __count for all different elements. If the maximum count becomes greater than__ _****n/2****_ __then break the loops and return the element having the maximum count. If the maximum count doesn’t become more than n/2 then the majority element__ _****doesn’t****_ _