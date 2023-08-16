# [剑指 Offer 39. 数组中出现次数超过一半的数字](https://leetcode.cn/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

简单



数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

 

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

 

**示例 1:**

```
输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
```

 

**限制：**

```
1 <= 数组长度 <= 50000
```



# 思路

**摩尔投票法：**

- 建立变量`mode`、`vote`保存众数和票数
- 遍历`nums`，每当`vote = 0`时，设`mode = nums的值`
- 当`nums的值 = mode`时，`++vote`，否则，`--vote`
- 遍历完，此时`vote > 0`，返回`mode`

- 时间复杂度：O(n)

- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int majorityElement(vector<int>& nums)
    {
        int mode = 0, vote = 0;
        for(auto it : nums)
        {
            if(vote == 0)
                mode = it;
            if(it == mode)
                ++vote;
            else
                --vote;
        }
        return mode;
    }
};
```

