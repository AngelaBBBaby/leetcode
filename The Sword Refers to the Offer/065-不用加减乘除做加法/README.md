# [剑指 Offer 65. 不用加减乘除做加法](https://leetcode.cn/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

简单



写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

 

**示例:**

```
输入: a = 1, b = 1
输出: 2
```

 

**提示：**

- `a`, `b` 均可能是负数或 0
- 结果不会溢出 32 位整数



# 思路

**位运算：**

- `a`和`b`的进位和为`a & b << 1`
- `a`和`b`的非进位和为`a ^= b`
- 令`b`迭代为进位和
- 当`b`不为0时，返回`a`

- 时间复杂度：O(1)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int add(int a, int b)
    {
        while(b != 0)
        {
            int carry = (a & b) << 1; //进位
            a ^= b; //非进位和
            b = carry;
        }
        return a;
    }
};
```

