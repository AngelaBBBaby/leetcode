# [剑指 Offer 62. 圆圈中最后剩下的数字](https://leetcode.cn/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

简单



0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。

 

**示例 1：**

```
输入: n = 5, m = 3
输出: 3
```

**示例 2：**

```
输入: n = 10, m = 17
输出: 2
```

 

**限制：**

- `1 <= n <= 10^5`
- `1 <= m <= 10^6`



# 思路

**动态规划：**

- 状态定义：`f(i)`，即`[i， m问题]`中开始的下标数
- 转移方程：`f(n) = (f(n-1) + m) % i`
- 初始状态：`f(1) = 0`
- 返回值： `f(n)`，即`[n， m问题]`中开始的下标数

- 时间复杂度：O(n)
- 空间复杂度：O(1)

![Picture2.png](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/1613584667-AQpTlK-Picture2.png)



# 代码实现

**C++：**

```
class Solution
{
public:
    int lastRemaining(int n, int m)
    {
        int x = 0;
        for(int i = 2; i <= n; i++)
        {
            x = (x + m) % i;
        }
        return x;
    }
};
```

