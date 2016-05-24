# Search for a Range
## 问题描述
Given a sorted array of integers, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

For example,
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].
## 分析
对数组做两次二分搜索，分别找出上界和下界。
## 代码实现

