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
```java
public int[] searchRange(int[] nums, int target) {
        int lo = 0;
        int hi = nums.length -1;
        while (lo < hi) {
            int mid = (lo + hi) / 2;
            if (nums[mid]< target)
                lo = mid + 1; //不停地向右移动lo,直到nums[mid] >= target
            else
                hi = mid; //向左移动hi,不加1是为了避免mid = left的情况。
        }
        int left;
        if(nums[lo] != target)
            return new int[] {-1,-1};
        else
            left = lo;
        hi = nums.length -1;
        while (lo < hi) {
            int mid = (lo + hi) / 2+1; // 避免([2,2],2)这种情况时出现死循环。
            if (nums[mid] > target) 
                hi = mid - 1;
            else 
                lo = mid;     
        }
        return new int[]{left, lo};
    }
```

## 扩展
**mid = (low + high) / 2 和 mid = low + (high - low) / 2 有何不同 ？**
前一种写法在low 和high 都比较大时会造成 low + high 大于Integer.MAX_VALUE,从而溢出。

**关于二分搜索low 和 high指针移动的问题**
1. 搜索特定值
        while (lo < hi) {
            int mid = (lo + hi) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                lo = mid + 1;
            } else {
                hi = mid -1;
            }
        }




