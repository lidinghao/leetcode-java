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

