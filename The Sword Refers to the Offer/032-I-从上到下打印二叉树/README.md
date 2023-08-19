# [剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

中等



从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

 

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回：

```
[3,9,20,15,7]
```

 

**提示：**

1. `节点总数 <= 1000`



# 思路

**广度优先：**

- 建立`queue q`实现层序遍历，并将`root`入队列，建立`vector v`保存值
- 当`q不为空`，将队头的左右节点（存在）入队列，将队头的值保存进`v`，剔除队头
- 当`q为空`，返回`v`

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    vector<int> levelOrder(TreeNode* root)
    {
        vector<int> v;
        if(!root)
            return v;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty())
        {
            v.push_back(q.front()->val);
            if(q.front()->left)
                q.push(q.front()->left);
            if(q.front()->right)
                q.push(q.front()->right);
            q.pop();
        }
        return v;
    }
};
```

