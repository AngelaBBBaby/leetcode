# [145. 二叉树的后序遍历](https://leetcode.cn/problems/binary-tree-postorder-traversal/)

难度简单



给你一棵二叉树的根节点 `root` ，返回其节点值的 **后序遍历** 。

 

**示例 1：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/pre1.jpg)

```
输入：root = [1,null,2,3]
输出：[3,2,1]
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

 

**提示：**

- 树中节点的数目在范围 `[0, 100]` 内
- `-100 <= Node.val <= 100`

 

**进阶：**递归算法很简单，你可以通过迭代算法完成吗？



# 思路

**递归：**

- 根据左子树->右子树->根节点的顺序进行递归
- 时间复杂度：O(n)
- 空间复杂度：O(n)

**非递归：**

- 建立一个栈
- 创建一个prev记录上一个出栈的节点
- 将root的左路节点入栈
- 当栈顶的右节点为空或者为prev，出栈栈顶，
- 当栈顶的右节点不为空，令root迭代为栈顶的右节点，重复以上两个步骤
- 将出栈节点的值保存到vector中
- 当栈为空并且root为空时，循环结束，返回vector

- 时间复杂度：O(n)
- 空间复杂度：O(n)

![1600934720-bMXWmu-二叉树前序遍历（迭代法）](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/1600934720-bMXWmu-%E4%BA%8C%E5%8F%89%E6%A0%91%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%EF%BC%88%E8%BF%AD%E4%BB%A3%E6%B3%95%EF%BC%89.gif)



# 代码实现

**C++：**

```
//递归
class Solution {
public:
    void _postorderTraversal(TreeNode *root, vector<int>& arr)
    {
        if (root == nullptr)
        {
            return;
        }
        _postorderTraversal(root->left, arr);
        _postorderTraversal(root->right, arr);
        arr.push_back(root->val);
    }

    vector<int> postorderTraversal(TreeNode *root) {
        vector<int> arr;
        _postorderTraversal(root, arr);
        return arr;
    }
};

//非递归
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) 
    {
        vector<int> arr;
        stack<TreeNode*> st;
        //prev为上一个出栈的节点
        TreeNode* prev = nullptr;
        while(root || !st.empty())
        {
            //走到最左节点
            while(root)
            {
                st.push(root);
                root = root->left;
            }
            TreeNode* top = st.top();

            if(top->right == nullptr || top->right == prev)
            {
                arr.push_back(top->val);
                st.pop();  
                prev = top;
            }
            else
            {
                root = top->right;              
            }
        }
        return arr;
    }
};
```

