# [剑指 Offer 07. 重建二叉树](https://leetcode.cn/problems/zhong-jian-er-cha-shu-lcof/)

中等



输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

 

**示例 1:**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

**示例 2:**

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

 

**限制：**

```
0 <= 节点个数 <= 5000
```



# 思路

**分治：**

- 建立`unordered_map um`存储中序遍历数组的下标，建立构建二叉树函数
- 前序遍历可以确定当前根节点的值，可在`um`中找到根节点，从而确定左子树的节点个数和右子树的节点个数
- 找到当前根节点的左子节点和右子节点，分别以左子节点为根和右子节点为根重复以上步骤
- 通过构建二叉树函数将其组成二叉树，返回其根节点

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    //root：前序遍历中根节点的索引
    //i：中序遍历中根节点的索引
    //left、right：中序遍历中左子树右子树的范围
    TreeNode* _buildTree(vector<int>& v, unordered_map<int, int>& um, int root, int left, int right)
    {
        if(left > right)
            return nullptr;
        TreeNode* node = new TreeNode(v[root]);
        int i = um[v[root]];
        node->left = _buildTree(v, um, root + 1, left, i - 1);
        node->right = _buildTree(v, um, root + i - left + 1, i + 1, right);
        return node;
    }

    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder)
    {
        vector<int> v(preorder);
        unordered_map<int, int> um;
        for(int i = 0; i < inorder.size(); ++i)
            um[inorder[i]] = i;
        return _buildTree(v, um, 0, 0, inorder.size() - 1);
    }
};
```

