# [剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode.cn/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

困难



给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

**示例:**

```
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

 

**提示：**

你可以假设 *k* 总是有效的，在输入数组 **不为空** 的情况下，`1 ≤ k ≤ nums.length`



# 思路

**单调队列+滑动窗口：**

- 建立双端队列`dq`，将`nums`的前k个数进队列形成窗口，并保证数的相对位置不变且前k个的最大值在`dq`的队头（最大值前的数丢弃），建立`vector v`保存窗口的最大值
- 遍历`nums`，移动滑动窗口，更新`dq`队头，每移动一次，将窗口中的最大值保存进`v`中
- 当遍历完，返回`v`

- 时间复杂度：O(n)
- 空间复杂度：O(k)



# 代码实现

C++：

```
class Solution
{
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k)
    {
        deque<int> dq;
        int i = 0;
        for(i = 0; i < k; ++i)
        {
            while(!dq.empty() && nums[i] >= nums[dq.back()])
                dq.pop_back();
            dq.push_back(i);
        }
        vector<int> v = {nums[dq.front()]};
        while(i < nums.size())
        {
            while(!dq.empty() && nums[i] >= nums[dq.back()])
                dq.pop_back();
            dq.push_back(i);
            while(dq.front() <= i - k)
                dq.pop_front();
            v.push_back(nums[dq.front()]);
            ++i;
        }
        return v;
    }
};
```

