# [剑指 Offer 12. 矩阵中的路径](https://leetcode.cn/problems/ju-zhen-zhong-de-lu-jing-lcof/)

中等



给定一个 `m x n` 二维字符网格 `board` 和一个字符串单词 `word` 。如果 `word` 存在于网格中，返回 `true` ；否则，返回 `false` 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 

例如，在下面的 3×4 的矩阵中包含单词 "ABCCED"（单词中的字母已标出）。

![img](https://angela-typora.oss-cn-guangzhou.aliyuncs.com/typora/word2.jpg)

 

**示例 1：**

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```

**示例 2：**

```
输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false
```

 

**提示：**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board `和` word `仅由大小写英文字母组成



# 思路

**深度优先搜索：**

- 建立DFS，每当访问一个点，将其标记，返回后取消标记
- 遍历`board`，找到与`word`首元素相同的元素
- 开始DFS搜索该元素的上下左右元素是否有一条路径能找到`word`字符串
- 若有，则返回true，否则，返回false

- 时间复杂度：O(n*m)
- 空间复杂度：O(n*m)



# 代码实现

**C++：**

```
class Solution
{
public:
    bool DFS(vector<vector<char>>& board, string word, int i, int j, int row, int col, int size)
    {
        if(i < 0 || i >= row || j < 0 || j >= col || board[i][j] != word[size])
            return false;
        if(size == word.size() - 1)
            return true;
        board[i][j] = '\0'; //标记已使用的元素
        bool res = DFS(board, word, i-1, j, row, col, size+1) || DFS(board, word, i+1, j, row, col, size+1) ||
                   DFS(board, word, i, j-1, row, col, size+1) || DFS(board, word, i, j+1, row, col, size+1);
        board[i][j] = word[size]; //取消标记已使用的元素
        return res;
    }

    bool exist(vector<vector<char>>& board, string word)
    {
        int row = board.size(), col = board[0].size();
        for(int i = 0; i < row; ++i)
        {
            for(int j = 0; j < col; ++j)
            {
                if(DFS(board, word, i, j, row, col, 0))
                    return true;
            }
        }
        return false;
    }
};
```

