# Search Insert Position
## 问题描述

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Here are few examples.
[1,3,5,6], 5 → 2
[1,3,5,6], 2 → 1
[1,3,5,6], 7 → 4
[1,3,5,6], 0 → 0

## 分析
和search for a range 的解答类似，都是基于二分搜索的变形。对于这类问题，都可以在二分搜索的基础上，对于不同的情形采用不同的判断条件和不同的移动方式，从而得到适合问题的解法。

## 代码实现
```java
        if (target > nums[nums.length -1]) return nums.length;
         int lo= 0, hi = nums.length - 1;
         while (lo < hi) {
            int mid = (lo + hi) / 2 ;
            if (nums[mid] >= target) {
                hi = mid;
            } else {
                lo = mid + 1;
            }
         }
        return  lo ;

```
## 扩展
