# [剑指 Offer 54. 二叉搜索树的第k大节点](https://leetcode.cn/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

简单



给定一棵二叉搜索树，请找出其中第 `k` 大的节点的值。

 

**示例 1:**

```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
```

**示例 2:**

```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
```

 

**限制：**

- 1 ≤ k ≤ 二叉搜索树元素个数



# 思路

**中序遍历倒序+全局变量：**

- 建立中序遍历倒序函数（降序排列），建立全局变量`target`保存目标值
- 每遍历完一个节点，`--k`，当`k = 0`时，令`target = root->val`
- 遍历完成，返回`target`

- 时间复杂度：O(n)

- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    int target = 0;
    void inorder_traversal(TreeNode* root, int& k)
    {
        if(!root || k <= 0)
            return;
        inorder_traversal(root->right, k);
        if(--k == 0)
        {
            target = root->val;
            return;
        }
        inorder_traversal(root->left, k);
    }

    int kthLargest(TreeNode* root, int k)
    {
        inorder_traversal(root, k);
        return target;
    }
};
```

