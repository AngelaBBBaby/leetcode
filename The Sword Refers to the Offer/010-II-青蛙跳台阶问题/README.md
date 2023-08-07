# [剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode.cn/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

简单



一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 `n` 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

**示例 1：**

```
输入：n = 2
输出：2
```

**示例 2：**

```
输入：n = 7
输出：21
```

**示例 3：**

```
输入：n = 0
输出：1
```

**提示：**

- `0 <= n <= 100`



# 思路

**动态规划：**

- 状态定义： f(i)，即第i个数字的值
- 转移方程： f(n)=f(n-1)+f(n-2)
- 初始状态： f(1)=1，f(2)=2
- 返回值： f(n)，即第n个数字的值

- 时间复杂度：O(n)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int numWays(int n)
    {
        if(n <= 2)
        {
            if(n == 0)
                return 1;
            return n;
        }
        int prev = 1, cur = 1, next = 2;
        for(int i = 2; i < n; ++i)
        {
            prev = cur;
            cur = next;
            next = (cur + prev) % 1000000007;
        }
        return next;
    }
};
```

