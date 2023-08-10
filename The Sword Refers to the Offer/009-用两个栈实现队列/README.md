# [剑指 Offer 09. 用两个栈实现队列](https://leetcode.cn/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

简单



用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和 `deleteHead` ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead` 操作返回 -1 )

 

**示例 1：**

```
输入：
["CQueue","appendTail","deleteHead","deleteHead","deleteHead"]
[[],[3],[],[],[]]
输出：[null,null,3,-1,-1]
```

**示例 2：**

```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

**提示：**

- `1 <= values <= 10000`
- 最多会对` appendTail、deleteHead `进行` 10000` 次调用



# 思路

**双栈：**

- 建立两个栈stack in和out，in用来入数据，out用来出数据
- appendTail通过in实现，数据直接入in栈
- deleteHead通过out实现，每当deleteHead时，若out为空则将in的全部数据依次弹出并压入out，返回out.top
- 时间复杂度：O(1)

- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class CQueue
{
public:
    CQueue()
    {}
    
    void appendTail(int value)
    {
        st_in.push(value);
    }
    
    int deleteHead()
    {
        if(st_out.empty())
        {
            while(!st_in.empty())
            {
                st_out.push(st_in.top());
                st_in.pop();
            }
        }
        if(st_out.empty())
            return -1;
        else
        {
            int val = st_out.top();
            st_out.pop();
            return val;
        }
    }
private:
    stack<int> st_in;
    stack<int> st_out;
};
```