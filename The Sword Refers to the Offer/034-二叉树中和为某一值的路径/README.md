# [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode.cn/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

中等



给你二叉树的根节点 `root` 和一个整数目标和 `targetSum` ，找出所有 **从根节点到叶子节点** 路径总和等于给定目标和的路径。

**叶子节点** 是指没有子节点的节点。

 

**示例 1：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/pathsumii1.jpg)

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```

**示例 2：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/pathsum2.jpg)

```
输入：root = [1,2,3], targetSum = 5
输出：[]
```

**示例 3：**

```
输入：root = [1,2], targetSum = 0
输出：[]
```

 

**提示：**

- 树中节点总数在范围 `[0, 5000]` 内
- `-1000 <= Node.val <= 1000`
- `-1000 <= targetSum <= 1000`



# 思路

**回溯：**

- 建立DFS函数，建立` vector<int> v`保存路径值，建立`vector<vector<int>> vv`保存目标路径
- 前序遍历`root`，当`root为空`，回溯节点
- 每经过一个节点，将节点的值保存到`v`，令`target - root->val`，每回溯一个节点，将节点的值从`v`中剔除
- 当`target = 0 && !root->left && !root->right`，将`v`中的路径保存到`vv`
- 遍历完`root`， 返回vv

- 时间复杂度：O(n)
- 时间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    void DFS(TreeNode* root, int target)
    {
        if(!root)
            return;
        v.push_back(root->val);
        target -= root->val;
        if(target == 0 && !root->left && !root->right)
            vv.push_back(v);
        DFS(root->left, target);
        DFS(root->right, target);
        v.pop_back();
    }

    vector<vector<int>> pathSum(TreeNode* root, int target) 
    {
        DFS(root, target);
        return vv;
    }

    vector<int> v;
    vector<vector<int>> vv;
};
```

