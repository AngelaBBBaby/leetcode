# [144. 二叉树的前序遍历](https://leetcode.cn/problems/binary-tree-preorder-traversal/)

难度简单

1091











给你二叉树的根节点 `root` ，返回它节点值的 **前序** 遍历。

 

**示例 1：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/inorder_1.jpg)

```
输入：root = [1,null,2,3]
输出：[1,2,3]
```

**示例 2：**

```
输入：root = []
输出：[]
```

**示例 3：**

```
输入：root = [1]
输出：[1]
```

**示例 4：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/inorder_5.jpg)

```
输入：root = [1,2]
输出：[1,2]
```

**示例 5：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/inorder_4.jpg)

```
输入：root = [1,null,2]
输出：[1,2]
```

 

**提示：**

- 树中节点数目在范围 `[0, 100]` 内
- `-100 <= Node.val <= 100`

 

**进阶：**递归算法很简单，你可以通过迭代算法完成吗？



# 思路

**递归：**

- 根据根节点->左子树->右子树的顺序进行递归

**非递归：**

- 建立一个栈，将根节点入栈
- 每次当节点出栈，将该节点的右节点和左节点分别进栈（不为空才进栈）
- 将出栈节点的值保存到vector中
- 当栈为空，循环结束，将vector返回



# 代码实现

**C++：**

```
//递归
class Solution {
public:
    void _preorderTraversal(TreeNode *root, vector<int>& arr)
    {
        if (root == nullptr)
        {
            return;
        }
        arr.push_back(root->val);
        _preorderTraversal(root->left, arr);
        _preorderTraversal(root->right, arr);
    }

    vector<int> preorderTraversal(TreeNode *root) {
        vector<int> arr;
        _preorderTraversal(root, arr);
        return arr;
    }
};

//非递归
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) 
    {
        //非递归
        vector<int> arr;
        stack<TreeNode*> st;
        if(root)
            st.push(root);
        while(!st.empty())
        {
            TreeNode* top = st.top();
            arr.push_back(top->val);
            st.pop();
            if(top->right)
                st.push(top->right);
            if(top->left)
                st.push(top->left);
        }
        return arr;
    }
};
```

