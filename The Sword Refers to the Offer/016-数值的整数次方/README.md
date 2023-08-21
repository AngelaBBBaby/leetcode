# [剑指 Offer 16. 数值的整数次方](https://leetcode.cn/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

中等



实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 x 的 n 次幂函数（即，xn）。不得使用库函数，同时不需要考虑大数问题。

 

**示例 1：**

```
输入：x = 2.00000, n = 10
输出：1024.00000
```

**示例 2：**

```
输入：x = 2.10000, n = 3
输出：9.26100
```

**示例 3：**

```
输入：x = 2.00000, n = -2
输出：0.25000
解释：2-2 = 1/22 = 1/4 = 0.25
```

 

**提示：**

- `-100.0 < x < 100.0`
- `-231 <= n <= 231-1`
- `n` 是一个整数
- 要么 `x` 不为零，要么 `n > 0` 。
- `-104 <= xn <= 104`



# 思路

**快速幂：**

- 建立`sum`保存结果
- 当幂次数`n`为偶数，`x * = x`
- 当幂次数`n`为奇数，`sum * = x`
- 迭代`n `，令`n /= 2`，重复上述判断
- 当`n = 0`，若最初的`n`为正数，返回`sum`，若最初的`n`为负数，返回`1 / sum`

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

![Picture2.png](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/379a042b9d8df3a96d1ac0f27346718033bf3bfce69731bab52bf6f372b4c8f4-Picture2.png)



# 代码实现

**C++：**

```
class Solution
{
public:
    double myPow(double x, int n)
    {
        long long N = n;
        return N >= 0 ? _myPow(x, N) : 1 / _myPow(x, -N);
    }

    double _myPow(double x, long long N)
    {
        double sum = 1.0;
        while(N > 0)
        {
            if(N % 2 == 1)
            {
                sum *= x;
            }
            x *= x;
            N /= 2;
        }
        return sum;
    }
};
```

