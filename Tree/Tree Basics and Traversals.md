Introduction to Trees

>   
> **_A **Tree** is a non-linear data structure where each node is connected to a number of nodes with the help of pointers or references._**  

  
  
A Sample tree is as shown below:  
![](https://www.geeksforgeeks.org/wp-content/uploads/tree.jpg)  
  
**Basic Tree Terminologies**:  

- **Root**: The root of a tree is the first node of the tree. In the above image, the root node is the node 30.
- **Edge**: An edge is a link connecting any two nodes in the tree. For example, in the above image there is an edge between node **11** and **6**.
- **Siblings**: The children nodes of same parent are called siblings. That is, the nodes with same parent are called siblings. In the above tree, nodes _5, 11, and 63_ are siblings.
- **Leaf Node**: A node is said to be the leaf node if it has no children. In the above tree, node **15** is one of the leaf nodes.
- **Height of a Tree**: Height of a tree is defined as the total number of levels in the tree or the length of the path from the root node to the node present at the last level. The above tree is of height **2**.

**Binary Tree Traversals**

Unlike linear data structures (Array, Linked List, Queues, Stacks, etc.), which have only one logical way to traverse them, trees can be traversed in different ways. Following are the generally used ways for traversing trees:  
  
![Example Tree](https://media.geeksforgeeks.org/wp-content/cdn-uploads/2009/06/tree12.gif "tree12")  
  

- Inorder (Left, Root, Right) : 4 2 5 1 3
- Preorder (Root, Left, Right) : 1 2 4 5 3.
- Postorder (Left, Right, Root) : 4 5 2 3 1

**Inorder traversal**
