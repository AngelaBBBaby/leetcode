# [剑指 Offer 56 - I. 数组中数字出现的次数](https://leetcode.cn/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

中等



一个整型数组 `nums` 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

 

**示例 1：**

```
输入：nums = [4,1,4,6]
输出：[1,6] 或 [6,1]
```

**示例 2：**

```
输入：nums = [1,2,10,4,1,4,3,3]
输出：[2,10] 或 [10,2]
```

 

**限制：**

- `2 <= nums.length <= 10000`





# 思路

**位运算：**

- 建立变量`a`，`b`保存目标值
- 遍历`nums`，将`nums`所有元素异或，令结果右移`m`位，找到异或结果中的第一位1
- 遍历`nums`，令所有元素与`m`位与，若结果为1，令该元素与`a`异或，若结果为0，令该元素与`b`异或
- 遍历结束，返回`a，b`

- 时间复杂度：O(n)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    vector<int> singleNumbers(vector<int>& nums)
    {
        int n = 0, m = 1, a = 0, b = 0;
        for(int num : nums)
            n ^= num;
        while((n & m) == 0)
            m <<= 1;
        for(int num : nums)
        {
            if(num & m)
                a ^= num;
            else
                b ^= num;
        }
        return {a, b};
    }
};
```

