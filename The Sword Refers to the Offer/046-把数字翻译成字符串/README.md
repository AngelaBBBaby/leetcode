# [剑指 Offer 46. 把数字翻译成字符串](https://leetcode.cn/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

中等



给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

**示例 1:**

```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

 

**提示：**

- `0 <= num < 231`



# 思路

**动态规划：**

- 状态定义：`f(i)`，即前i个数字的翻译方法
- 转移方程：若`"10" <= n-1与n-2组成的字符 <= "25"`，则`f(n) = f(n-1) + f(n-2)`，否则`f(n) = f(n-1)`
- 初始状态：`f(0) = 1`，`f(1) = 1`
- 返回值： `f(n)`，即前n个数字的翻译方法

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    int translateNum(int num)
    {
        string s = to_string(num);
        vector<int> v(s.size() + 1, 0);
        v[0] = 1;
        v[1] = 1;
        for(int i = 2; i <= s.size(); ++i)
        {
            string tmp = s.substr(i-2, 2);
            if(tmp <= "25" && tmp >= "10")
                v[i] = v[i-1] + v[i-2];
            else
                v[i] = v[i-1];
        }
        return v[s.size()];
    }
};
```

