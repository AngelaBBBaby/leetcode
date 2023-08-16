# [剑指 Offer 61. 扑克牌中的顺子](https://leetcode.cn/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

简单



从**若干副扑克牌**中随机抽 `5` 张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

 

**示例 1:**

```
输入: [1,2,3,4,5]
输出: True
```

 

**示例 2:**

```
输入: [0,0,1,2,5]
输出: True
```

 

**限制：**

数组长度为 5 

数组的数取值为 [0, 13] 



# 思路

**哈希+最值：**

- 建立哈希表判断是有重复值，若有重复值返回false
- 遍历`nums`，建立`max_num`，`min_num`变量保存`nums`中的最大值最小值
- 遍历完成，若`max_num-min_num < 5`，返回true，否则返回false

- 时间复杂度：O(n)

- 空间复杂度：O(n)



# 代码实现

C++：

```
class Solution
{
public:
    bool isStraight(vector<int>& nums)
    {
        int hash[14] = {0};
        int max_num = 0, min_num = 13;
        for(auto it : nums)
        {
            if(it == 0)
                continue;
            hash[it]++;
            if(hash[it] > 1)
                return false;
            max_num = max(max_num, it);
            min_num = min(min_num, it);
        }
        return max_num - min_num < 5;
    }
};
```

