# [剑指 Offer 49. 丑数](https://leetcode.cn/problems/chou-shu-lcof/)

中等



我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

 

**示例:**

```
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```

**说明:** 

1. `1` 是丑数
2. `n` **不超过**1690



# 思路

**动态规划：**

- 状态定义：`f(i)`，即第i个数字丑数
- 转移状态：建立`vector<int> v`保存丑数，建立三个变量`a`，`b`，`c`分别表示当前丑数乘以2，3，5的值，取`a`，`b`，`c`中最小的丑数填入`v`，迭代被选中的丑数，迭代当前丑数
- 初始状态：`f(0) = 1`
- 返回值： `f(n)`，即第n个丑数
- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    int nthUglyNumber(int n)
    {
        vector<int> v(n);
        v[0] = 1;
        int a = 0, b = 0, c = 0;
        for(int i = 1; i < n; ++i)
        {
            int v_a = v[a] * 2, v_b = v[b] * 3, v_c = v[c] * 5;
            v[i] = min(min(v_a, v_b), v_c);
            if(v[i] == v_a) 
                ++a;
            if(v[i] == v_b) 
                ++b;
            if(v[i] == v_c) 
                ++c;
        }
        return v[n-1];
    }
};
```

