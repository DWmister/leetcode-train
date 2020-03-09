15、[零钱兑换](https://leetcode-cn.com/problems/coin-change/)

给定不同面额的硬币**coins**和一个总金额**amount**。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回`-1`。

**示例 1:**

```
输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1
```

**示例 2:**

```
输入: coins = [2], amount = 3
输出: -1
```
**说明：**

你可以认为每种硬币的数量是无限的。

**解题:**

```js
/**
 * @param {number[]} coins
 * @param {number} amount
 * @return {number}
 */
var coinChange = function(coins, amount) {
	    /**
	     * 方法： 动态规划
	     * 动态规划问题的一般形式就是求最值
	     * 求解动态规划的核心问题就是穷举，把所有可行的答案穷举出来，然后在其中找最值
	     *
	     * 动态规划问题的三要素：
	     * 1、穷举会存在‘重叠子问题’，如果暴力穷举的话效率会极其低下
	     * 2、动态规划问题具备‘最优子结构’，通过子问题的最值得到原问题的最值
	     * 3、只有列出正确的‘状态转移方程’(实际上就是描述问题结构的数学形式)才能正确的穷举
	     *
	     * 其中写出状态转移方程是最困难的
	     * 写出状态转移方程的思维框架：
	     * 明确‘状态’ ——> 定义dp数组/函数的定义 ——> 明确‘选择’ ——> 明确base case
	     *
	     * 最优子结构的特点：子问题间相互独立
	     * 例子：要求amount = 11的最少硬币数(原问题),如果知道amount = 10的最少硬币数(子问题)，只需把子问题的答案加一即可,以此类推。
	     *
	     * 推导该例子的状态转移方程：
	     * 1、明确状态：由于硬币数量是无限的，所以唯一的状态就是目标金额amount
	     * 2、定义dp数组：当前目标金额n(子问题的n)，至少需要dp[n]个硬币(用数组存放每个金额所需最少硬币数)
	     * 3、确定选择并优化：无论当前金额n是多少，从硬币列表中选择一个coin,则当前金额就会减少coin,即：dp[n-coin]+1 = dp[n]
	     * 4、最后：当目标金额为0时，所需硬币数为0；当目标金额<0时，返回-1
	     * 
	     * 
	     * 执行用时: 116 ms, 在所有 JavaScript 提交中击败了68.72%的用户
	     * 内存消耗: 41.3 MB, 在所有 JavaScript 提交中击败了38.07%的用户
	     */
	    // var dp = new Array(amount + 1).fill(Infinity)
	    // dp[0] = 0
	    // for (var n = 1; n <= amount; n ++ ) {
	    //     for (var coin of coins) {
	    //         if (n - coin >= 0) {
	    //             dp[n] = Math.min(dp[n], dp[n - coin] + 1)
	    //         }
	    //     }
	    // }
	    // return dp[amount] === Infinity ? -1 : dp[amount]

	    /**
	     * 以下是用时上的小优化
	     * 
	     * 执行用时: 108 ms, 在所有 JavaScript 提交中击败了70.74%的用户
	     * 内存消耗: 41.2 MB, 在所有 JavaScript 提交中击败了39.20%的用户
	     */
	    var dp = [0]
	    for (var n = 1; n <= amount; n ++ ) {
	        dp[n] = amount + 1
	        for (var coin of coins) {
	            if (n - coin >= 0) {
	                dp[n] = dp[n - coin] + 1 > dp[n] ? dp[n] : dp[n - coin] + 1
	            }
	        }
	    }
	    return dp[amount] > amount ? -1 : dp[amount]
	};
```