# 18. 4Sum
## 问题描述
Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

Note:
* Elements in a quadruplet (a,b,c,d) must be in non-descending order. (ie, a ≤ b ≤ c ≤ d)
* The solution set must not contain duplicate quadruplets.
```
    For example, given array S = {1 0 -1 0 -2 2}, and target = 0.

    A solution set is:
    (-1,  0, 0, 1)
    (-2, -1, 1, 2)
    (-2,  0, 0, 2)
```
## 分析
k-sum问题都可以通过双指针左右夹逼来解决，一般步骤是，先排序，然后外层做k-2层循环，最内层循环采用双指针左右夹逼。排序时间复杂度为O(nlgn),共有k-1层循环，所以时间复杂度为O(max{nlgn,n^k-1})。

对于k >= 4的情况，采用左右夹逼容易超时。因此可以采用预计算的方式，先缓存所有两个数组合及他们的和，在最内层循环时直接取出所有和等于target减去外面两层和的组合。

由于数组经过排序，也可以采用剪枝的方式，首先在最外面层循环中去掉太大或太小的数，再把它转为3Sum,再剪枝，再转为2Sum。

## 代码实现
**cache版**
```java
public class FourSum {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        Map<Integer, List<int[]>> cache = new HashMap<>();
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                int sum = nums[i] + nums[j];
                if (cache.containsKey(sum)) {
                    List<int[]> list = cache.get(sum);
                    list.add(new int[]{i, j});
                } else {
                    List<int[]> list = new ArrayList<>();
                    list.add(new int[]{i, j});
                    cache.put(sum, list);
                }
            }
        }
        Set<String> used = new HashSet<>();
        List<List<Integer>> result = new ArrayList<>();
        for (int i = 0; i < nums.length - 3; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            for (int j = i + 1; j < nums.length - 2; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) continue;
                int key = target - nums[i] - nums[j];
                if (!cache.containsKey(key)) {
                    continue;
                }
                for (int[] ints : cache.get(key)) {
                    if (j >= ints[0]) continue;
                    Integer[] solution = {nums[i], nums[j], nums[ints[0]], nums[ints[1]]};
                    if (!used.contains(Arrays.toString(solution))) {
                        used.add(Arrays.toString(solution));
                        List<Integer> list = new ArrayList<>(Arrays.asList(solution));

                        result.add(list);

                    }

                }
            }
        }
        return result;
    }
```
**pruning版**，效率更高
```java
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums.length == 0) return result;
        Arrays.sort(nums);
        int max = nums[nums.length - 1];
        int min = nums[0];
        //去除太大或太小
        if (4*min > target || 4*max < target) return result;
        for (int i = 0; i < nums.length -3; i++) {
            //去除太大
            if (4*nums[i]> target) return result;
            //去除重复
            if (i > 0 && nums[i] == nums[i-1]) continue;
            for (int j = i+1; j < nums.length - 2; j++) {
            //去除太大
             if ((nums[i] + 3*nums[j])> target) break;
               //去除重复
                if (j > i+1 && nums[j] == nums[j-1]) continue;
                int p = j + 1, q = nums.length - 1;
                while (p < q) {
                    int sum = nums[i] + nums[j] + nums[p] + nums[q];
                    if (sum == target) {
                        result.add(Arrays.asList(nums[i], nums[j], nums[p], nums[q]));
                        p++;
                        q--;
                        //去除重复
                        while (nums[q] == nums[q + 1] && p<q) q--;
                        while (nums[p] == nums[p-1] && p<q) p++;
                    } else if (sum > target) {
                        q--;
                        //去除重复
                        while (nums[q] == nums[q + 1] && p<q) q--;
                    } else {
                        p++;
                        //去除重复
                        while (nums[p] == nums[p-1] && p<q) p++;
                    }
                }


            }
        }
        return result;
    }
```
