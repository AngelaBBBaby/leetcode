# [剑指 Offer 25. 合并两个排序的链表](https://leetcode.cn/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

简单



输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

**示例1：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

**限制：**

```
0 <= 链表长度 <= 1000
```



# 思路

**迭代：**

- 建立新链表`l3`，存储合并后的数据，并用`head`保存`l3`的头结点
- 遍历`l1`和`l2`，比较大小，谁小谁保存到`l3`后迭代
- 当`l1`或`l2`为空时，不为空的直接保存到`l3`
- 返回`head->next`

- 时间复杂度：O(n+m)
- 空间复杂度：O(1)

**递归：**

- 建立递归函数，将l1和l2作为实参进行递归
- 比较l1和l2的val，谁小将谁的->next继续递归
- 当l1或者l2为空时，返回不为空的链表，递归结束

- 时间复杂度：O(n+m)
- 空间复杂度：O(n+m)



# 代码实现

**C++：**

```
//迭代
class Solution
{
public: 
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2)
    {
        if(l1 == nullptr && l2 == nullptr)
            return nullptr;
        if(l1 == nullptr)
            return l2;
        if(l2 == nullptr)
            return l1;
        ListNode* l3 = new ListNode;
        ListNode* head = l3;
        while(l1 && l2)
        {
            if(l1->val <= l2->val)
            {
                l3->next = l1;
                l1 = l1->next;
            }
            else
            {
                l3->next = l2;
                l2 = l2->next;
            }      
            l3 = l3->next;
        }
        l3->next = l1 == nullptr ? l2 : l1;
        return head->next;
    }   
};

//递归
class Solution
{
public: 
    ListNode* _mergeTwoLists(ListNode* l1, ListNode* l2)
    {
        if(l1 == nullptr && l2 == nullptr)
            return nullptr;
        if(l1 == nullptr)
            return l2;
        else if(l2 == nullptr)
            return l1;
        else if(l1->val < l2->val)
        {
            l1->next = _mergeTwoLists(l1->next, l2);
            return l1;
        }
        else
        {
            l2->next = _mergeTwoLists(l1 , l2->next);
            return l2;
        }
    }
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2)
    {
        ListNode* l3 = _mergeTwoLists(l1, l2);
        return l3;
    }   
};
```

