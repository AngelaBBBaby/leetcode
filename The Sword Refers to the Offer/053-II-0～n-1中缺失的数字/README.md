# [剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode.cn/problems/que-shi-de-shu-zi-lcof/)

简单



一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

 

**示例 1:**

```
输入: [0,1,3]
输出: 2
```

**示例 2:**

```
输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```

 

**限制：**

```
1 <= 数组长度 <= 10000
```



# 思路

**二分查找：**

- 使用二分查找解决，只需注意中值的选取问题
- 若中值位的`nums值`与中值相等，说明缺值在右半区域
- 若中值位的`nums值`与中值不相等，说明缺值在左半区域
- 当左边界和右边界相等时，返回左边界的值

- 时间复杂度：O(logn)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int missingNumber(vector<int>& nums)
    {
        int left = 0, right = nums.size() - 1;
        while(left <= right)
        {
            int mid = (left + right) / 2;
            if(nums[mid] == mid)
                left = mid + 1;
            else
                right = mid - 1;
        }
        return left;
    }
};
```

