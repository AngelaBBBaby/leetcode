# [21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

难度简单



将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

 

**示例 1：**

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/merge_ex1.jpg)

```
输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
```

**示例 2：**

```
输入：l1 = [], l2 = []
输出：[]
```

**示例 3：**

```
输入：l1 = [], l2 = [0]
输出：[0]
```

 

**提示：**

- 两个链表的节点数目范围是 `[0, 50]`
- `-100 <= Node.val <= 100`
- `l1` 和 `l2` 均按 **非递减顺序** 排列



# 思路

**迭代法：**

- 创建一个带头新链表list
- list1跟list2比，谁小谁就放到list->next中
- 哪个放入就迭代到下一个
- 当其中一个为空，即全部数都放进list中，另一个直接放入

**递归法：**

- 判断list1和list2哪个值更小
- 更小的递归它的下一个
- 直到其中一个为空链表



# 代码实现

**C++：**

```
//迭代法
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) 
    {
        if(list1 == nullptr)
            return list2;
        if(list2 == nullptr)
            return list1;
        
        ListNode* listhead = new ListNode(-1);
        ListNode* list = listhead;
        while(list1 != nullptr && list2 != nullptr)
        {
            if(list1->val <= list2->val)
            {
                list->next = list1;
                list1 = list1->next; 
            }
            else
            {
                list->next = list2;
                list2 = list2->next; 
            }
            list = list->next;
        }
        list->next = list1 != nullptr ? list1 : list2;
        return listhead->next;
    }
};

//递归法
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) 
    {
        if (l1 == nullptr) 
        {
            return l2;
        } 
        else if (l2 == nullptr) 
        {
            return l1;
        } 
        else if (l1->val < l2->val)
        {
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        } 
        else 
        {
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};
```

