# [剑指 Offer 50. 第一个只出现一次的字符](https://leetcode.cn/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

简单



在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

**示例 1:**

```
输入：s = "abaccdeff"
输出：'b'
```

**示例 2:**

```
输入：s = "" 
输出：' '
```

 

**限制：**

```
0 <= s 的长度 <= 50000
```



# 思路

**哈希表：**

- 建立哈希表映射`s`的字符
- 遍历`s`，若哈希表中不包含该字符，则修改哈希表中对应键值为true
- 若哈希表中包含该字符，则修改哈希表中对应键值为false
- 遍历结束，再次遍历，返回哈希表中键值为false的字符
- 时间复杂度：O(n)

- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    char firstUniqChar(string s)
    {
        unordered_map<char, bool> um;
        for(auto it : s)
            um[it] = um.find(it) == um.end();
        for(auto it : s)
        {
            if(um[it])
                return it;
        }
        return ' ';
    }
};
```

