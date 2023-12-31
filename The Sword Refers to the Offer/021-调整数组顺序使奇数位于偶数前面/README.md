# [剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

简单



输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数在数组的前半部分，所有偶数在数组的后半部分。

 

**示例：**

```
输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
```

 

**提示：**

1. `0 <= nums.length <= 50000`
2. `0 <= nums[i] <= 10000`



# 思路

**原地交换：**

- 先从`nums`的左边开始向右遍历`nums`，找偶数
- 然后从`nums`的右边开始向左遍历`nums`，找奇数
- 交换奇数偶数位置
- 当在中间相遇，返回`nums`

- 时间复杂度：O(n)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    vector<int> exchange(vector<int>& nums)
    {
        int head = 0;
        int tail = nums.size() - 1;
        while(head < tail)
        {
            while(nums[head] % 2 != 0 && head < tail)
            {
                ++head;
            }
            while(nums[tail] % 2 == 0 && head < tail)
                --tail;
            swap(nums[head], nums[tail]);
        }
        return nums;
    }
};
```

