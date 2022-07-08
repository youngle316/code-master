# 3.移除元素

**移除元素**这类题通常是让在 **$O(1)$** 的空间复杂度下完成，也就是直接在原数组上进行修改

## 例题

### ****[27. 移除元素](https://leetcode.cn/problems/remove-element/)****

给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

```jsx
输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2]
解释：函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。
     你不需要考虑数组中超出新长度后面的元素。例如，函数返回的新长度为 2 ，
		 而 nums = [2,2,3,3] 或 nums = [2,2,0,0]，也会被视作正确答案。

输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,4,0,3]
解释：函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。
		 注意这五个元素可为任意顺序。你不需要考虑数组中超出新长度后面的元素。
```

**题解**

```jsx
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function(nums, val) {
    let i = 0;
    for (let j = 0; j < nums.length; j++) {
        if (nums[j] !== val) {
            nums[i] = nums[j];
            i++;
        }
    }
    return i;
};
```

### ****[26. 删除有序数组中的重复项](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/)****

给你一个 升序排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。

由于在某些语言中不能改变数组的长度，所以必须将结果放在数组nums的第一部分。更规范地说，如果在删除重复项之后有 k 个元素，那么 nums 的前 k 个元素应该保存最终结果。

将最终结果插入 nums 的前 k 个位置后返回 k 。

不要使用额外的空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

```jsx
输入：nums = [1,1,2]
输出：2, nums = [1,2,_]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。

输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
```

**题解**

```jsx
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    let i = 0;
    for (let j = 0; j < nums.length; j++) {
        if (nums[j] !== nums[j + 1]) {
            nums[i] = nums[j];
            i++;
        }
    }
    return i;
};
```

### ****[283. 移动零](https://leetcode.cn/problems/move-zeroes/)****

给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

**请注意** ，必须在不复制数组的情况下原地对数组进行操作。

```jsx
输入: nums = [0,1,0,3,12]
输出: [1,3,12,0,0]

输入: nums = [0]
输出: [0]
```

**题解**

```jsx
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var moveZeroes = function(nums) {
    let j = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== 0) {
            let temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
            j++;
        }
    }
};
```

### ****[884. 两句话中的不常见单词](https://leetcode.cn/problems/uncommon-words-from-two-sentences/)****

句子 是一串由空格分隔的单词。每个 单词 仅由小写字母组成。

如果某个单词在其中一个句子中恰好出现一次，在另一个句子中却 没有出现 ，那么这个单词就是 不常见的 。

给你两个 句子 s1 和 s2 ，返回所有 不常用单词 的列表。返回列表中单词可以按 任意顺序 组织。

```jsx
输入：s1 = "this apple is sweet", s2 = "this apple is sour"
输出：["sweet","sour"]

输入：s1 = "apple apple", s2 = "banana"
输出：["banana"]
```

**题解**

```jsx
/**
 * @param {string} s1
 * @param {string} s2
 * @return {string[]}
 */
var uncommonFromSentences = function(s1, s2) {
    let arr = s1.split(' ').concat(s2.split(' '));
    let result = [];
    const map = new Map();
    arr.forEach((item) => {
        if (map.has(item)) {
            let value = map.get(item)
            map.set(item, value + 1);
        } else {
            map.set(item, 0);
        }
    });
    for (const [key, value] of map) {
        if (value === 0) {
            result.push(key);
        }
    }
    return result;
};
```

### ****[844. 比较含退格的字符串](https://leetcode.cn/problems/backspace-string-compare/)****

给定 s 和 t 两个字符串，当它们分别被输入到空白的文本编辑器后，如果两者相等，返回 true 。# 代表退格字符。

注意：如果对空文本输入退格字符，文本继续为空。

```jsx
输入：s = "ab#c", t = "ad#c"
输出：true
解释：s 和 t 都会变成 "ac"。

输入：s = "ab##", t = "c#d#"
输出：true
解释：s 和 t 都会变成 ""。

输入：s = "a#c", t = "b"
输出：false
解释：s 会变成 "c"，但 t 仍然是 "b"。
```

**题解**

```jsx
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var backspaceCompare = function(s, t) {
    return fun(s) === fun(t);
};

const fun = (str) => {
    let arr = [];
    for (let i = 0; i < str.length; i++) {
        if (str[i] !== '#') {
            arr.push(str[i]);
        } else {
            arr.pop(str[i]);
        }
    }
    return arr.join('');
}
```

### ****[977. 有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/)****

给你一个按 **非递减顺序**排序的整数数组 `nums`，返回 **每个数字的平方**组成的新数组，要求也按 **非递减顺序**排序。

```jsx
输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]

输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]
```

**题解**

```jsx
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var sortedSquares = function(nums) {
    return nums.map((item) => item * item).sort((a, b) => a- b);
};
```