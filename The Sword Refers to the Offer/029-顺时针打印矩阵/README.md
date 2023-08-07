# [剑指 Offer 29. 顺时针打印矩阵](https://leetcode.cn/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

简单



输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

 

**示例 1：**

```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```

**示例 2：**

```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

 

**限制：**

- `0 <= matrix.length <= 100`
- `0 <= matrix[i].length <= 100`



# 思路

**设定边界法：**

- 建立vector v，求出矩阵大小，并建立矩阵的边界变量，建立变量k记录已遍历的数量
- 往右遍历矩阵，到右边界时停止，将值push_back入v中，上边界+1
- 往下遍历矩阵，到下边界时停止，将值push_back入v中，右边界-1
- 往左遍历矩阵，到左边界时停止，将值push_back入v中，下边界-1
- 往上遍历矩阵，到上边界时停止，将值push_back入v中，左边界+1
- 当k=矩阵大小，返回v

- 时间复杂度：O(n)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix)
    {
        vector<int> v;
        if(matrix.size() == 0 || matrix[0].size() == 0)
            return v;
        int length = matrix[0].size();
        int width = matrix.size();
        int size = length * width;
        int k = 0;
        //定义边界
        int up = 0, down = width-1, right = length-1, left = 0;
        int line = 0, row = 0;
        while(k < size)
        {
            //右
            for(line = left; line <= right && k < size; ++line)
            {
                v.push_back(matrix[up][line]);
                ++k;
            }
            ++up;

            //下
            for(row = up; row <= down && k < size; ++row)
            {
                v.push_back(matrix[row][right]);
                ++k;
            }
            --right;

            //左
            for(line = right; line >= left && k < size; --line)
            {
                v.push_back(matrix[down][line]);
                ++k;
            }
            --down;

            //上
            for(row = down; row >= up && k < size; --row)
            {
                v.push_back(matrix[row][left]);
                ++k;
            }
            ++left;
        }
        return v;
    }
};
```

