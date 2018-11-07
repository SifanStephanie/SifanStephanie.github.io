---
layout: post
title: "Tree Traversal 3"
description: "一般树bfs+dfs遍历"
categories: [Algorithms]
tags: [Tree]
redirect_from:
  - /2018/10/06/
---
 

**Please Read the Tree Traversal 1 & 2 First!**

After discussing about the binary tree, let’s turn to the N-ary tree, which means that a node many have more than two children, and we store these children using List<Node> children;

The basic idea to do the traverse is exactly the same as the binary tree except we need to using **Loop** to traverse all their children one by one.(The same idea as traverse the left and right children of the binary tree.) 

**The BFS Traverse( Leetcode 429. N-ary Tree Level Order Traversal):**

Recall from Binary Tree BFS Traverse, we using QUEUE to store the node in the same level and each time add the left and right children to the queue. Now we just need to add the whole children list into the queue.
For the BFS way:
~~~ ruby
public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> result= new ArrayList<>();
        Queue<Node> q=new LinkedList<>();
        if(root==null)
            return result;
        q.offer(root);
        while(!q.isEmpty()){
            List<Integer> level=new ArrayList<>();
            int size=q.size();
            for(int i=0;i<size;i++){
                Node temp=q.poll();
                level.add(temp.val);
/* Below is the only difference, we need to add all the children of the current node tmp into the queue */
                for(Node c:temp.children){ 
                    q.offer(c);
                }
            }
            result.add(level);
        }
        return result;
    }
~~~

Also as stated before, if we keep track each level, we could achieve the BFS using DFS way.
For the DFS way:
~~~ ruby
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> res = new ArrayList<>();
        dfs(root, 0, res);
        return res;
    }
    private void dfs(Node node, int level, List<List<Integer>> res) {
        if (node == null)
            return;
        if(res.size()-1<level){
            res.add(new ArrayList<>());
        }
        res.get(level).add(node.val);
/* Below is the only difference, instead of just traversing the left and right children, 
we need to dfs all the children of node */
        for (Node n : node.children) dfs(n, level + 1,res);
    }
~~~ 