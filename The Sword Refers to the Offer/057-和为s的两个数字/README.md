# [剑指 Offer 57. 和为s的两个数字](https://leetcode.cn/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

简单



输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

 

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
```

**示例 2：**

```
输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]
```

 

**限制：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^6`



# 思路

**双指针：**

- 建立双指针left和right分别指向nums的头和尾
- 让left所在的值与right所在的值相加，对比target的大小，若比他大，right指针向左移，若比他小，left指针向右移
- 当相等时，返回left和right所在的值；当left与right相遇，返回空
- 时间复杂度：O(n)
- 空间复杂度：O(1)

**哈希表：**

- 建立一个哈希表
- 遍历数组，在哈希表中找target-nums[i]的值，若没找到，将数组的值以<值，下标>的形式存进哈希表中
- 找到后返回迭代器->second（即下标数）和当前的数组下标
- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
//双指针
class Solution
{
public:
    vector<int> twoSum(vector<int>& nums, int target)
    {
        int left = 0;
        int right = nums.size() - 1;
        while(left < right)
        {
            if(nums[left] + nums[right] > target)
                --right;
            else if(nums[left] + nums[right] < target)
                ++left;
            else
                return {nums[left], nums[right]};  
        }
        return {};
    }
};

//哈希表
class Solution
{
public:
    vector<int> twoSum(vector<int>& nums, int target)
    {
        unordered_map<int, int> um;
        int j = 0;
        for(int i = 0; i < nums.size(); i++)
            {
                auto it = um.find(target - nums[i]);
                if(it != um.end())
                    //it->second返回第一个值的下标
                    return {it->first, nums[i]};
                //找的是值而不是下标
                //所以key为值，valu为下标，例如nums[1]->m[7] = 1
                um[nums[i]] = i;
            }
        return {};
    }
};
```

