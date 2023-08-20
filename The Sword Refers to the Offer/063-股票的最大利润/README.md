# [剑指 Offer 63. 股票的最大利润](https://leetcode.cn/problems/gu-piao-de-zui-da-li-run-lcof/)

中等



假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

 

**示例 1:**

```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```

**示例 2:**

```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

 

**限制：**

```
0 <= 数组长度 <= 10^5
```





# 思路

**动态规划：**

- 状态定义：`f(i)`，即第i天买卖股票获得的最大利润
- 转移方程：`f(n) = max(f(n-1), prices[n] - min_num`，`min_num`是`prices[0]-prices[n-1]`中最小的值
- 初始状态：`f(1) = 0`
- 返回值： `f(n)`，即第n天买卖股票获得的最大利润

- 时间复杂度：O(n)

- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int maxProfit(vector<int>& prices)
    {
        if(prices.size() == 0)
            return 0;
        int max_gain = 0;
        int min_num = prices[0];
        for(int i = 1; i < prices.size(); ++i)
        {
            min_num = min(min_num, prices[i]);
            max_gain = max(max_gain, prices[i] - min_num);
        }
        return max_gain;
    }
};
```

