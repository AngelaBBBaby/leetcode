# [剑指 Offer 04. 二维数组中的查找](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

中等



在一个 n * m 的二维数组中，每一行都按照从左到右 **非递减** 的顺序排序，每一列都按照从上到下 **非递减** 的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

**示例:**

现有矩阵 matrix 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = `5`，返回 `true`。

给定 target = `20`，返回 `false`。

 

**限制：**

```
0 <= n <= 1000
0 <= m <= 1000
```



# 思路

**Z字形查找：**

- 从`matrix`的右上角开始找`target`
- 若该数比`target`大，左移
- 若该数比`target`小，下移
- 若找到`target`，返回true，若超出数组边界，返回false

- 时间复杂度：O(n+m)
- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target)
    {
        int row_size = matrix.size();
        if(row_size == 0)
            return false;
        int line_size = matrix[0].size();
        int target_row = 0;
        int target_line = line_size - 1;
        while(target_row < row_size && target_line >= 0)
        {
            if(matrix[target_row][target_line] == target)
                return true;
            else if(matrix[target_row][target_line] > target)
                --target_line;
            else if(matrix[target_row][target_line] < target)
                ++target_row;
        }
        return false;
    }
};
```

