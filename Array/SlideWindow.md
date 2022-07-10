# 4.滑动窗口

> 所谓**滑动窗口**，就是不断的调节子序列的起始位置和终止位置，从而得出我们想要的结果。
> 

## 例题

### ****[209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)****

给定一个含有 n 个正整数的数组和一个正整数 target 。

找出该数组中满足其和 ≥ target 的长度最小的 连续子数组 `[numsl, numsl+1, ..., numsr-1, numsr]` ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

```jsx
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。

输入：target = 4, nums = [1,4,4]
输出：1

输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
```

**题解**

```jsx
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 */
var minSubArrayLen = function(target, nums) {
    let left = 0;
    let right = 0;
    let min = nums.length + 1;
    let sum = 0;
    while (right < nums.length) {
        sum += nums[right];
        if (sum >= target) {
            while (sum - nums[left] >= target) {
                sum -= nums[left++];
            }
            min = Math.min(min, right - left + 1);
        }
        right++;
    }
    return min === nums.length + 1 ? 0 : min;
};
```
