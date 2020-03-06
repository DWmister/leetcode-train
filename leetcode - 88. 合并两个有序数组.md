12、[合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

给定两个有序整数数组 *nums1* 和 *nums2*，将 *nums2* 合并到 *nums1* 中*，*使得 *num1* 成为一个有序数组。

**说明**:

初始化`nums1`和`nums2`的元素数量分别为`m`和`n`。
你可以假设`nums1`有足够的空间（空间大小大于或等于`m + n`）来保存`nums2`中的元素。

**示例:**

```
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```

**解题:**

```js
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function(nums1, m, nums2, n) {
    /**
     * 方法一： 直观的 切割合并排序
     * 
     * 执行用时: 68 ms, 在所有 JavaScript 提交中击败了61.44%的用户
     * 内存消耗: 34.8 MB, 在所有 JavaScript 提交中击败了36.73%的用户
     */
    // nums1.splice(m)
    // nums2.splice(n)
    // nums1.push(...nums2)
    // nums1.sort((a, b) => a - b)

    /**
     * 方法二： 双指针(从后往前)
     * 
     * 执行用时: 60 ms, 在所有 JavaScript 提交中击败了91.28%的用户
     * 内存消耗: 33.9 MB, 在所有 JavaScript 提交中击败了75.51%的用户
     */
    var p1 = m - 1
    var p2 = n - 1
    var p = m + n - 1
    while (p1 >= 0 && p2 >= 0) {
        if (nums1[p1] < nums2[p2]) {
            nums1[p] = nums2[p2]
            p2 --
        } else {
            nums1[p] = nums1[p1]
            p1 --
        }
        p --
    }
    // 如果nums2还存在，则将其剩余元素替换nums1的前面剩余元素
    if (p2 >= 0) {
        nums1.splice(0, p2 + 1, ...nums2.slice(0, p2 + 1))
    }
};
```