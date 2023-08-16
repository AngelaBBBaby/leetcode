# [剑指 Offer 06. 从尾到头打印链表](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

难度简单



输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

**示例 1：**

```
输入：head = [1,3,2]
输出：[2,3,1]
```

 

**限制：**

```
0 <= 链表长度 <= 10000
```

通过次数636,690

提交次数856,122



# 思路

**逆序数组：**

- 建立一个`vector arr`
- 遍历链表，将链表中的值放到`arr`中
- 将`arr`逆置，完成后返回`arr`

- 时间复杂度：O(n)
- 空间复杂度：O(n)

**栈实现：**

- 建立一个vector arr和一个stack st
- 遍历链表，将链表中的值入栈 
- 遍历stack，将stack的值放进arr后出栈
- 遍历完成，返回arr

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
//逆序数组
class Solution
{
public:
    vector<int> reversePrint(ListNode* head)
    {
        vector<int> arr;
        while(head)
        {
            arr.push_back(head->val);
            head = head->next;
        }
        int i = 0;
        int len = arr.size();
        int j = len - 1;
        while(i < j)
        {
            swap(arr[i], arr[j]);
            ++i;
            --j;
        }
        return arr;
    }
};

//栈实现
class Solution {
public:
    vector<int> reversePrint(ListNode* head)
    {
        vector<int> arr;
        stack<int> st;
        while(head)
        {
            st.push(head->val);
            head = head->next;
        }
        while(!st.empty())
        {
            arr.push_back(st.top());
            st.pop();
        }
        return arr;
    }
};
```

