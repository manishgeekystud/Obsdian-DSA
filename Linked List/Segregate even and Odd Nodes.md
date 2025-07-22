Given a Linked List of integers, write a function to modify the linked list such that all even numbers appear before all the odd numbers in the modified linked list. Also, keep the order of even and odd numbers the same.

**Examples:** 

**Input:** 17->15->8->12->10->5->4->1->7->6->NULL
**Output:** 8->12->10->4->6->17->15->5->1->7->NULL

Input: 8->12->10->5->4->1->6->NULL
Output: 8->12->10->4->6->5->1->NULL

// If all numbers are even then do not change the list
**Input:** 8->12->10->NULL
**Output:** 8->12->10->NULL

// If all numbers are odd then do not change the list
**Input:** 1->3->5->7->NULL
**Output:** 1->3->5->7->NULL

-----------------------------------------------------------------------
**Solution**

The idea is to split the linked list into two:  one containing all even nodes and the other containing all odd nodes. And finally, attach the odd node linked list after the even node linked list.

