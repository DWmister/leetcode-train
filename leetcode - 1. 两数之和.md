1、两数之和 https://leetcode-cn.com/problems/two-sum/

给定一个整数数组 `nums` 和一个目标值 `target`，请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

**示例:**

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```
**解题:**

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    /**
     * 首先创建一个空对象
     * 只需要一层循环设置对象的key和value
     * key：数组内每个元素与target的差值
     * value: 当前元素在数组内的下标
     * 如果这个对象的key中含有数组内的某一项，则返回这个对象key的value和数组内那一项的下标
     * 时间复杂度：O(n)
     * 
     * 执行用时: 60 ms, 在所有 JavaScript 提交中击败了95.29%的用户
     * 内存消耗: 34.7 MB, 在所有 JavaScript 提交中击败了59.81%的用户
     */
    let obj = {}
    for (var i = 0; i < nums.length; i ++) {
        if (obj.hasOwnProperty(nums[i])) {
            return [obj[nums[i]], i]
        }
        obj[target -  nums[i]] = i
    }
}
```
