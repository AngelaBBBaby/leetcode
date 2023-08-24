# [剑指 Offer 40. 最小的k个数](https://leetcode.cn/problems/zui-xiao-de-kge-shu-lcof/)

简单



输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

 

**示例 1：**

```
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```

**示例 2：**

```
输入：arr = [0,1,2,1], k = 1
输出：[0]
```

 

**限制：**

- `0 <= k <= arr.length <= 10000`
- `0 <= arr[i] <= 10000`



# 思路

**排序：**

- 使用C++库中的sort函数将`arr`进行排序
- 建立`vector v`保存`arr`前k个数
- 返回`v`

- 时间复杂度：O(n*logn)

- 空间复杂度：O(logn)

**快排：**

- 建立基准变量`key`，建立快排函数
- 以基准变量中值对`arr`进行快排
- 当`key < k`，对右半区进行快排，更改`key`值
- 当`key > k`，对左半区进行快排，更改`key`值
- 当`key = k`，返回当前arr的前`key`个数

- 时间复杂度：O(n)

- 空间复杂度：O(logn)



# 代码实现

**C++：**

```
//排序
class Solution
{
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k)
    {
        vector<int> v;
        sort(arr.begin(), arr.end());
        for(int i = 0; i < k; i++)
            v.push_back(arr[i]);
        return v;
    }
};

//快排
class Solution
{
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k)
    {
        if (k >= arr.size()) 
            return arr;
        return quickSort(arr, k, 0, arr.size()-1);
    }

    vector<int> quickSort(vector<int>& arr, int k, int left, int right)
    {
        int i = left, j = right;
        while (i < j)
        {
            while (i < j && arr[j] >= arr[left])
            {
                j--;
            }
            while (i < j && arr[i] <= arr[left])
            {
                i++;
            }
            swap(arr[i], arr[j]);
        }
        swap(arr[i], arr[left]);
        if (i > k) 
            return quickSort(arr, k, left, i - 1);
        if (i < k) 
            return quickSort(arr, k, i + 1, right);
        vector<int> res;
        res.assign(arr.begin(), arr.begin() + k);
        return res;
    }
};
```

