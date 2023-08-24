# [剑指 Offer 66. 构建乘积数组](https://leetcode.cn/problems/gou-jian-cheng-ji-shu-zu-lcof/)

中等



给定一个数组 `A[0,1,…,n-1]`，请构建一个数组 `B[0,1,…,n-1]`，其中 `B[i]` 的值是数组 `A` 中除了下标 `i` 以外的元素的积, 即 `B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]`。不能使用除法。

 

**示例:**

```
输入: [1,2,3,4,5]
输出: [120,60,40,30,24]
```

 

**提示：**

- 所有元素乘积之和不会溢出 32 位整数
- `a.length <= 100000`



# 思路

**动态规划：**

- 状态定义：`f(i)`，即第i个数字的其他数的乘积和
- 转移方程：`f(n) = f(i) * f(j)`（`f(i)`，`f(j)`分别代表n左、右侧的乘积和）
- 初始状态：`f(0) = 1`
- 返回值： `f(n)`，即第n个数字的其他数的乘积和

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

C++：

```
class Solution
{
public:
    vector<int> constructArr(vector<int>& a)
    {
        if(a.size() == 0)
            return {};
        vector<int> v(a.size(), 1);
        v[0] = 1;
        for(int i = 1; i < a.size(); ++i)
        {
            v[i] = v[i-1] * a[i-1];
        }
        int tmp = 1;
        for(int j = a.size() - 2; j >= 0; --j)
        {
            tmp *= a[j+1];
            v[j] *= tmp;
        }
        return v;
    }
};
```

