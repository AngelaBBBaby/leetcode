# [剑指 Offer 45. 把数组排成最小的数](https://leetcode.cn/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

中等



输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

 

**示例 1:**

```
输入: [10,2]
输出: "102"
```

**示例 2:**

```
输入: [3,30,34,5,9]
输出: "3033459"
```

 

**提示:**

- `0 < nums.length <= 100`

**说明:**

- 输出结果可能非常大，所以你需要返回一个字符串而不是整数
- 拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0



# 思路

**变种快排：**

- 建立`vector<string> v`，建立`string s`保存结果
- 建立变种快排函数，若拼接字符串`x + y > y + x`，则`x`应该在`y`右边；若拼接字符串`x + y < y + x`，则`x`应该在`y`左边
- 将`nums`中的元素转换成字符保存到`v`中
- 对`v`中的元素快排
- 排序结束，将`v`中的元素保存到`s`，返回s

- 时间复杂度：O(n*logn)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    string minNumber(vector<int>& nums)
    {
        vector<string> v;
        for(int n = 0; n < nums.size(); ++n)
           v.push_back(to_string(nums[n]));
        quick_sort(v, 0, v.size() - 1);
        string s;
        for(auto it : v)
            s += it;
        return s;
    }

    void quick_sort(vector<string>& v, int left, int right)
    {
        if(left >= right)
            return;
        int i = left, j = right;
        while(i < j)
        {
            while(i < j && v[i] + v[j] <= v[j] + v[i])
                ++i;
            while(i < j && v[j] + v[i] >= v[i] + v[j])
                j--;
            swap(v[i], v[j]);
        }
        swap(v[i], v[right]);
        quick_sort(v, left, i - 1);
        quick_sort(v, i + 1, right);
    }
};
```

