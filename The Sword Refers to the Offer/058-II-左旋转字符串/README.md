# [剑指 Offer 58 - II. 左旋转字符串](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

难度简单



字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

 

**示例 1：**

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

**示例 2：**

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

 

**限制：**

- `1 <= k < s.length <= 10000`



# 思路

**双指针：**

- 拷贝`s`到新的`string str`上，`len`为`s`的size大小，`i`为`s`的下标，`n`为需要旋转的前n个字符
- 遍历`s`，将`n`前面的字符放到`str`的`i + len - n`的位置上，将`n`前面的字符放到`str`的`(i+len-n) % len`的位置上
- 遍历完成，返回`str`
- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    string reverseLeftWords(string s, int n)
    {
        string str = s;
        int len = s.size();
        for(int i = 0; i < len; i++)
        {
            //i+len-n就是n前面的数的位置
            //(i+len-n)%len就是n后面的数的位置
            str[(i+len-n) % len] = s[i];
        }
        return str;
    }
};
```

