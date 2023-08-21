# [剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode.cn/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

中等



输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

 

参考以下这颗二叉搜索树：

```
     5
    / \
   2   6
  / \
 1   3
```

**示例 1：**

```
输入: [1,6,3,2,5]
输出: false
```

**示例 2：**

```
输入: [1,3,2,6,5]
输出: true
```

 

**提示：**

1. `数组长度 <= 1000`



# 思路

**递归：**

- 建立递归函数
- 根据二叉搜索树后序遍历特性可知`postorder`最后一个元素即为根节点`root`
- 遍历`postorder`，找到第一个比根节点大的元素记为`mid_right`

- `[0, mid_right - 1]`即为左子树，所有值小于根节点；`[mid_right, root - 1]`即为右子树，所有值大于根节点
- 递归遍历左子树右子树，继续划分左右子树，判断是否满足值条件
- 若不满足值条件，返回false，若满足值条件，返回true

- 时间复杂度：O(n^2)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class Solution
{
public:
    bool verifyPostorder(vector<int>& postorder)
    {
        return solution(postorder, 0, postorder.size() - 1);
    }

    bool solution(vector<int>& postorder, int left, int right)
    {
        if(left >= right)
            return true;
        int mid_right = left;
        while(postorder[mid_right] < postorder[right])
        {
            ++mid_right;
        }
        int mid_left = mid_right;
        while(postorder[mid_left] > postorder[right])
        {
            ++mid_left;
        }
        return mid_left == right && solution(postorder, left, mid_right - 1) && solution(postorder, mid_right, right - 1);
    }
};
```

