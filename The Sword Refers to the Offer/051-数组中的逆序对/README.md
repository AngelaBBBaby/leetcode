# [剑指 Offer 51. 数组中的逆序对](https://leetcode.cn/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

困难



在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

 

**示例 1:**

```
输入: [7,5,6,4]
输出: 5
```

 

**限制：**

```
0 <= 数组长度 <= 50000
```



# 思路

**归并排序：**

- 建立`vector<int> v`拷贝原数组`nums`，建立归并排序函数，建立变量`sum`保存逆序对之和
- 将`nums`归并排序，`nums`将被划分成若干对左右子集
- 划分完成后，每队左右子集开始合并，令`i，j`分别为左子集的首元素和右子集的首元素

- 每当`左子集中的i元素 < 右子集中的j元素`，将`左子集中的i元素`保存到`nums`中，`++i`
- 每当`左子集中的i元素 > 右子集中的j元素`，将`右子集中的j元素`保存到`nums`中，此时左子集中`i-末尾`都与`j`形成逆序和，保存`i-末尾`的数量至`sum`中，`++j`
- 当所有子集合并完成，此时的`nums`是一个增序数组，返回`sum`

- 时间复杂度：O(n*logn)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    int reversePairs(vector<int>& nums)
    {
        vector<int> v(nums.size());
        int left = 0, right = nums.size() - 1;
        return solution(nums, v, left, right);
    }
    int solution(vector<int>& nums, vector<int>& v, int left, int right)
    {
        if(left >= right)
            return 0;
        int mid = (left + right) / 2 ;
        //划分
        int sum = solution(nums, v, left, mid) + solution(nums, v, mid + 1, right);
        //合并
        int i = left, j = mid + 1; //i，j分别指向左、右子集的首元素
        for(int tmp = left; tmp <= right; ++tmp)
        {
            v[tmp] = nums[tmp];
        }
        for(int tmp = left; tmp <= right; ++tmp)
        {
            if(i == mid + 1)
                nums[tmp] = v[j++];
            else if(j == right + 1 || v[i] <= v[j])
                nums[tmp] = v[i++];
            else
            {
                nums[tmp] = v[j++];
                sum += mid - i + 1;
            }
        }
        return sum;
    }
};
```

