# [剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode.cn/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

中等



请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

 

**示例 1:**

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

 

提示：

- `s.length <= 40000`



# 思路

**动态规划+哈希表：**

- 状态定义：`f(i)`，即前i个字符串中最长字串个数

- 转移方程：若`f(i - 1) < i - j`（即字符`s[i]`在`f(i - 1)`区间之外）`f(n) = f(n-1) + 1`，否则，`f(n) = i - j`（j为i的左边第一个相同字符的下标）
- 初始状态：`f(1) = 1`
- 返回值： `f(n)`，即前n个字符串中最长字串个数
- 时间复杂度：O(n)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int lengthOfLongestSubstring(string s)
    {
        if(s.size() == 0)
            return 0;
        unordered_map<char, int> um;
        int max_num = 1;
        vector<int> v(s.size(), 0);
        v[0] = 1;
        for(int i = 1; i < s.size(); ++i)
        {
            int j = i - 1;
            while(j >= 0 && s[i] != s[j])
                --j;
            if(v[i-1] < i - j)
                v[i] = v[i-1] + 1;
            else
                v[i] = i - j;
            um[s[i]] = i;
            max_num = max(v[i], max_num);
        }
        return max_num;
    }
};
```

