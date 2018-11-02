---
layout: post
title: "Tree Traversal 2"
description: "二叉树递归+非递归dfs"
categories: [Algorithms]
tags: [Tree]
redirect_from:
  - /2018/10/01/
---
 

** Please Read the Tree Traversal 1 First! **

**DFS Binary Tree:**
Now let’s talk about the Depth-First-Search(DFS) of a binary tree.

There are three DFS ways: **Pre-Order Traversal**, **In-Order Traversal** and **Post-Order Traversal**, and the easiest way to achieve these three traversal ways is to use recursion. Because each time we need to go deeper along some path until reaching the leaf nodes, and then the recursion way could help us to track the path.

**Pre-Order Traversal Recursion:**
~~~ Ruby
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
**In-Order Traversal Recursion:**
~~~ Ruby
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
**Post-Order Traversal Recursion:**
~~~ Ruby
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
