# [剑指 Offer 47. 礼物的最大价值](https://leetcode.cn/problems/li-wu-de-zui-da-jie-zhi-lcof/)

中等



在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

 

**示例 1:**

```
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```

 

提示：

- `0 < grid.length <= 200`
- `0 < grid[0].length <= 200`



# 思路

**动态规划：**

- 建立`vector<vector<int>> vv`保存到该元素的最大价值（比原数组多开辟一行一列）
- 状态定义：`f[i][j]`，即第i行j列的礼物的最大价值
- 转移方程：`f[m][n] = max(f[m-1][n] + grid[m-1][n-1], f[m][n-1] + grid[m-1][n-1])`
- 初始状态：`f[0][j] = 0  `，`f[i][0] = 0`（多出来的一行一列都为0）
- 返回值： `f[m-1][n-1]`，即第n行n列的礼物的最大价值（最后一个元素的最大价值）

- 时间复杂度：O(n*m)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    int maxValue(vector<vector<int>>& grid)
    {
        int row = grid.size() + 1, col = grid[0].size() + 1;
        vector<vector<int>> vv(row, vector<int>(col, 0));
        for(int i = 1; i < row; ++i)
        {
            for(int j = 1; j < col; ++j)
            {
                vv[i][j] = max(vv[i-1][j] + grid[i-1][j-1], vv[i][j-1] + grid[i-1][j-1]);
            }
        }
        return vv[row-1][col-1];
    }
};
```

