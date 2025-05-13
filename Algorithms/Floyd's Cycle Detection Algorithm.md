*This algorithm is used to ****find a loop**** in a ****linked list****. It uses two pointers one moving ****twice**** as ****fast**** as the other one.

While traversing the linked list **one** of these things will occur-

- The ****Fast**** pointer may reach the end (NULL) which shows that there is no loop in the linked list.
- The ****Fast**** pointer again catches the slow pointer at some time therefore a loop exists in the linked list.

The idea is to start with the ****two pointers slow**** and ****fast****, both starting at the ****head**** of the linked list.

- While traversing the List:
    - ****slow**** pointer will move one step at a time.
    - ****fast**** pointer moves two steps at a time.
    - If there’s a ****cycle****, the fast pointer will eventually catch up with the slow pointer within the cycle because it’s moving faster.
    - If there’s ****no cycle****, the fast pointer will reach the end of the list (i.e., it will become ****NULL****).
- When the slow and fast pointers meet, a ****cycle**** or ****loop**** exists.

Initially, **both** the cars are at **flag-1** together for the first time.

  
![Find loop in Singly Linked List](https://files.codingninjas.in/article_images/floyd-s-cycle-finding-algorithm-2-1657036934.webp)

When the next reading was taken, **Car B** has already taken a leap and reached **flag-3** while **Car M** was at **flag-2**.

  
![Find loop in Singly Linked List](https://files.codingninjas.in/article_images/floyd-s-cycle-finding-algorithm-3-1657036934.webp)

In the next time interval **Car B** has reached **flag-5** and **Car M** is at **flag-3**.

  
![Find loop in Singly Linked List](https://files.codingninjas.in/article_images/floyd-s-cycle-finding-algorithm-4-1657036935.webp)

Now **Car B** is at **flag-7** and **Car-M** is at **flag-4**.

  
![Find loop in Singly Linked List](https://files.codingninjas.in/article_images/floyd-s-cycle-finding-algorithm-5-1657036935.webp)

Well **Car B** has completed the loop, still unaware, and reaches **flag-3** whereas **Car M** is at **flag-5**.

  
![Find loop in Singly Linked List](https://files.codingninjas.in/article_images/floyd-s-cycle-finding-algorithm-6-1657036935.webp)

Moving ahead in loop **Car B** reaches **flag-5** and **Car-M** has reached **flag-6**.

![Find loop in Singly Linked List](https://files.codingninjas.in/article_images/floyd-s-cycle-finding-algorithm-7-1657036936.webp)

At this instant, **both are at the same flag**. So they will come to notice that they are **stuck in a loop**.

  
![Find loop in Singly Linked List](https://files.codingninjas.in/article_images/floyd-s-cycle-finding-algorithm-8-1657036936.webp)

  // Function to find the length of a loop in the linked list.
    
    public int countNodesinLoop(Node head) {
        Node slow =head;
        Node fast=head.next;
      while(slow!=fast)
       {
           if(fast==null || fast.next==null)
              return 0;
         fast=fast.next.next;
         slow=slow.next;
      }
      int size=1;
       fast=fast.next;
       while(fast!=slow)
       {
           fast=fast.next;
           size++;
       }
       return size; 
    }
}
## Find the Starting Node of a Cycle in a Linked List

To find the starting node of a cycle in a linked list, follow the steps below:

> - Using above algorithm [](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/)we can find the ****meeting point (if cycle exists)**** where the slow and fast pointers ****intersect**** inside the cycle.
> - After detecting the cycle, reset one pointer ****(slow)**** to the ****head**** of the list. Keep the other pointer ****(fast)**** at the meeting point.
> - Move both pointers ****one s****tep at a time. The node where they meet again is the ****start**** of the cycle.

```
// Function to detect and remove loop
// in a linked list that may contain loop
static Node detectAndRemoveLoop(Node head)
{
  // If list is empty or has 
  // only one node without loop
  if (head == null || head.next == null)
    return null;

  Node slow = head, fast = head;

  // Move slow and fast 1 
  // and 2 steps ahead 
  // respectively.
  slow = slow.next;
  fast = fast.next.next;

  // Search for loop using 
  // slow and fast pointers
  while (fast != null && 
         fast.next != null) 
  {
    if (slow == fast)
      break;
    slow = slow.next;
    fast = fast.next.next;
  }

  // If loop does not exist
  if (slow != fast)
    return null;

  // If loop exists. Start slow from
  // head and fast from meeting point.
  slow = head;
  while (slow != fast) 
  {
    slow = slow.next;
    fast = fast.next;
  }

  return slow;
}
```