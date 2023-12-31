# [1. 两数之和](https://leetcode.cn/problems/two-sum/)

难度简单



给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** *`target`* 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

 

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

**示例 2：**

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

**示例 3：**

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

 

**提示：**

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **只会存在一个有效答案**

 

**进阶：**你可以想出一个时间复杂度小于 `O(n2)` 的算法吗？



# 思路

**哈希表：**

- 建立一个哈希表
- 遍历数组，在哈希表中找target-nums[i]的值，若没找到，将数组的值以<值，下标>的形式存进哈希表中
- 找到后返回迭代器->second（即下标数）和当前的数组下标
- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
//哈希表
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target)
    {
        //vector<int> v;
        unordered_map<int, int> m;
        int j = 0;
        for(int i = 0; i < nums.size(); i++)
            {
                auto it = m.find(target - nums[i]);
                if(it != m.end())
                    //it->second返回第一个值的下标
                    return {it->second, i};
                //找的是值而不是下标
                //所以key为值，valu为下标，例如nums[1]->m[7] = 1
                m[nums[i]] = i;
            }
        return {};
    }
};
```

