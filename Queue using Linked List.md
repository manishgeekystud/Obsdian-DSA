## **1. Concept Recap — What is a Queue?**

A **Queue** is a linear data structure that follows the **FIFO (First In, First Out)** principle:

- The **first** element inserted is the **first** to be removed.
    
- Think of it like people standing in a line at a ticket counter.
    

**Two main operations:**

- **enqueue(x)** → insert an element at the **rear**.
    
- **dequeue()** → remove an element from the **front**.
    

---

## **2. Why Linked List for Queue?**

We can implement a queue using:

- **Array** → Fixed size, requires resizing when full.
    
- **Linked List** → Dynamic size, no need for resizing.
    

**Advantages of Linked List Queue:**

- Can grow and shrink dynamically.
    
- Enqueue/Dequeue operations are **O(1)** if we maintain both head and tail references.
    

---

## **3. Structure of a Linked List Queue**

A **Queue using Linked List** will have:

- **Node** (contains `data` and `next` pointer)
    
- **Front** pointer → points to the first element (for dequeue)
    
- **Rear** pointer → points to the last element (for enqueue)
    

**Diagram:**

`Front → [data|next] → [data|next] → [data|null] ← Rear`

---

## **4. Node Structure**

Each node will have:


---

## **5. Queue Class with Linked List**

We maintain:

- `front` → points to first node.
    
- `rear` → points to last node.
    
- Optional: `size` → number of elements in the queue.
    

---

## **6. Operations in Detail**

### **1) isEmpty()**

Check if the queue is empty.

`public boolean isEmpty() {     return front == null; }`

---

### **2) enqueue(int data)**

**Steps:**

1. Create a new node.
    
2. If queue is empty → set both `front` and `rear` to new node.
    
3. Else → link `rear.next` to new node and update `rear`.
    

**Time Complexity:** O(1)  
**Code:**

java
```java
public void enqueue(int data) {
    Node newNode = new Node(data);
    if (rear == null) { // Queue is empty
        front = rear = newNode;
        return;
    }
    rear.next = newNode;
    rear = newNode;
}

```
---

### **3) dequeue()**

**Steps:**

1. If queue is empty → print error or throw exception.
    
2. Store `front.data` to return.
    
3. Move `front` to `front.next`.
    
4. If `front` becomes `null` → set `rear` to `null`.
    

**Time Complexity:** O(1)  
**Code:**

java
```java
public int dequeue() {
    if (front == null) {
        throw new RuntimeException("Queue is empty");
    }
    int value = front.data;
    front = front.next;
    if (front == null) { // Queue became empty
        rear = null;
    }
    return value;
}

```
---

### **4) peek()**

Return the element at the front without removing it.
```java
public int peek() {
    if (front == null) {
        throw new RuntimeException("Queue is empty");
    }
    return front.data;
}

```


---

### **5) size()**

Optional helper method.
```java
public int size() {
    int count = 0;
    Node temp = front;
    while (temp != null) {
        count++;
        temp = temp.next;
    }
    return count;
}

```

Or maintain a `size` variable and update it in enqueue/dequeue for O(1) size retrieval.

---

## **7. Full Java Implementation**

```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class QueueUsingLinkedList {
    private Node front, rear;

    public QueueUsingLinkedList() {
        front = rear = null;
    }

    public boolean isEmpty() {
        return front == null;
    }

    public void enqueue(int data) {
        Node newNode = new Node(data);
        if (rear == null) {
            front = rear = newNode;
            return;
        }
        rear.next = newNode;
        rear = newNode;
    }

    public int dequeue() {
        if (front == null) {
            throw new RuntimeException("Queue is empty");
        }
        int value = front.data;
        front = front.next;
        if (front == null) {
            rear = null;
        }
        return value;
    }

    public int peek() {
        if (front == null) {
            throw new RuntimeException("Queue is empty");
        }
        return front.data;
    }

    public void display() {
        if (front == null) {
            System.out.println("Queue is empty");
            return;
        }
        Node temp = front;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
        System.out.println();
    }
}

public class Main {
    public static void main(String[] args) {
        QueueUsingLinkedList queue = new QueueUsingLinkedList();
        
        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);

        queue.display(); // 10 20 30

        System.out.println("Dequeued: " + queue.dequeue()); // 10
        System.out.println("Front element: " + queue.peek()); // 20

        queue.display(); // 20 30
    }
}

```

---

## **8. Time & Space Complexity**

|Operation|Time Complexity|Space Complexity|
|---|---|---|
|enqueue|O(1)|O(1) extra|
|dequeue|O(1)|O(1) extra|
|peek|O(1)|O(1) extra|
|isEmpty|O(1)|O(1) extra|

**Space complexity** overall: **O(n)** (for storing `n` elements in the linked list).

---

## **9. Common Pitfalls**

- Forgetting to update `rear` to `null` when queue becomes empty.
    
- Not handling the case when both `front` and `rear` are `null` in enqueue/dequeue.
    
- Accidentally traversing the entire list in enqueue (should be O(1)).