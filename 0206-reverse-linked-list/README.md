# [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

难度简单



给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

 

**示例 1：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/rev1ex1.jpg)

```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```

**示例 2：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/rev1ex2.jpg)

```
输入：head = [1,2]
输出：[2,1]
```

**示例 3：**

```
输入：head = []
输出：[]
```

 

**提示：**

- 链表中节点的数目范围是 `[0, 5000]`
- `-5000 <= Node.val <= 5000`

 

**进阶：**链表可以选用迭代或递归方式完成反转。你能否用两种方法解决这道题？



# 思路

**递归法：**

- 定义两个指针： pre 和 cur ；pre 在前 cur 在后
- 每次让 pre 的 next 指向 cur 
- 实现一次局部反转局部反转完成之后，pre 和 cur 同时往前移动一个位置循环上述过程，直至 pre 到达链表尾部

- 时间复杂度：O(n)
- 空间复杂度：O(1)

![迭代.gif](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/7d8712af4fbb870537607b1dd95d66c248eb178db4319919c32d9304ee85b602-%E8%BF%AD%E4%BB%A3.gif)

**迭代法：**

- 递归到链表的最后一个结点，该结点就是反转后的头结点，记作 ret 
- 每次函数在返回的过程中，让当前结点的下一个结点的 next 指针指向当前节点
- 同时让当前结点的 next 指针指向 NULL ，从而实现从链表尾部开始的局部反转
- 当递归函数全部出栈后，链表反转完成

时间复杂度：O(n)

空间复杂度：O(n)

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/8951bc3b8b7eb4da2a46063c1bb96932e7a69910c0a93d973bd8aa5517e59fc8.gif)



# 代码实现

**C++：**

```
//迭代法
class Solution
{
public:
    ListNode* reverseList(ListNode* head) 
    {
        ListNode* prev = nullptr;
        ListNode* cur = head;
        while (curr) 
        {
            ListNode* next = cur->next;
            cur->next = prev;
            prev = cur;
            cur = next;
        }
        return prev;
    }
};

//递归法
class Solution 
{
public:
    ListNode* reverseList(ListNode* head) 
    {
        if (!head || !head->next) 
        {
            return head;
        }
        ListNode* ret = reverseList(head->next);
        head->next->next = head;
        head->next = nullptr;
        return ret;
    }
};
```

