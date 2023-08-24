# [剑指 Offer 13. 机器人的运动范围](https://leetcode.cn/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

中等



地上有一个m行n列的方格，从坐标 `[0,0]` 到坐标 `[m-1,n-1]` 。一个机器人从坐标 `[0, 0] `的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

 

**示例 1：**

```
输入：m = 2, n = 3, k = 1
输出：3
```

**示例 2：**

```
输入：m = 3, n = 1, k = 0
输出：1
```

**提示：**

- `1 <= n,m <= 100`
- `0 <= k <= 20`



# 思路

**广度优先搜索：**

- 建立`queue q`存储坐标信息以及数位和，建立变量`count`记录能到达的格子数

- 从开始坐标开始，每次向下向右移动（将下、右坐标入`q`），剔除`q`的头元素，标记到过的坐标，每到一个坐标判断数位和是否满足要求
- 当`q为空`时，返回`count`

- 时间复杂度：O(n*m)
- 空间复杂度：O(n*m)



# 代码实现

**C++：**

```
class Solution
{
public:
    int movingCount(int m, int n, int k)
    {
        vector<vector<bool>> vv(m, vector<bool>(n, false));
        queue<vector<int>> q;
        q.push({0, 0, 0, 0}); //坐标+数位和
        int count = 0;
        while(!q.empty())
        {
            vector<int> v = q.front();
            q.pop();
            int x = v[0], y = v[1], sx = v[2], sy = v[3];
            if(x >= m || y >= n || sx + sy > k || vv[x][y])
                continue;
            vv[x][y] = true;
            ++count;
            q.push({x + 1, y, (x + 1) % 10 != 0 ? sx + 1 : sx - 8, sy});
            q.push({x, y + 1, sx, (y + 1) % 10 != 0 ? sy + 1 : sy - 8});
        }
        return count;
    }
};
```

