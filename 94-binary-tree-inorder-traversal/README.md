# [94. 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)

难度简单



给定一个二叉树的根节点 `root` ，返回 *它的 **中序** 遍历* 。

 

**示例 1：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/inorder_1.jpg)

```
输入：root = [1,null,2,3]
输出：[1,3,2]
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

- 树中节点数目在范围 `[0, 100]` 内
- `-100 <= Node.val <= 100`

 

**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？



# 思路

**递归：**

- 根据左子树->根节点->右子树的顺序进行递归
- 时间复杂度：O(n)
- 空间复杂度：O(n)

**非递归：**

- 建立一个栈
- 将root的所有左子树的左节点入栈
- 当左节点为空时，出栈当前的栈顶，将当前栈顶的右节点（不为空）入栈
- 令root迭代为当前栈顶，重复以上两个步骤
- 将所有出栈节点的值保存到vector中
- 当root为空且栈为空时，结束循环，返回vector

- 时间复杂度：O(n)
- 空间复杂度：O(n)

![1.gif](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/47fff35dd3fd640ba60349c78b85242ae8f4b850f06a282cd7e92c91e6eff406-1.gif)



# 代码实现

**C++：**

```
//递归
class Solution 
{
public:
    void _inorderTraversal(TreeNode* root, vector<int>& arr)
    {
        if (!root)
        {
            return;
        }
        _inorderTraversal(root->left, arr);
        arr.push_back(root->val);
        _inorderTraversal(root->right, arr);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> arr;
        _inorderTraversal(root, arr);
        return arr;
    }
};

//非递归
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) 
    {
        vector<int> arr;
        stack<TreeNode*> st;
        while(!st.empty() || root)
        {
            while(root)
            {
                st.push(root);
                root = root->left;
            }

            root = st.top();
            arr.push_back(root->val);
            st.pop();

            root = root->right;
        }
        return arr;
    }
};
```

