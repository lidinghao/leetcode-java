# Remove Duplicates from Sorted Array
## 问题描述
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,
Given input array nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

## 分析
维护一个边界，边界左边是已经目前得到的不同的数，不断遍历，将得到的下一个不重复插入边界左边。
## 代码实现
```java
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int id = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i]!=nums[id-1]) {
                nums[id++] = nums[i];
            }
        }
        return id;

    }
```
