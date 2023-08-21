# [剑指 Offer 38. 字符串的排列](https://leetcode.cn/problems/zi-fu-chuan-de-pai-lie-lcof/)

中等



输入一个字符串，打印出该字符串中字符的所有排列。

 

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

 

**示例:**

```
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
```

 

**限制：**

```
1 <= s 的长度 <= 8
```



# 思路

**回溯：**

- 建立`vector<bool> vb`标记字符的使用情况，建立`string str`保存目标字符串，建立`vector<string> vs`保存结果，建立遍历`i`表示空位
- 每有一个空位，遍历一次`s`
- 每经过一个字符，标记该字符为已使用（true），若当前的字符已使用，迭代到下一个字符，若未使用，则占用一个空位
- 当`i = s.size()`，说明有一个可行解，保存进`vs`中
- 遍历结束，返回vs

- 时间复杂度：O(n×n!)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    vector<string> permutation(string s)
    {
        string str;
        int size = s.size();
        vb.resize(size, false);
        sort(s.begin(), s.end());
        DFS(s, str, 0, size);
        return vs;
    }

    void DFS(string s, string& str, int i, int size)
    {
        if(i == size)
        {
            vs.push_back(str);
            return;
        }
        for(int j = 0; j < size; ++j)
        {
            if(vb[j] || (j > 0 && !vb[j-1] && s[j] == s[j-1]))
                continue;
            str.push_back(s[j]);
            vb[j] = true;
            DFS(s, str, i + 1, size);
            str.pop_back();
            vb[j] = false;
        }
        
    }

    vector<bool> vb;
    vector<string> vs;
}; 
```

