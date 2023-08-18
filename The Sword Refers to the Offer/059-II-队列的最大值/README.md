# [剑指 Offer 59 - II. 队列的最大值](https://leetcode.cn/problems/dui-lie-de-zui-da-zhi-lcof/)

中等



请定义一个队列并实现函数 `max_value` 得到队列里的最大值，要求函数`max_value`、`push_back` 和 `pop_front` 的**均摊**时间复杂度都是O(1)。

若队列为空，`pop_front` 和 `max_value` 需要返回 -1

**示例 1：**

```
输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
```

**示例 2：**

```
输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
```

 

**限制：**

- `1 <= push_back,pop_front,max_value的总操作数 <= 10000`
- `1 <= value <= 10^5`



# 思路

**双端队列：**

- 建立双端队列`dq`保存队列中的最大值

- `push_back`时，将dq中比该数据小的数全部剔除，保证`dq`中的数据按递减排列
- `pop_front`时，若该数据是`dq`的队头，则删除该队头
- `max_value`时，若`dq不为空`，返回队头数据，否则返回`-1`

- 时间复杂度：O(1)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class MaxQueue
{
    deque<int> dq;
    queue<int> q;
public:
    MaxQueue()
    {}
    
    int max_value()
    {
        return dq.empty() ? -1 : dq.front();
    }
    
    void push_back(int value)
    {
        q.push(value);
        while(!dq.empty() && value > dq.back())
            dq.pop_back();
        dq.push_back(value);

    }
    
    int pop_front()
    {
        if(q.empty())
            return -1;
        int front = q.front();
        if(front == dq.front())
            dq.pop_front();
        q.pop();
        return front;
    }
};
```

