# [剑指 Offer 32 - II. 从上到下打印二叉树 II](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

简单



从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

 

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
  [9,20],
  [15,7]
]
```

 

**提示：**

1. `节点总数 <= 1000`



# 思路

**广度优先：**

- 建立队列`q`，根元素入队列，建立`vector<vector<int\>> vv`保存结果
- 当队列不为空的时候，求出当前队列的长度`size`（每层的个数），依次从队列中取`size`个元素进行拓展，然后进入下一次迭代，建立`vector v`保存每层的值
- 每次迭代结束，将`v`的值保存至`vv`中
- 当队列为空时，迭代结束，返回`vv`

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
//广度优先
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
        while(!q.empty())
        {
            vector<int> v;
            int size = q.size();
            while(size)
            {
                if(q.front()->left)
                    q.push(q.front()->left);
                if(q.front()->right)
                    q.push(q.front()->right);
                v.push_back(q.front()->val);
                q.pop();
                --size;
            }
            vv.push_back(v);
        }
        return vv;
    }
};
```

