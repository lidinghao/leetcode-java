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


