# [剑指 Offer 11. 旋转数组的最小数字](https://leetcode.cn/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

简单



把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

给你一个可能存在 **重复** 元素值的数组 `numbers` ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的**最小元素**。例如，数组 `[3,4,5,1,2]` 为 `[1,2,3,4,5]` 的一次旋转，该数组的最小值为 1。 

注意，数组 `[a[0], a[1], a[2], ..., a[n-1]]` 旋转一次 的结果为数组 `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]` 。

 

**示例 1：**

```
输入：numbers = [3,4,5,1,2]
输出：1
```

**示例 2：**

```
输入：numbers = [2,2,2,0,1]
输出：0
```

 

**提示：**

- `n == numbers.length`
- `1 <= n <= 5000`
- `-5000 <= numbers[i] <= 5000`
- `numbers` 原来是一个升序排序的数组，并进行了 `1` 至 `n` 次旋转





# 思路

**二分查找：**

- 利用二分查找解决，只需要考虑中值的选取问题
- 若右边界的numbers值大于中值的numbers值，说明最小数在左半区域
- 若右边界的numbers值小于中值的numbers值，说明最小数在右半区域
- 若右边界的numbers值等于中值的numbers值，需要调整右边界
- 当左边界大于或等于右边界时，返回左边界的numbers值

- 时间复杂度：O(logn)

- 空间复杂度：O(1)



# 代码实现

**C++：**

```
class Solution
{
public:
    int minArray(vector<int>& numbers)
    {
        int left = 0, right = numbers.size() - 1;
        while(left < right)
        {
            int mid = (left + right) / 2;
            if(numbers[mid] < numbers[right])
                right = mid;
            else if(numbers[mid] > numbers[right])
                left = mid + 1;
            else
                --right;
        }
        return numbers[left];
    }
};
```

