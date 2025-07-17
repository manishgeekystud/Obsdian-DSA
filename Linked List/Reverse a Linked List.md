**Examples**: 

> _**Input**: Head of following linked list_   
> _1->2->3->4->NULL_   
> _**Output**: Linked list should be changed to,_   
> _4->3->2->1->NULL_
> 
> _**Input**: Head of following linked list_   
> _1->2->3->4->5->NULL_   
> _**Output**: Linked list should be changed to,_   
> _5->4->3->2->1->NULL_

**Follow the steps below to solve the problem:**

- Initialize three pointers **prev** as NULL, **curr** as **head**, and **next** as NULL.
- Iterate through the linked list. In a loop, do the following:
    - Before changing the **next** of **curr**, store the **next** node 
        - next = curr -> next
    - Now update the **next** pointer of **curr** to the **prev** 
        - curr -> next = prev 
    - Update **prev** as **curr** and **curr** as **next** 
        - prev = curr 
        - curr = next

**Code**
```java
/* Function to reverse the linked list */
	Node reverse(Node node)
	{
		Node prev = null;
		Node current = node;
		Node next = null;
		while (current != null) {
			next = current.next;
			current.next = prev;
			prev = current;
			current = next;
		}
		node = prev;
		return node;
	}

```
