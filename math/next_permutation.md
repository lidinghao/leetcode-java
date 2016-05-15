# Next Permutation
## 分析
主要是分析并发现数字中的规律。
![pic](https://www.nayuki.io/res/next-lexicographical-permutation-algorithm/next-permutation-algorithm.png)
## 代码实现
```java
    public void nextPermutation(int[] nums) {
        if (nums==null || nums.length <= 1) return;
        int i = nums.length -2;
        while (i >= 0 && nums[i] >= nums[i+1]) i--;
        if (i >= 0) {
        int j = nums.length -1;
            while (nums[j] <= nums[i]) j--;
            swap(nums, i, j);

        }
        reverse(nums, i+1, nums.length -1);
    }

    private void reverse(int[] nums, int i, int j) {
        while (i < j) {
            swap(nums, i,j);
            i++;
            j--;
        }
    }

    private void swap(int[] nums, int i, int j) {
        nums[i] ^= nums[j];
        nums[j] ^= nums[i];
        nums[i] ^= nums[j];
    }
```
