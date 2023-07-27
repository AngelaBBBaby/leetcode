# [102. 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/)

难度中等



给你二叉树的根节点 `root` ，返回其节点值的 **层序遍历** 。 （即逐层地，从左到右访问所有节点）。

 

**示例 1：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/tree1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：[[3],[9,20],[15,7]]
```

**示例 2：**

```
输入：root = [1]
输出：[[1]]
```

**示例 3：**

```
输入：root = []
输出：[]
```

 

**提示：**

- 树中节点数目在范围 `[0, 2000]` 内
- `-1000 <= Node.val <= 1000`



# 思路

- 创建一个队列来，将root的根节点入队列
- 每出队列一个节点之前，将它的左节点和右节点入队列
- 设定变量sz为当前队列中数的个数，即为层数
- 每个节点遍历结束将出队列的节点的值放入v中
- 每个层数遍历结束将v放入vv中
- 当队列为空时，循环结束，将vv返回

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) 
    {
        queue<TreeNode*> q;
        vector<vector<int>> vv;
        //将根节点入队列
        if(root)
            q.push(root);
        while(!q.empty())
        {
            vector<int> v;
            //建立变量sz记录层数
            int sz = q.size();
            while(sz--)
            {
                //将当前q.front()节点的左节点和右节点入队列后，出队列
                TreeNode* front = q.front();
                v.push_back(front->val);
                q.pop();
                if(front->left)
                    q.push(front->left);
                if(front->right)
                    q.push(front->right);
            }
            vv.push_back(v);
        }
        return vv;
    }
};
```

