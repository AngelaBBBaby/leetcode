# [剑指 Offer 18. 删除链表的节点](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

简单



给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

**注意：**此题对比原题有改动

**示例 1:**

```
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```

**示例 2:**

```
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```

 

**说明：**

- 题目保证链表中节点的值互不相同
- 若使用 C 或 C++ 语言，你不需要 `free` 或 `delete` 被删除的节点



# 思路

**迭代：**

- 遍历链表，找到目标值
- 将目标值的prev->next链上cur->next
- 当目标值为head的时候特殊处理
- 修改完成，返回head

- 时间复杂度 ：O(n)
- 空间复杂度 ：O(1)

**递归：**

- 建立递归函数，将head->next和val作为实参进行递归

- 当head为空时返回空
- 当head->val不为val时递归head->next，当head->val为val时结束递归，返回head->next

- 时间复杂度 ：O(n)
- 空间复杂度 ：O(n)



# 代码实现

**C++：**

```
//迭代
class Solution {
public:
    ListNode* deleteNode(ListNode* head, int val)
    {
        ListNode* prev = head;
        ListNode* cur = head;
        while(cur)
        {
            if(cur->val == val)
            {
                if(cur == head)
                {
                    head = cur->next;
                }
                else
                    prev->next = cur->next;
                return head;
            }
            prev = cur;
            cur = cur->next;
        }
        return head;
    }
};

//递归
class Solution {
public:
    ListNode* deleteNode(ListNode* head, int val)
    {
        if (head == nullptr)
            return head;
        if (head->val == val)
        return head->next;
        head->next = deleteNode(head->next, val);
        return head;
    }
};
```

