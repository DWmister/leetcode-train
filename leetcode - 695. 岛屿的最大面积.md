21、[岛屿的最大面积](https://leetcode-cn.com/problems/max-area-of-island/)

给定一个包含了一些**0**和**1**的非空二维数组`grid`, 一个**岛屿**是由四个方向 (水平或垂直) 的`1`(代表土地) 构成的组合。你可以假设二维矩阵的四个边缘都被水包围着。

找到给定的二维数组中最大的岛屿面积。(如果没有岛屿，则返回面积为0。)

**示例 1：**

```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
```

对于上面这个给定矩阵应返回 `6`。注意答案不应该是11，因为岛屿只能包含水平或垂直的四个方向的‘1’。

**示例 2：**

```
[[0,0,0,0,0,0,0,0]]
```

对于上面这个给定的矩阵, 返回 `0`。

**说明：**

DFS（深度优先搜索）和 BFS（广度优先搜索）的对比图：

![DFS 与 BFS](https://pic.leetcode-cn.com/725e473003c35e3be67ac6177cc6744fa04b0466795b5e69c7d673f626206b86-file_1583293748397)

**解题:**

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var maxAreaOfIsland = function(grid) {
    /**
     * 方法一： DFS
     * 递归判断每一个位置是否为1，并将其置为0，在加其周围四个方向的值
     * 注意：边界处理
     *
     * 执行用时: 80 ms, 在所有 JavaScript 提交中击败了91.67%的用户
     * 内存消耗: 36.2 MB, 在所有 JavaScript 提交中击败了85.37%的用户
     * 时间复杂度：O(r*c) r、c分别为网格的行数列数，每个网格有且只访问一次
     * 空间复杂度：O(r*c)
     */
    // let result = 0
    // for (var i = 0; i < grid.length; i ++) {
    // 	for (var j = 0; j < grid[0].length; j ++) {
    // 		if (grid[i][j] === 1) {
    // 			result = Math.max(result, dfs(grid, i, j))
    // 		}
    // 	}
    // }
    // return result
    
  		/**
	     * 方法二： BFS
	     */
	    // 存放所有值为1的坐标
	    var position = []
	    for (var i = 0; i < grid.length; i ++) {
	        for (var j = 0; j < grid[0].length; j ++) {
	            if (grid[i][j] === 1) {
	                position.push([i, j])
	            }
	        }
	    }
	    // 四个方向
	    var direction = [[-1, 0], [1, 0], [0, -1], [0, 1]]
	    // 记录每个位置是否已被访问 (创建了一个与grid相同网格数的二维数组)
	    var visited = new Array(grid.length).fill(0).map(_ => new Array(grid[0].length).fill(0))
	    var max_area = 0
	    var cur_area = 0
	    while (position.length) {
	        var [x, y] = position.pop()
	        cur_area += 1
	        // 临时缓存位置为1的地方,判断其四个方向是否为1，是则添加它们，去除该位置的缓存
	        var stack = [[x, y]]

	        while (stack.length) {
	            var [x, y] = stack.pop()
	            visited[x][y] = 1
	            for (var d of direction) {
	                var new_x = x + d[0]
	                var new_y = y + d[1]
	                if (0 <= new_x && new_x < grid.length && 0 <= new_y && new_y < grid[0].length && !visited[new_x][new_y] && grid[new_x][new_y] === 1) {
	                    visited[new_x][new_y] = 1
	                    cur_area += 1
	                    stack.push([new_x, new_y])
	                }
	            }
	        }
	        max_area = Math.max(max_area,cur_area)
	        cur_area = 0
	    }
	    return max_area
	};
	// function dfs(grid, i, j) {
	// 	if (i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] === 0) {
	// 		return 0
	// 	}
	// 	grid[i][j] = 0
	// 	let area =  1
	// 	area += dfs(grid, i + 1, j)
	// 	area += dfs(grid, i - 1, j)
	// 	area += dfs(grid, i, j +  1)
	// 	area += dfs(grid, i, j - 1)
	// 	return area
	// }
```