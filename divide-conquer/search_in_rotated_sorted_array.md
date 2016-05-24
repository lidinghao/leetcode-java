# Search in Rotated Sorted Array

## 问题描述
Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.


## 分析
仍然采用二分搜索的方法，由于至少有一半的元素是有序的，因此，每次将数组重新划分后，我们将low和mid比较，以此pivot是否落在左边区间，然后对两中情况分别处理。
1. 如果pivot不在左边区间，则左边是有序的，通过target >= A[low] && target < A[mid] 判断target的是否在左分区，如果是则hi= mid -1,如果不是，则lo = mid+1;
2. 如果pivot在左边区间，则右边是有序的，通过target > A[mid] && target <= A[hi] 判断target的是否在右分区，如果是则lo= mid + 1,如果不是，则hi = mid -1;
可见，该方法和二分搜索是类似的，只不过判断target是在左分区还是在右分区，需要根据pivot是否在左边做特殊处理。
## 代码实现
```java
public int search(int[] nums, int target) {
        int lo = 0, hi = nums.length -1;
        while (lo <= hi) {
            int mid = (lo + hi) / 2;
            if (target == nums[mid]) return mid;
            if (nums[lo] <= nums[mid]) {
                if (target >= nums[lo] && target < nums[mid]) {
                    hi = mid - 1;
                } else {
                    lo = mid + 1;
                }
            } else {
                if (target > nums[mid] && target <= nums[hi]) {
                    lo = mid + 1;
                } else {
                    hi = mid - 1;
                }
            }
        }
      return -1;
    }
```

