# [剑指 Offer 37. 序列化二叉树](https://leetcode.cn/problems/xu-lie-hua-er-cha-shu-lcof/)

困难



请实现两个函数，分别用来序列化和反序列化二叉树。

你需要设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

**提示：**输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 [LeetCode 序列化二叉树的格式](https://support.leetcode-cn.com/hc/kb/article/1567641/)。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。

 

**示例：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/serdeser.jpg)

```
输入：root = [1,2,3,null,null,4,5]
输出：[1,2,3,null,null,4,5]
```



# 思路

**层序遍历：**

**序列化：**

- 建立`queue q`保存经过的结点，建立`string s`保存节点的值
- 层序遍历`root`，将经过的节点入`q`，将节点的值保存到`s`中
- 遍历结束，拼接s，用`，`隔开每个值，返回s
- 时间复杂度：O(n)
- 空间复杂度：O(n)

**反序列化：**

- 建立`vecrot<string> v`保存`data`经过处理后所有字符（剔除`，`），建立`queue q`保存经过的节点，建立`TreeNode* root`为反序列化的树结构
- 遍历`v`，将经过的节点入`q`，链接`q->front`节点的左右节点
- 遍历结束，返回`root`

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Codec
{
public:
    string serialize(TreeNode* root)
    {
        string res;
        if (!root) 
            return res;
        queue<TreeNode*> q;
        q.push(root); 

        while(!q.empty())
        {
            TreeNode* front = q.front();
            q.pop();
            if(front)
            {
                res += to_string(front->val) + ',';
                q.push(front->left);
                q.push(front->right);
            }
            else
                res += "null,";
        }
        return res.substr(0, res.size() - 1);
    }

    TreeNode* deserialize(string data)
    {
        if (data.empty()) 
            return nullptr;
        vector<string> v = split(data);
        
        queue<TreeNode*> q;
        TreeNode* root = new TreeNode(stoi(v[0]));
        q.push(root);
        int i = 1;

        while (!q.empty())
        {
            TreeNode* front = q.front();
            q.pop();
            if (v[i] != "null")
            {
                front->left = new TreeNode(stoi(v[i]));
                q.push(front->left);
            }
            ++i;
            if (v[i] != "null")
            {
                front->right = new TreeNode(stoi(v[i]));
                q.push(front->right);
            }
            ++i;
        }
        return root;
    }

    vector<string> split(string& s)
    {
        vector<string> res;
        int n = s.size();
        int i = 0;
        while (i < n)
        {
            int j = i + 1;
            while (j < n && s[j] != ',')
                ++j;
            res.push_back(s.substr(i, j - i));
            i = j + 1;
        }
        return res;
    }
};
```

