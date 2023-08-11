# [剑指 Offer 42. 连续子数组的最大和](https://leetcode.cn/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

简单



输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

 

**示例1:**

```
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

 

**提示：**

- `1 <= arr.length <= 10^5`
- `-100 <= arr[i] <= 100`



# 思路

**动态规划：**

- 状态定义： f(i)，即以第 i 个数结尾的连续子数组的最大和
- 转移方程： f(n)=max(f(n-1)+nums[n]，nums[n])
- 初始状态： f(1)=nums[i]
- 返回值： f(n)，即以最后一个数结尾的连续子数组的最大和

- 时间复杂度：O(logn)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int maxSubArray(vector<int>& nums)
    {
        int pre = 0, max_sum = nums[0];
        for(const auto& it : nums)
        {
            pre = max(pre + it, it);
            max_sum = max(pre, max_sum);
        }
        return max_sum;
    }
};
```

