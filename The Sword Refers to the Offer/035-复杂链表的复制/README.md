[剑指 Offer 35. 复杂链表的复制](https://leetcode.cn/problems/fu-za-lian-biao-de-fu-zhi-lcof/)



中等



771





相关企业

请实现 `copyRandomList` 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 `next` 指针指向下一个节点，还有一个 `random` 指针指向链表中的任意节点或者 `null`。

 

**示例 1：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/e1.png)

```
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

**示例 2：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/e2.png)

```
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```

**示例 3：**

**![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/e3.png)**

```
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]
```

**示例 4：**

```
输入：head = []
输出：[]
解释：给定的链表为空（空指针），因此返回 null。
```

 

**提示：**

- `-10000 <= Node.val <= 10000`
- `Node.random` 为空（null）或指向链表中的节点。
- 节点数目不超过 1000 



# 思路

**拼接+拆分：**

- 复制原链表
- 将复制链表的每个节点拼接到原链表同节点的后面
- 拆分复制链表和原链表，返回复制链表的头

- 时间复杂度：O(n)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    Node* copyRandomList(Node* head)
    {
        if(!head) 
            return nullptr;
        Node* cur = head;
        while(cur)
        {
            Node* copy = new Node(cur->val);
            copy->next = cur->next;
            cur->next = copy;
            cur = copy->next;
        }
        cur = head;
        while(cur)
        {
            if(cur->random)
                cur->next->random = cur->random->next;
            cur = cur->next->next;
        }
        Node* newhead = head->next;
        Node* pre = head;
        cur = head->next;
        while(cur->next)
        {
            pre->next = pre->next->next;
            cur->next = pre->next->next;
            pre = pre->next;
            cur = pre->next;
        }
        pre->next = nullptr;
        return newhead;
    }
};
```

