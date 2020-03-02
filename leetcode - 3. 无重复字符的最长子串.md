8、[无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

给定一个字符串，请你找出其中不含有重复字符的 **最长子串** 的长度。

**示例 1:**

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```
**示例 3:**

```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```


**解题:**

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    /**
     * 方法一： 滑动窗口
     * 从头遍历，把重复元素从左侧移出，找出最长长度
     * 
     * 时间复杂度: O(n)
     * 执行用时: 92 ms, 在所有 JavaScript 提交中击败了85.42%的用户
     * 内存消耗: 37.7 MB, 在所有 JavaScript 提交中击败了89.95%的用户
     */
    // var max_len = 0
    // var left = 0
    // var map = new Map()
    // for (var i = 0; i < s.length; i ++) {
    //     var cur = s[i]
    //     left = map.get(cur) >= left ? map.get(cur) + 1 : left
    //     map.set(cur, i)
    //     max_len = Math.max(max_len, i - left + 1)
    // }
    // return max_len

    /**
     * 方法二： 原理同上(实现方式不同)
     * 定义一个新变量存储最长的非重复字符串
     * 
     * 执行用时: 84 ms, 在所有 JavaScript 提交中击败了96.19%的用户
     * 内存消耗: 39.8 MB, 在所有 JavaScript 提交中击败了61.76%的用户
     */
    var max_len = 0
    var max_str = ''
    for (var i = 0; i < s.length; i ++ ) {
        var cur_char = s[i]
        var isExist = max_str.indexOf(cur_char)
        if (isExist === -1) {
            max_str += cur_char
            max_len = max_len < max_str.length ? max_str.length : max_len
        } else {
            max_str = max_str.substr(isExist + 1) + cur_char
        }
    }
    return max_len
};
```

