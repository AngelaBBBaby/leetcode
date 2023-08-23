# [剑指 Offer 41. 数据流中的中位数](https://leetcode.cn/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

困难



如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

- void addNum(int num) - 从数据流中添加一个整数到数据结构中。
- double findMedian() - 返回目前所有元素的中位数。

**示例 1：**

```
输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
[[],[1],[2],[],[3],[]]
输出：[null,null,null,1.50000,null,2.00000]
```

**示例 2：**

```
输入：
["MedianFinder","addNum","findMedian","addNum","findMedian"]
[[],[2],[],[3],[]]
输出：[null,null,2.00000,null,2.50000]
```

 

**限制：**

- 最多会对 `addNum、findMedian` 进行 `50000` 次调用





# 思路

**优先队列：**

查找中位数

- 若元素个数为奇数，返回`Min.top()`
- 若元素个数为偶数，返回`(Min.top() + Max.top()) / 2.0`

- 时间复杂度：O(1)
- 空间复杂度：O(n)

添加数字

- 建立优先级队列`priority_queue<int, vector<int>, less<int>> Min`，`priority_queue<int, vector<int>, greater<int>> Max`，`Min`以大堆形式保存比中位数小的值，`Max`以小堆形式保存比中位数大的值
- 每当添加数字，若该数大于`Min.top()`（中位数），入`Max`；若该数小于`Min.top()`（中位数），入`Min`
- 每次添加完一个数字后，保证`Min中的元素个数`等于`Max中的元素个数`或`Min中的元素个数`等于`Max中的元素个数 + 1`

- 时间复杂度：O(logn)
- 空间复杂度：O(n)



# 代码实现

**C++：**

```
class MedianFinder
{
public:
    /** initialize your data structure here. */
    MedianFinder()
    {}
    
    void addNum(int num)
    {
        if(Min.empty() || num <= Min.top())
        {
            Min.push(num);
            if(Max.size() < Min.size() - 1)
            {
                Max.push(Min.top());
                Min.pop();
            }
        }
        else 
        {
            Max.push(num);
            if(Min.size() < Max.size())
            {
                Min.push(Max.top());
                Max.pop();
            }
        }
    }
    
    double findMedian()
    {
        if(Min.size() <= Max.size())
            return (Min.top() + Max.top()) / 2.0;
        else
            return (double)Min.top();
    }

    priority_queue<int, vector<int>, less<int>> Min;
    priority_queue<int, vector<int>, greater<int>> Max;
};
```

