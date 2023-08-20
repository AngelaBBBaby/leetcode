# [剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode.cn/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

中等



输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。

 

为了让您更好地理解问题，以下面的二叉搜索树为例：

 

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/bstdlloriginalbst.png)

 

我们希望将这个二叉搜索树转化为双向循环链表。链表中的每个节点都有一个前驱和后继指针。对于双向循环链表，第一个节点的前驱是最后一个节点，最后一个节点的后继是第一个节点。

下图展示了上面的二叉搜索树转化成的链表。“head” 表示指向链表中有最小元素的节点。

 

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/bstdllreturndll.png)

 

特别地，我们希望可以就地完成转换操作。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继。还需要返回链表中的第一个节点的指针



# 思路

**层序遍历：**

- 建立层序遍历函数，建立变量`pre`保存当前节点的上一个节点，`head`保存头结点

- 层序遍历`root`，找到最左子节点，令其为`head`，令其为`pre`
- 每当找到一个节点，将该节点双向链上`pre`后，令其为`pre`

- 当遍历结束，令`pre->right = head，head->left = pre`（首位节点相连），返回head

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    Node* treeToDoublyList(Node* root)
    {
        if(!root)
            return nullptr;
        level_traversal(root);
        head->left = pre;
        pre->right = head;
        return head;
    }

    void level_traversal(Node* cur)
    {
        if(!cur)
            return;
        level_traversal(cur->left);
        if(pre)
        {
            pre->right = cur;
            cur->left = pre;
            pre = cur;
        }
        else
        {
            head = cur;
            pre = cur;
        }
        level_traversal(cur->right);
    }

    Node* pre, *head;
};
```

