## Invert Binary Tree

Invert a binary tree.

**Example:**

Input:

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

Output:

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

## Solution

这道题目很直接，就是反转二叉树。本来这道题目很平常，却因为一位大神而走红。故事完整版可以Google 搜索 Max Invert Binary Tree，这里就不详细说了。

对于二叉树的题目，我们可能会直觉的想到使用递归。这里我们首先保存左子树，然后分别递归地翻转左右子树，最后将root 返回即可。使用递归的方法代码看起来十分简洁。

使用递归的时间复杂度为 O(n)，空间复杂度为 O(n)。

```java
 public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }

        TreeNode tempLeft = root.left;
        root.left = invertTree(root.right);
        root.right = invertTree(tempLeft);

        return root;

    }
```

