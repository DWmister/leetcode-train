[1052. 爱生气的书店老板](https://leetcode-cn.com/problems/grumpy-bookstore-owner/)

今天，书店老板有一家店打算试营业`customers.length`分钟。每分钟都有一些顾客`（customers[i]）`会进入书店，所有这些顾客都会在那一分钟结束后离开。

在某些时候，书店老板会生气。 如果书店老板在第`i`分钟生气，那么`grumpy[i] = 1`，否则`grumpy[i] = 0`。 当书店老板生气时，那一分钟的顾客就会不满意，不生气则他们是满意的。

书店老板知道一个秘密技巧，能抑制自己的情绪，可以让自己连续`X`分钟不生气，但却只能使用一次。

请你返回这一天营业下来，最多有多少客户能够感到满意的数量。

**示例:**

```
输入：customers = [1,0,1,2,1,1,7,5], grumpy = [0,1,0,1,0,1,0,1], X = 3
输出：16
解释：
书店老板在最后 3 分钟保持冷静。
感到满意的最大客户数量 = 1 + 1 + 1 + 1 + 7 + 5 = 16.
```

**解题:**

```js
/**
 * @param {number[]} customers
 * @param {number[]} grumpy
 * @param {number} X
 * @return {number}
 */
var maxSatisfied = function(customers, grumpy, X) {
    let result = 0
    let max = 0
    let temp = 0
    let left = 0, right = 0

    while (right < customers.length) {
        // 记录未开技能时，客户的满意量
        result += grumpy[right] ? 0 : customers[right]
        // 记录区间内可补偿的最大值(老板生气时候的值)
        temp += grumpy[right] ? customers[right] : 0

        if (right - left + 1 > X) {
            temp -= grumpy[left] ? customers[left] : 0
            left ++
        }
        right ++
        max = Math.max(max, temp)
    }
    return result + max
};
```