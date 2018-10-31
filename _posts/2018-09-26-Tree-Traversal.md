---
layout: post
title: "Tree Traversal"
description: "二叉树递归+非递归版本的dfs+bfs 非二叉树遍历"
categories: [Algorithms]
tags: [Tree]
redirect_from:
  - /2018/09/26/
---

There are two general ways for traversing a tree (not restrict to trees’ traversal): **the Depth-First-Search(DFS) & the Breadth-First-Search(BFS).** These two ways are both traverse method while using different ways.


The traverse means that we start from some point P, and we go through all the points which connected to P, and repeat these process until all the points have been  visited. 

Here we just talk about the tree traversal.

**BFS:** BFS means that we first go through all the children which connected to the root(A), which is B and C. And then we search from the first child B to get D, and we search from the second child C to get E and F. Because we could not get any nodes from D E and F. Then it is done! The sequence is *ABCDEF*

**DFS:** For binary trees, there are three kinds of DFS: *Pre-Order Traversal, In-Order Traversal and Post-Order Traversal*. The total idea of these three traversal is to go as deep as it can to reach the leaf node, and since it could not go deeper from a leaf node, at this time, we choose another path and then go as deep as we can.

But how to choose the path?

Pre-Order Traversal tells us to “visit” the current node first and its child nodes. Always the left child and then the right child. The sequence is *ABDCEF*

In-Order Traversal “visit” the left branch, then the current node, and finally the right branch. The sequence is *DBAECF*

Post-Order Traversal “visit” its child nodes before the current node. The sequence is *DBEFCA*

Therefore, we could determine which algorithm best fits the problem by viewing the position of the current node that we want to visit. But the most common of these is In-Order Traversal.

