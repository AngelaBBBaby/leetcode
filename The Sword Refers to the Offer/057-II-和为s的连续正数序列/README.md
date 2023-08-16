# [剑指 Offer 57 - II. 和为s的连续正数序列](https://leetcode.cn/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

简单



输入一个正整数 `target` ，输出所有和为 `target` 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

 

**示例 1：**

```
输入：target = 9
输出：[[2,3,4],[4,5]]
```

**示例 2：**

```
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
```

 

**限制：**

- `1 <= target <= 10^5`



# 思路

**滑动窗口：**

- 建立滑动窗口的左边界和右边界，`sum`为滑动窗口之和，建立`vector<vector<int\>> vv`记录和为`target`的连续正数序列 
- 当 `sum > target`时，向右移动左边界，更新`sum`
- 当 `sum < target`时，向右移动右边界，更新`sum`
- 当  `sum = target`时，记录此时滑动窗口的序列至`vv`中，并向右移动右边界
- 当左边界与右边界重合，返回`vv`

- 时间复杂度：O(n)
- 空间复杂度：O(1)

![Picture2.png](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/1611495306-LsrxgS-Picture2.png)



# 代码实现

**C++：**

```
class Solution
{
public:
    vector<vector<int>> findContinuousSequence(int target)
    {
        vector<vector<int>> vv;
        int left = 1, right = 2;
        int sum = left + right;
        while(left < right)
        {
            if(sum == target)
            {
                vector<int> v;
                for(int i = left; i <= right; ++i)
                    v.push_back(i);
                vv.push_back(v);
            }
            if(sum > target)
            {
                sum -= left;
                ++left;
            }
            else
            {
                ++right;
                sum += right;
            }
        }
        return vv;
    }
};
```

