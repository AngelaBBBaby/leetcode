# [剑指 Offer 27. 二叉树的镜像](https://leetcode.cn/problems/er-cha-shu-de-jing-xiang-lcof/)

简单



请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

`   4   /  \  2   7 / \  / \ 1  3 6  9`
镜像输出：

```
   4   /  \  7   2 / \  / \ 9  6 3  1
```

 

**示例 1：**

```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

 

**限制：**

```
0 <= 节点个数 <= 1000
```





# 思路

**递归：**

- 从根节点开始，递归地对树进行遍历

- 从叶子节点先开始翻转得到镜像
- 当前遍历到的节点root的左右两棵子树都已经翻转，交换两棵子树的位置
- 返回root

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    TreeNode* mirrorTree(TreeNode* root)
    {
        if(!root)
            return nullptr;
        TreeNode* left = mirrorTree(root->left);
        TreeNode* right = mirrorTree(root->right);
        root->left = right;
        root->right = left;
        return root;
    }
};
```

