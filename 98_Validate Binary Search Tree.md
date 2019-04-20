##  Validate Binary Search Tree

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**Example 1:**

```
Input:
    2
   / \
  1   3
Output: true
```

## Solution

这道题是给定一个二叉树，判断这个树是不是二叉搜索树（BST）。

我们首先来回顾一下什么是二叉搜索树。二叉搜索树是指空树或者具有下列性质的二叉树：

- 左子树上所有节点的值均小于它的根节点的值；
- 右子树上所有节点的值均大于它的根节点的值；
- Recursively，左右子树也分别为二叉搜索树。

了解了二叉搜索树的性质之后，我们再来了解一下中序遍历。中序遍历是遍历完左子树之后，再输出该节点的值，然后遍历右子树，即左根右。

了解了上述概念之后，我们可以分析一下，如果一棵树是二叉搜索树的话，那么按照中序遍历的话，输出的结果应该是按照升序排序的（不理解的话可以在纸上画一下）。所以这道题常见的思路就是按照中序对树进行遍历，然后判断输出的结果是否是升序即可。

#### Approach1:循环

```java
 public boolean isValidBST(TreeNode root) {
        if (root==null || (root.left == null && root.right == null)){
            return true;
        }
        // 中序遍历树
        List<Integer> list = new ArrayList();
     	// 用来暂存节点的栈
        Stack<TreeNode> treeStack = new Stack<>();
        TreeNode node = root;

        while(node != null || !treeStack.isEmpty()){
            while(node != null){
                treeStack.push(node);
                node = node.left;
            }

            if(!treeStack.isEmpty()){
                TreeNode tNode = treeStack.pop();
                list.add(tNode.val);
                node = tNode.right;
            }
        }

        long temp = Long.MIN_VALUE;
        for(int n : list){
            if (temp >= n){
                return false;
            }
            temp = n;
        }

        return true;
    }
```

#### Approach2:递归

