# [剑指 Offer 28. 对称的二叉树](https://leetcode.cn/problems/dui-cheng-de-er-cha-shu-lcof/)

简单



请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

`  1   / \  2  2 / \ / \ 3  4 4  3`
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

```
  1   / \  2  2   \  \   3   3
```

 

**示例 1：**

```
输入：root = [1,2,2,3,4,4,3]
输出：true
```

**示例 2：**

```
输入：root = [1,2,2,null,3,null,3]
输出：false
```

 

**限制：**

```
0 <= 节点个数 <= 1000
```



# 思路

**递归：**

- 建立递归函数，p指针和q指针一开始都指向这棵树的根
- p右移时，q左移，p左移时，q右移
- 每次检查当前 ppp 和 qqq 节点的值是否相等，再判断左右子树是否对称
- 若都相等且遍历完树，则返回true，否则返回false
- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    bool _isSymmetric(TreeNode* p, TreeNode* q)
    {
        if(!p && !q)
            return true;
        if(!p || !q)
            return false;
        return p->val == q->val && _isSymmetric(p->left, q->right)
                         && _isSymmetric(p->right, q->left);
    }
    
    bool isSymmetric(TreeNode* root)
    {
        return _isSymmetric(root, root);
    }
};
```

