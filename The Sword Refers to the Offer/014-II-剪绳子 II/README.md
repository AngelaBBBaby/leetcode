# [剑指 Offer 14- II. 剪绳子 II](https://leetcode.cn/problems/jian-sheng-zi-ii-lcof/)

中等



给你一根长度为 `n` 的绳子，请把绳子剪成整数长度的 `m` 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m - 1]` 。请问 `k[0]*k[1]*...*k[m - 1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

 

**示例 1：**

```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

**示例 2:**

```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

 

**提示：**

- `2 <= n <= 1000`



# 思路

**数学+快速幂：**

- 与[剑指 Offer 14- I. 剪绳子](https://leetcode.cn/problems/jian-sheng-zi-lcof/)主体相等，需要处理大数越界情况下的求余问题
- 使用快速幂解决大数求余问题（参考[剑指 Offer 16. 数值的整数次方](https://leetcode.cn/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)）

- 时间复杂度：O(logn)
- 空间复杂度：O(1)



# 代码实现

C++：

```
class Solution
{
public:
    int cuttingRope(int n)
    {
        if(n <= 3)
        return n - 1;
        int a = n / 3 - 1, p = 1000000007;
        long sum = 1, x = 3;
        for(; a > 0; a /= 2)
        {
            if(a % 2)
                sum = (sum * x) % p;
            x = (x * x) % p;
        }
        if(n % 3 == 0)
            return (int)(sum * 3 % p);
        if(n % 3 == 1)
            return (int)(sum * 4 % p);
        return (int)(sum * 6 % p);
    }
};
```

