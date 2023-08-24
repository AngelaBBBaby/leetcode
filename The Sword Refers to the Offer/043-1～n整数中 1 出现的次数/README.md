# [剑指 Offer 43. 1～n 整数中 1 出现的次数](https://leetcode.cn/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

困难



输入一个整数 `n` ，求1～n这n个整数的十进制表示中1出现的次数。

例如，输入12，1～12这些整数中包含1 的数字有1、10、11和12，1一共出现了5次。

 

**示例 1：**

```
输入：n = 12
输出：5
```

**示例 2：**

```
输入：n = 13
输出：6
```

 

**限制：**

- `1 <= n < 2^31`



# 思路

**数学：**

- 建立变量`res`保存结果，建立变量`cur`保存当前位，`high`保存`cur`的高位，`low`保存`cur`的低位，`digit`为10的位因子

- 令`cur`从`n`的个位开始迭代到最高位
- 若`cur = 0`，出现1的次数只由`high`决定，出现次数为`high * digit`，保存到`res`
- 若`cur = 1`，出现1的次数由`high`和`low`决定，出现次数为`high * digit + low + 1`，保存到`res`
- 若`cur = 2~9`，出现1的次数只由`high`决定，出现次数为`(high + 1) * digit`，保存到`res`
- 迭代结束，返回`res`

- 时间复杂度：O(logn)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int countDigitOne(int n)
    {
        long digit = 1, res = 0;
        int high = n / 10, cur = n % 10, low = 0;
        while(cur || high)
        {
            if(cur == 0)
                res += high * digit;
            else if(cur == 1)
                res += high * digit + low + 1;
            else
                res += (high + 1) * digit;
            low += cur * digit;
            cur = high % 10;
            high /= 10;
            digit *= 10;
        }
        return res;
    }
};
```

