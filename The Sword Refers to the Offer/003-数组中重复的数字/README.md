# [剑指 Offer 03. 数组中重复的数字](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

简单



找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

**示例 1：**

```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

 

**限制：**

```
2 <= n <= 100000
```



# 思路

**哈希表：**

- 建立哈希表
- 遍历数组中的每个数字，映射到哈希表中
- 当映射值大于1，返回该值

- 时间复杂度：O(n)

- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    int findRepeatNumber(vector<int>& nums)
    {
        unordered_map<int, bool> um;
        for(auto it : nums)
        {
        	if(um[it] == true)
                return it;
            um[it] = true;
        }
        return -1;
    }
};
```

