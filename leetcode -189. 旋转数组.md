4、旋转数组 `https://leetcode-cn.com/problems/rotate-array/`

给定一个数组，将数组中的元素向右移动 *k* 个位置，其中 *k* 是非负数。

**示例1:**

```
输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]
```
**示例2:**

```
输入: [-1,-100,3,99] 和 k = 2
输出: [3,99,-1,-100]
解释: 
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]
```
**说明:**

```
尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
要求使用空间复杂度为 O(1) 的 原地 算法。
```

**解题:**

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var rotate = function(nums, k) {
    /**
     * 方法一：切片和插入
     * 执行用时: 72 ms, 在所有 JavaScript 提交中击败了91.72%的用户
     * 内存消耗: 35.2 MB, 在所有 JavaScript 提交中击败了83.96%的用户
     */

    // 计算k和数组长度的余数
    k = k % nums.length
    // 数组切割
    var temp = nums.splice(-k, k)
    nums.unshift(...temp)

    /**
     * 方法二：循环+出入栈 
     * 循环k % nums.length次
     * 执行用时: 100 ms, 在所有 JavaScript 提交中击败了55.97%的用户
     * 内存消耗: 35.5 MB, 在所有 JavaScript 提交中击败了44.10%的用户
     */
    // var count = 0
    // k %= nums.length
    // while (count < k) {
    //     var popData = nums.pop()
    //     nums.unshift(popData)
    //     count ++
    // }

}

```