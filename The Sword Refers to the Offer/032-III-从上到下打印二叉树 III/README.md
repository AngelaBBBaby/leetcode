# [剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

中等



请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

 

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [20,9],
  [15,7]
]
```

 

**提示：**

1. `节点总数 <= 1000`



# 思路

**广度优先：**

- 建立`queue q`实现层序遍历，并将`root`入队列，建立`vector v`保存值，建立`vector<vector<int>> vv`保存每层的值
- 当`q不为空`，将队头的左右节点（存在）入队列，将队头的值保存进`v`，剔除队头
- 每层遍历完，若是偶数层，将v中的值逆置后保存进`vv`，若是奇数层，直接保存进`vv`
- 当`q为空`，返回`vv`

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    vector<vector<int>> levelOrder(TreeNode* root)
    {
        vector<vector<int>> vv;
        if(!root)
            return vv;
        queue<TreeNode*> q;
        q.push(root);
        int line = 1;
        while(!q.empty())
        {
            vector<int> v;
            int size = q.size();
            while(size--)
            {
                v.push_back(q.front()->val);
                if(q.front()->left)
                    q.push(q.front()->left);
                if(q.front()->right)
                    q.push(q.front()->right);
                q.pop();
            }
            if(line % 2 == 0)
                reverse(v.begin(), v.end());
            vv.push_back(v);
            ++line;
        }
        return vv;
    }
};
```

