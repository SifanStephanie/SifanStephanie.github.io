---
layout: post
title: "Tree Traversal 2"
description: "二叉树递归+非递归dfs"
categories: [Algorithms]
tags: [Tree]
redirect_from:
  - /2018/10/01/
---
 

**Please Read the Tree Traversal 1 First!**

**DFS Binary Tree:**
Now let’s talk about the Depth-First-Search(DFS) of a binary tree.

**Recursion:**
There are three DFS ways: **Pre-Order Traversal**, **In-Order Traversal** and **Post-Order Traversal**, and the easiest way to achieve these three traversal ways is to use recursion. Because each time we need to go deeper along some path until reaching the leaf nodes, and then the recursion way could help us to track the path.

Pre-Order Traversal Recursion:
~~~ ruby
List<Integer> res=new ArrayList<>();
    public List<Integer> preorderTraversal(TreeNode root){
        preOrder(root);
        return res;  
    }
    private void preOrder(TreeNode root){
        if(root==null)
            return;
        /* add the value first and then traverse the left and then right child.*/
        res.add(root.val); 
        preOrder(root.left);
        preOrder(root.right);
    }
~~~
In-Order Traversal Recursion:
~~~ ruby
List<Integer> res=new ArrayList<>();
    public List<Integer> inorderTraversal(TreeNode root){
        inOrder(root);
        return res;  
    }
    private void inOrder(TreeNode root){
        if(root==null)
            return;
        inOrder(root.left); // we need to visit the left first
        /* after visit the left child of the node, 
        we then visit the node and add the value. */
        res.add(root.val); 
        inOrder(root.right);// then we go to the right child of the node
    }
~~~
Post-Order Traversal Recursion:
~~~ ruby
List<Integer> res=new ArrayList<>();
    public List<Integer> postorderTraversal(TreeNode root) {
        postOrder(root);
        return res;

    }
    private void traverse(TreeNode root){
        if(root==null)
            return ;
        postOrder(root.left);
        postOrder(root.right);
        /* after visiting the left and the right children, 
        we visit the node itself at last.*/
        res.add(root.val); 
    }
~~~

From the above these recursion codes, we could easily find that using the recursion to do the traversal is really simple, just keep in mind at what order to traverse the tree. To be simplify, just remind the position of visiting the node itself! 

1, preOrder, visit the node first!

2, inOrder, visit the node between the left and the right child!

3, postOrder, visit the node last!

---
**Iteration:**

One way to practice the ability of writing code and better understating recursion is to change the recursion into iteration. It is actually not that hard because the recursion has persevered the inter-results in stacks automatically, we could also use the stacks to persevere the inter-result by ourselves through pushing and poping.

For the elegant of the code and the unified form, we use the same Structure for these three traverse. But there is a slightly different change in post-Order Traversal. We will discuss the detail later.

**Pre-Order Traversal Iteration (144. Binary Tree Preorder Traversal):**
~~~ ruby
public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode p = root;
        while(!stack.isEmpty() || p != null) {
            if(p != null) {
                stack.push(p);
                res.add(p.val);  // visit the node FIRST!
                p = p.left; 
            } else {
                TreeNode node = stack.pop();
                p = node.right;
            }
        }
        return res;
    }
~~~

**In-Order Traversal Iteration (94. Binary Tree Inorder Traversal):**
~~~ ruby
public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode p = root;
        while(!stack.isEmpty() || p != null) {
            if(p != null) {
                stack.push(p);
                p = p.left; 
            } else {
                TreeNode node = stack.pop();
                res.add(node.val);  // visit the node after all left children
                p = node.right;
            }
        }
        return res;
    }
~~~

**Post-Order Traversal Iteration (145. Binary Tree Postorder Traversal):**

First let’s look at the tree we have used in Tree Traversal 1.
![image01](http://sifanstephanie.github.io/assets/images/posts/tree1.png)

The Post-Order Traversal is DBEFCA because we first visit the left chid and right chid and finally visit the node itself. Now let’s think about the Pre-Order Traversal, as stated before, we go to the node itself first, and then its children from left to right. Therefore, if we go to the node itself first still, and then its children but this time from right to left, what could we get? Yes, the reverse of the order of the Pots-Order Traversal. 

That is the reason why we use the LinkedList structure here, because we need to add the result every time at the beginning of the result list (for the reverse). The difference between LinkedList and ArrayList is that ArrayList is a dynamic array, if we want to add something in the beginning, we need to move all the element in the array one to the right, this would cause O(n). However, the LinkedList is a singly linked list connecting each other with ptr, so we just set up a connection at the beginning of the list for inserting something at the front, and this would cause just O(1). Then the only thing to do is traverse the right children first and then left.
~~~ ruby
public List<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> res = new LinkedList<>();// using linked list
        Stack<TreeNode> stack = new Stack<>();
        TreeNode p = root;
        while(!stack.isEmpty() || p != null) {
            if(p != null) {
                stack.push(p);
                res.addFirst(p.val);  // just ad the preorder but adding at the beginning to make the reverse.
                p = p.right;             // visit the right children first
            } else {
                TreeNode node = stack.pop();
                p = node.left;           // then visit the left children
            }
        }
        return res;
    }
~~~