# [剑指 Offer 58 - I. 翻转单词顺序](https://leetcode.cn/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

简单



输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

 

**示例 1：**

```
输入: "the sky is blue"
输出: "blue is sky the"
```

**示例 2：**

```
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```

**示例 3：**

```
输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

 

**说明：**

- 无空格字符构成一个单词。
- 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
- 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。



# 思路

**双指针：**

- 先将`s`整个翻转
- 从头遍历`s`，建立双指针找完整的单词，将单词翻转
- 遍历完成后处理多余的空格
- 返回`s`

- 时间复杂度：O(n)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    string reverseWords(string s)
    {
        //整体翻转
        reverse(s.begin(), s.end());
        
        int len = s.size();
        int idx = 0;
        for(int start = 0; start < len; ++start)
        {
            if (s[start] != ' ')
            {
                //填一个空白字符然后将idx移动到下一个单词的开头位置
                if (idx != 0)
                    s[idx++] = ' ';

                //找单词
                int end = start;
                while(end < len && s[end] != ' ')
                {
                    s[idx++] = s[end++];
                }
                //单词翻转
                reverse(s.begin() + idx - (end - start), s.begin() + idx);

                //找下一个单词
                start = end;
            }
        }
        s.erase(s.begin() + idx, s.end());
        return s;
    }
};
```

