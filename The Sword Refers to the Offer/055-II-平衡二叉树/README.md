# [剑指 Offer 55 - II. 平衡二叉树](https://leetcode.cn/problems/ping-heng-er-cha-shu-lcof/)

简单



输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

 

**示例 1:**

给定二叉树 `[3,9,20,null,null,15,7]`

```
    3
   / \
  9  20
    /  \
   15   7
```

返回 `true` 。

**示例 2:**

给定二叉树 `[1,2,2,3,3,null,null,4,4]`

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

返回 `false` 。

 

**限制：**

- `0 <= 树的结点个数 <= 10000`



# 思路

**深度优先搜索（后序遍历）：**

- 建立后序遍历算法

- 递归计算节点 `root` 的左子树的深度
- 递归计算节点 `root` 的右子树的深度
- 当`root` 为空时返回
- 返回`右子树的深度-左子树的深度+1`
- 当每个节点的左子树与右子树的深度差不大于1时，返回true，否则返回false

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    bool isBalanced(TreeNode* root)
    {
        if(!root)
            return true;
        return (abs(DFS(root->left) - DFS(root->right))<=1) && isBalanced(root->left) && isBalanced(root->right);
        
    }

    int DFS(TreeNode* root)
    {
        if(!root)
            return 0;
        return max(DFS(root->left), DFS(root->right))+1;
    }
};
```

