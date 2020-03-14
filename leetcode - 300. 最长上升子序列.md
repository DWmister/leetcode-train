20、[最长上升子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

给定一个无序的整数数组，找到其中最长上升子序列的长度。

**示例:**

```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
```

**解题:**

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var lengthOfLIS = function(nums) {
    /**
     * 方法一： 动态规划
     * 设置dp数组，存放以每个元素结尾的 最长上升子序列的长度
     * 注意：这个子序列可以不是连续的
     */
    // const len = nums.length
    // if (!len) {
    // 	return 0
    // }
    // if (len === 1) {
    // 	return 1
    // }
    // var dp = new Array(len).fill(1)
    // for (var i = 1; i < len; i++) {
    // 	for (var j = 0; j < i; j++) {
    // 		dp[i] = Math.max(dp[i], nums[j] < nums[i] ? dp[j] + 1 : 1)
    // 	}
    // }
    // return Math.max(...dp)

    /**
     * 方法二：双指针
     * 递归获取最长子序列，返回其长度
     */
    var list = []
    for (num of nums) {
    	recursion(list, num)
    }
    return list.length
};
function recursion(list, n) {
    const len = list.length
    if (!len || n > list[len - 1]) {
        return list.push(n)
    }
    if (len === 1 && n < list[0]) {
        return list[0] = n
    }

    var left = 0
    var right = len - 1
    while (left <= right) {
        var mid = Math.floor((left + right) / 2)
        if (n > list[mid]) {
            left  = mid + 1
        } else {
            right = mid - 1
        }
    }
    list[left] = n
}
```