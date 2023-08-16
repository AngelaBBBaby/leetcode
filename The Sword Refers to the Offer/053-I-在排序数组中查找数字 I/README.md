# [剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

简单



统计一个数字在排序数组中出现的次数。

 

**示例 1:**

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
```

**示例 2:**

```
输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
```

 

**提示：**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- `nums` 是一个非递减数组
- `-109 <= target <= 109`



# 思路

**二分查找：**

- 在二分查找中加入`bool lower`以方便复用

- 先通过二分查找找到跟`target`相等的值的左范围`left`
- 后通过二分查找找到跟`target`相等的值的右范围`right`
- 返回`right - left + 1`

- 时间复杂度：O(logn)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int binarySearch(vector<int>& nums, int target, bool lower)
    {
        int size = nums.size();
        int left = 0, right = size - 1;
        while(left <= right)
        {
            int mid = (left+right) / 2;
            if(nums[mid] > target || (lower && nums[mid] >= target))
            {
                right = mid - 1;
                size = mid;
            }
            else
                left = mid + 1;
        }
        return size;
    }

    int search(vector<int>& nums, int target)
    {
        if(nums.size() == 0)
            return 0;
        int left = binarySearch(nums, target, true);
        int right = binarySearch(nums, target, false) - 1;
        return right - left + 1;
    }
};
```

