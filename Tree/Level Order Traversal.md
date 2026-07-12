
In the Level Order Traversal, the binary tree is traversed level-wise starting from the first to last level sequentially.  
  
Consider the below binary tree:  
![](https://www.geeksforgeeks.org/wp-content/uploads/binarytree.png)  
  
The Level Order Traversal of the above Binary Tree will be: **10 20 30 40 50 60 70 80**.  
  
**Algorithm**: The Level Order Traversal can be implemented efficiently using a **Queue**.  

1. Create an empty queue q.
2. Push the root node of tree to q. That is, q.push(root).
3. Loop while the queue is not empty:
    - Pop the top node from queue and print the node.
    - Enqueue node's children (first left then right children) to q
    - Repeat the process until queue is not empty.