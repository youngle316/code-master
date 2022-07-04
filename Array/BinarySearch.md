# 2. 二分查找

## 定义

二分查找就是取数组的中间值，判断中间值和目标值的大小，再从一分为二的数组中满足条件的一半再次去中间值进行判断。
此方法的前提是 数组是**有序的**，同时不包含**重复元素**。

## 写法

- `while (left <= right)` 要使用 `<=` ，因为 `left === right` 是有意义的，所以使用  `≤`
- `if (nums[middle] > target) right` 要赋值为 `middle - 1`，因为当前这个 `nums[middle]`一定不是 `target`，那么接下来要查找的左区间结束下标位置就是 `middle - 1`

## 例题

### ****[704. 二分查找](https://leetcode.cn/problems/binary-search/)****

给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

```bash
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4

输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```

**题解**

```jsx
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    let left = 0;
    let right = nums.length - 1;
    while(left <= right) {
        let mid = left + Math.floor((right - left) / 2);
        if(nums[mid] > target) {
            right = mid - 1;
        } else if(nums[mid] < target) {
            left = mid + 1;
        } else {
            return mid;
        }
    }
    return -1;
};
```

### ****[35. 搜索插入位置](https://leetcode.cn/problems/search-insert-position/)****

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 `O(log n)` 的算法。

```bash
输入: nums = [1,3,5,6], target = 5
输出: 2

输入: nums = [1,3,5,6], target = 2
输出: 1

输入: nums = [1,3,5,6], target = 7
输出: 4
```

**题解**

```jsx
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
    let left = 0;
    let right = nums.length - 1;
    while(left <= right) {
        let mid = left + Math.floor((right - left) / 2);
        if(nums[mid] > target) {
            right = mid - 1;
        } else if(nums[mid] < target) {
            left = mid + 1
        } else {
            return mid;
        }
    }
    return right + 1;
};
```

### ****[34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)****

给你一个按照非递减顺序排列的整数数组 nums，和一个目标值 target。请你找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 target，返回 [-1, -1]。

你必须设计并实现时间复杂度为 O(log n) 的算法解决此问题。

```jsx
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]

输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]

输入：nums = [], target = 0
输出：[-1,-1]
```

**题解**

```jsx
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function(nums, target) {
    const mid = getMid(nums, target);
    if(mid === -1) {
        return [-1, -1];
    }
    let left = mid;
    let right = mid;
    while(left - 1 >= 0 && nums[left - 1] === target) {
        left -= 1;
    }
    while(right + 1 <= nums.length - 1 && nums[right + 1] === target) {
        right += 1;
    }
    return [left, right];
};

const getMid = (nums, target) => {
    let left = 0;
    let right = nums.length - 1;
    while(left <= right) {
        let mid = left + Math.floor((right - left) / 2);
        if(nums[mid] < target) {
            left = mid + 1;
        } else if(nums[mid] > target) {
            right = mid - 1;
        } else {
            return mid;
        }
    }
    return -1;
}
```

### ****[69. x 的平方根](https://leetcode.cn/problems/sqrtx/)****

给你一个非负整数 x ，计算并返回 x 的 算术平方根 。

由于返回类型是整数，结果只保留 整数部分 ，小数部分将被 舍去 。

注意：不允许使用任何内置指数函数和算符，例如 pow(x, 0.5) 或者 x ** 0.5 。

```jsx
输入：x = 4
输出：2

输入：x = 8
输出：2
解释：8 的算术平方根是 2.82842..., 由于返回类型是整数，小数部分将被舍去。
```

**题解**

```jsx
/**
 * @param {number} x
 * @return {number}
 */
var mySqrt = function(x) {
    let left = 0;
    let right = x;
    while(left <= right) {
        let mid = left + Math.floor((right - left) / 2);
        if (mid * mid <= x) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return right;
};
```

****[367. 有效的完全平方数](https://leetcode.cn/problems/valid-perfect-square/)****

给定一个 正整数 num ，编写一个函数，如果 num 是一个完全平方数，则返回 true ，否则返回 false 。

进阶：不要 使用任何内置的库函数，如  sqrt 。

```jsx
输入：num = 16
输出：true

输入：num = 14
输出：false
```

**题解**

```jsx
/**
 * @param {number} num
 * @return {boolean}
 */
var isPerfectSquare = function(num) {
    let left = 1;
    let right = num;
    while(left <= right) {
        let mid = left + Math.floor((right-left) / 2);
        if(mid * mid > num) {
             right = mid - 1;
        } else if(mid * mid < num) {
            left = mid + 1;
        } else {
           return true;
        }
    }
    return false;
};
```