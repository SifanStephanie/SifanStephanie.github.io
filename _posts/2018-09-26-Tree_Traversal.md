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

Here we just talk about the tree traversal based on this tree below:
![image01](http://sifanstephanie.github.io/assets/images/posts/tree1.png)


**BFS:** BFS means that we first go through all the children which connected to the root(A), which is B and C. And then we search from the first child B to get D, and we search from the second child C to get E and F. Because we could not get any nodes from D E and F. Then it is done! The sequence is *ABCDEF*

**DFS:** For binary trees, there are three kinds of DFS: *Pre-Order Traversal, In-Order Traversal and Post-Order Traversal*. The total idea of these three traversal is to go as deep as it can to reach the leaf node, and since it could not go deeper from a leaf node, at this time, we choose another path and then go as deep as we can.

But how to choose the path?

**Pre-Order Traversal** tells us to “visit” the current node first and its child nodes. Always the left child and then the right child. The sequence is *ABDCEF*

**In-Order Traversal** “visit” the left branch, then the current node, and finally the right branch. The sequence is *DBAECF*

**Post-Order Traversal** “visit” its child nodes before the current node. The sequence is *DBEFCA*

Therefore, we could determine which algorithm best fits the problem by viewing the position of the current node that we want to visit. But the most common of these is In-Order Traversal.

---
Now let’s talk about how to write code to do BFS and DFS on diary tree & non-binary tree.

**BFS Binary Tree Traverse:**
We want to store the nodes'value of each level from left to right in a list, and return the list of every level from top to bottom. *(leetcode 102. Binary Tree Level Order Traversal)*. That is we want to return **[[‘A’],[‘B’,’C’],[‘D’,’E’,’F’]]** for the above tree.

The general Idea is to store all the node on the same level, and using these nodes to get to their chidden, which is on the next level. 

How to store all the nodes of the same? Yes, we think about using a QUEUE! Because we could get value by FIFO order to traverse from left to right. Below is a very traditional way to do BFS of a binary tree and it does use the idea of BFS because we just traverse each level of the tree from left to right and top to bottom.


~~~ ruby
public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res=new ArrayList<>();    // store the result
        Queue<TreeNode> q=new LinkedList<>();    // store the TreeNode
        if(root==null)    // if there is no tree node in a tree
            return res;
        q.offer(root); // root is the level 0.
        /* up till now, the q contains all the node on level 0, which is the root node.*/
        while(!q.isEmpty()){    // until we visit all the nodes
            /* get the size of current level ! 
            this is really important since we would get out the current nodes on level x and put in the nodes on level x+1, 
            and this operation would break up the level constrain of the queue.*/
            int size=q.size();    

            // make a new level to store nodes
            List<Integer> level=new ArrayList<>();

            /* we just put out all the nodes from the same level one by one and add their children in to the new level list */
            for(int i=0;i<size;i++){
                TreeNode tmp=q.poll();
                level.add(tmp.val);//    visit the node
                if(tmp.left!=null)// add the left child of the current node
                    q.offer(tmp.left);
                if(tmp.right!=null) // add the right child of the current node
                    q.offer(tmp.right);
            }
            /* after we traverse all the nodes of the same level. we add the final level list to the result.*/
            res.add(level);
        }
        return res;
    }
~~~ 

However, could we use the DFS thoughts to solve this problem? definitely true!
Let’s think about the DFS methods again. we need to go alone one road until we could not reach further (a leaf node). Then we can back and choose another way. Therefore, the level would increase by 1 each time we go to next level, and we need to create a new level list to store the new level just as the above code. When we come back, we only do one thing: add the node into the already exists level lists.

~~~ ruby
public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res=new ArrayList<>(); // store the result
        traverse(root,0,res);
        return res;
    }
    private void traverse(TreeNode node, int level, List<List<Integer>> res){
        if(node==null) // reach the null of the tree
            return;

        /* first let’s think about what is stored in res? 
        It is the List<Integer> which means res contains the list of each level. 
        So when the res’s size is smaller than the current size of level we have reached, we need to add a new level list. 
        NOTICE: the level starts from 0 */
        if(res.size()-1<level){ 
            res.add(new ArrayList<>());
        }
        // add the node into the current level list
        res.get(level).add(node.val);
        //visit the left child and level increase by 1 
        traverse(node.left,level+1,res); 
        // visit the right child and level increase by 1
        traverse(node.right,level+1,res);
    }
~~~


