Given the `head` of a singly linked list, return `true` _if it is a_ _palindrome_ _or_ `false` _otherwise_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

**Input:** head = [1,2,2,1]
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

**Input:** head = [1,2]
**Output:** false

**Constraints:**

- The number of nodes in the list is in the range `[1, 105]`.
- `0 <= Node.val <= 9`

---------------------------------------------------------------------
**Interview Tip**
Every Linked List Problem, if you can't do it in LinkedList format, copy the data in list and now your question would become for an array, solve it.

# Approach ( Using List )

To Check if the Given Linked List is palindrome or not , we can copy the data in list and then check if the list if palindrome or not.

# Complexity

- Time complexity: O(N)

- Space complexity: O(N)

# Code

```java
public boolean isPalindrome(ListNode head) {
        List<Integer> list = new ArrayList();
        while(head != null) {
            list.add(head.val);
            head = head.next;
        }
        
        int left = 0;
        int right = list.size()-1;
        while(left < right && list.get(left) == list.get(right)) {
            left++;
            right--;
        }
        return left >= right;
    }
```
```

**# Approach#2** ( Using Stack )

First push all data in stack, and then traverse linked list and keep popping element from stack one by one, so stack will give you element from last.

# Code

```
```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        Stack<Integer> stack = new Stack();
        ListNode curr = head;
        while(curr != null) {
            stack.push(curr.val);
            curr = curr.next;
        }
        curr = head;
        while(curr != null && curr.val == stack.pop()) {
            curr = curr.next;
        }
        return curr == null;
    }
}
```
```

# Approach#3 ( Using Recursion )

As you know, if any problem you can do using stack only then you can use recursion as well ( mostly ).

So we will have one global pointer as curr we will move this pointer once we reach the end and recursion will start from end of the list.

# Code
```
```java
class Solution {
    ListNode curr;
    public boolean isPalindrome(ListNode head) {
        curr = head;
        return solve(head);
    }

    public boolean solve(ListNode head) {
        if(head == null) return true;
        boolean ans = solve(head.next) && head.val == curr.val;
        curr = curr.next;
        return ans;
    }
}
```
```
