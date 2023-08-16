# [剑指 Offer 30. 包含min函数的栈](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/)

简单



定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

 

**示例:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

 

**提示：**

1. 各函数的调用总次数不超过 20000 次



# 思路

**双栈：**

- 建立主栈和辅助栈，push一个最大值进入辅助栈中
- 调用push函数时，若该值小于辅助栈的top值，则该值入两个栈，若该值不小于辅助栈的top值，该值入主栈，辅助栈入栈它的top值，
- 调用pop函数时，两个栈都pop
- 调用min函数时，返回辅助栈的top值

- 时间复杂度：O(1)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class MinStack
{
public:
    /** initialize your data structure here. */
    MinStack()
    {
        minstack.push(INT_MAX);
    }
    
    void push(int x)
    {
        stack.push(x);
        minstack.top() > x ? minstack.push(x) : minstack.push(minstack.top());
    }
    
    void pop()
    {
        minstack.pop();
        stack.pop();
    }
    
    int top()
    {
        return stack.top();
    }
    
    int min()
    {
        return minstack.top();
    }
private:
    ::stack<int> stack;
    ::stack<int> minstack;
};
```

