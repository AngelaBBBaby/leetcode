# [剑指 Offer 05. 替换空格](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

难度简单



请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

 

**示例 1：**

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

 

**限制：**

```
0 <= s 的长度 <= 10000
```



# 思路

**字符串修改：**

- 需要考虑增容问题，所以直接新建一个`string arr`，不然需要在原string开辟新空间
- 遍历`s`，当不是空格时，直接push_back进`arr`中，当是空格时，分别push_back `%`，`2`，`0`进`arr`中
- 遍历完成，返回arr
- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution {
public:
    string replaceSpace(string s) 
    {
        string arr;
        for(auto& e : s)
        {
            if(e == ' ')
            {
                arr.push_back('%');
                arr.push_back('2');
                arr.push_back('0');
            }
            else
            {
                arr.push_back(e);
            }
        }
        return arr;
    }
};
```

