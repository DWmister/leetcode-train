19、[多数元素](https://leetcode-cn.com/problems/majority-element/)

给定一个大小为`n`的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于`⌊ n/2 ⌋`的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

**示例1:**

```
输入: [3,2,3]
输出: 3
```

**示例2:**

```
输入: [2,2,1,1,1,2,2]
输出: 2
```
**解题:**

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    /**
     * 方法一： 直接排序获取众数
     * 由题意可知：数组非空，众数一定存在，且数量大于数组长度的一半。
     * 那么：数组排序后的中位数一定为众数
     */
    // nums.sort((a, b) => a - b)
    // return nums[Math.floor(nums.length / 2)]

    /**
     * 方法二： Boyer-Moore 投票算法
     * 算法核心：对拼消耗(消除不同元素，直到没有不同元素即为所求)
     *
     * 执行用时: 64 ms, 在所有 JavaScript 提交中击败了95.42%的用户
     * 内存消耗: 37 MB, 在所有 JavaScript 提交中击败了99.58%的用户
     */
    // var majority = nums[0]
    // var count = 1
    // for (var i = 1; i < nums.length; i ++) {
    //     if (count === 0) {
    //         majority = nums[i]
    //     }
    //     if (nums[i] === majority) {
    //         count ++
    //     } else {
    //         count --
    //     }
    // }
    // return majority

    /**
     * 方法三： 通过对象存储每个元素出现的次数
     * 次数出现最多的那个即为众数。
     * 在本题中，出现次数大于数组长度的一半的元素即为众数
     * 
     * 执行用时: 68 ms, 在所有 JavaScript 提交中击败了89.69%的用户
     * 内存消耗: 37.6 MB, 在所有 JavaScript 提交中击败了65.28%的用户
     */
    let map = new Map()
    for (var num of nums) {
        if (map.has(num)) {
            map.set(num, map.get(num) + 1)
        } else {
            map.set(num, 1)
        }
    }
    for (var [key, val] of map) {
        if (val > nums.length / 2) {
            return key
        }
    }
};
```