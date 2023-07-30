# [剑指 Offer 24. 反转链表](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/)

难度简单



定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

 

**示例:**

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

 

**限制：**

```
0 <= 节点个数 <= 5000
```



# 思路

**迭代：**

- 建立ListNode* cur和next，分别保存当前节点（头节点的下一个）和当前节点的下一个节点
- 首先令head->next为nullptr
- 令cur->next为head
- 进行迭代（head = cur，cur = next，next = cur->next）
- 当cur为nullptr时，迭代结束，返回head

- 时间复杂度：O(n)
- 空间复杂度：O(1)

**递归：**

- 建立递归函数，形参为当前节点和上一个节点
- 将head和nullptr作为实参调用递归函数
- 递归函数遍历链表，当当前节点不为nullptr，继续递归当前节点为nullptr时，返回上一个节点
- 递归结束，完成链表反转

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
//迭代
class Solution
{
public:
    ListNode* reverseList(ListNode* head)
    {
        if(head == nullptr)
            return head;
        ListNode* cur = head->next;
        ListNode* next = head; //初始化，给不为空的即可
    	head->next = nullptr;
        while(cur)
        {
            if(next)
                next = cur->next;
            cur->next = head;
            head = cur;
            cur = next;
        }
        return head;
    }
};

//递归
class Solution {
public:
    ListNode* _reverseList(ListNode* cur, ListNode* prev)
    {
        if(cur == nullptr)
            return prev;
        ListNode* rl = _reverseList(cur->next, cur);
        cur->next = prev;
        return rl;
    }

    ListNode* reverseList(ListNode* head)
    {
        ListNode* rl = _reverseList(head, nullptr);
        return rl;
    }
};
```

