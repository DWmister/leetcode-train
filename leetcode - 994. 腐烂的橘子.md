7、[腐烂的橘子](https://leetcode-cn.com/problems/rotting-oranges/)

在给定的网格中，每个单元格可以有以下三个值之一：

- 值 0 代表空单元格；
- 值 1 代表新鲜橘子；
- 值 2 代表腐烂的橘子。

每分钟，任何与腐烂的橘子（在 4 个正方向上）相邻的新鲜橘子都会腐烂。

返回直到单元格中没有新鲜橘子为止所必须经过的最小分钟数。如果不可能，返回 -1。

**示例 1：**

**![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/16/oranges.png)**

```
输入：[[2,1,1],[1,1,0],[0,1,1]]
输出：4
```

**示例 2：**

```
输入：[[2,1,1],[0,1,1],[1,0,1]]
输出：-1
解释：左下角的橘子（第 2 行， 第 0 列）永远不会腐烂，因为腐烂只会发生在 4 个正向上。
```

**示例 3:**

```
输入：[[0,2]]
输出：0
解释：因为 0 分钟时已经没有新鲜橘子了，所以答案就是 0 。
```

**解题:**

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var orangesRotting = function(grid) {
    /**
     * 方法： 广度优先遍历(BFS)
     * 
     * 执行用时: 76 ms, 在所有 JavaScript 提交中击败了87.95%的用户
     * 内存消耗: 36.8 MB, 在所有 JavaScript 提交中击败了29.63%的用户
     */
    // 网格的长宽
    const H = grid.length
    const W = grid[0].length
    // 新鲜橘子的数量
    var fresh = 0
    // 存放腐烂橘子的栈
    var queue = []
    // 最小分钟数
    var minute = 0
    // 一分钟内的 新增的腐烂橘子
    var add_q = []


    // 循环行列计算出新鲜子的数量，并将腐烂橘子推入栈
    for (var r = 0; r < H; r++ ) {
        for (var c = 0; c < W; c++ ) {
            if (grid[r][c] === 1) {
                fresh ++
            }
            if (grid[r][c] === 2) {
                queue.push([r, c])
            }
        }
    }

    // 腐烂逻辑一
    // while (fresh && queue.length) {
    // 	add_q = []
    //     while (queue.length) {
    //         var [r, c] = queue.shift()
    //         // 上侧格子
    //         if (r - 1 >= 0 && grid[r - 1][c] === 1) {
    //             grid[r - 1][c] = 2
    //             fresh --
    //             add_q.push([r - 1, c])
    //         }
    //         // 下侧格子
    //         if (r + 1 < H && grid[r + 1][c] === 1) {
    //             grid[r + 1][c] = 2
    //             fresh --
    //             add_q.push([r + 1, c])
    //         }
    //         // 左侧格子
    //         if (c - 1 >= 0 && grid[r][c - 1] === 1) {
    //             grid[r][c - 1] = 2
    //             fresh --
    //             add_q.push([r, c - 1])
    //         }
    //         // 右侧格子
    //         if (c + 1 < W && grid[r][c + 1] === 1) {
    //             grid[r][c + 1] = 2
    //             fresh --
    //             add_q.push([r, c + 1])
    //         }
    //     }
    //     minute += 1
    //     queue = add_q
    // }

    // 腐烂逻辑二：
    // 定义可污染的四个方向 上下左右
    var direction = [[-1, 0], [1, 0], [0, -1], [0, 1]]
    while (fresh && queue.length) {
        let len = queue.length
        while (len--) {
            var [r, c] = queue.shift()
            for (var i = 0; i < 4; i ++ ) {
                var dx = r + direction[i][0]
                var dy = c + direction[i][1]
                if (dx < 0 || dx >= H || dy < 0 || dy >= W || grid[dx][dy] !== 1) {
                    continue
                }
                fresh --
                grid[dx][dy] = 2
                queue.push([dx, dy])
            }
        }
        minute += 1
    }

    // 如果还有新鲜橘子幸存，则返回-1，否则 返回最小分钟数
    return fresh ? -1 : minute
};
```