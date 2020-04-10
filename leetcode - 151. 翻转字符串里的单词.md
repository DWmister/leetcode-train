22、[翻转字符串里的单词](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

给定一个字符串，逐个翻转字符串中的每个单词。

**示例1:**

```
输入: "the sky is blue"
输出: "blue is sky the"
```

**示例2:**

```
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```

**示例3:**

```
输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

**说明:**

```
无空格字符构成一个单词。
输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

**解题:**

```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function(s) {
    // 方法一： 依次调用split/filter/reverse/join方法
    // return s.split(' ').filter(Boolean).reverse().join(' ')

    /**
     * 方法二：自定义过滤和反转的方法
     * Runtime: 52 ms, faster than 85.37% of JavaScript online submissions for Reverse Words in a String.
     * Memory Usage: 34.8 MB, less than 81.82% of JavaScript online submissions for Reverse Words in a String.
     */
    let arr = s.split(' ')
    let RevererArr = []
    for (let i = arr.length - 1; i >= 0; i --) {
        if (arr[i]) {
            RevererArr.push(arr[i])
        }
    }
    let result = RevererArr.join(' ')
    return result
};

```