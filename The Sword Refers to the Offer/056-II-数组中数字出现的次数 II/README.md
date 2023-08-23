# [剑指 Offer 56 - II. 数组中数字出现的次数 II](https://leetcode.cn/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

中等



在一个数组 `nums` 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

 

**示例 1：**

```
输入：nums = [3,4,3,3]
输出：4
```

**示例 2：**

```
输入：nums = [9,1,7,9,7,9,7]
输出：1
```

 

**限制：**

- `1 <= nums.length <= 10000`
- `1 <= nums[i] < 2^31`



# 思路

**位运算：**

- 建立变量`target`保存目标值，建立`vector<int> v`保存所有位的1的个数
- 遍历`nums`，将`nums`所有元素的每一位1保存到`v`对应的位置中
- 遍历`v`，所有与3取模不为0的位即为`target`的1位
- 遍历结束，返回`target`
- 时间复杂度：O(n)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int singleNumber(vector<int>& nums)
    {
        vector<int> v(32);
        for(int num : nums)
        {
            for(int i = 0; i < 32; ++i)
            {
                v[i] += num & 1;
                num >>= 1;
            }
        }
        int target = 0;
        for(int i = 0; i < 32; ++i)
        {
            target <<= 1;
            target |= v[31 - i] % 3;
        }
        return target;
    }
};
```

