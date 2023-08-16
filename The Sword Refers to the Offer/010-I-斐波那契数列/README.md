# [剑指 Offer 10- I. 斐波那契数列](https://leetcode.cn/problems/fei-bo-na-qi-shu-lie-lcof/)

简单



写一个函数，输入 `n` ，求斐波那契（Fibonacci）数列的第 `n` 项（即 `F(N)`）。斐波那契数列的定义如下：

```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```

斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

 

**示例 1：**

```
输入：n = 2
输出：1
```

**示例 2：**

```
输入：n = 5
输出：5
```

 

**提示：**

- `0 <= n <= 100`



# 思路

**动态规划：**

- 状态定义：`f(i)`，即第i个数字的值
- 转移方程：`f(n) =f(n-1) + f(n-2)`
- 初始状态：`f(1) = 1`，`f(2) = 2`
- 返回值：`f(n)`，即第n个数字的值
- 时间复杂度：O(n)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int fib(int n)
    {
        if(n < 2)
            return n;
        int prev = 0, cur = 0, next = 1;
        for (int i = 2; i <= n; ++i)
        {
            prev = cur;
            cur = next;
            next = (prev + cur) % 1000000007;
        }
        return next;
    }
};
```

