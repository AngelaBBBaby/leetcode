# [剑指 Offer 44. 数字序列中某一位的数字](https://leetcode.cn/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

中等



数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

 

**示例 1：**

```
输入：n = 3
输出：3
```

**示例 2：**

```
输入：n = 11
输出：0
```

 

**限制：**

- `0 <= n < 2^31`



# 思路

**数学：**

- 确认`n`所在数字的位数：建立变量`digit`表示位数，`start`表示每`digit`位数的起始数字，`count`表示位数数量，`count = 9 * digit * start`
- 确定`n`所在的数字`num`：`num = start + (n - 1) / digit`
- 确定`n`是`num`中的哪一位数`res`：`res = (to_string(num))[(n - 1) % digit] - '0'`
- 返回`res`

- 时间复杂度：O(logn)
- 空间复杂度：O(logn)



# 代码实现

**C++：**

```
class Solution
{
public:
    int findNthDigit(int n)
    {
        long digit = 1, start = 1, count = 9;
        while(n > count)
        {
            n -= count;
            ++digit;
            start *= 10;
            count = 9 * digit * start;
        }
        long num = start + (n - 1) / digit;
        return (to_string(num))[(n - 1) % digit] - '0'
    }
};
```

