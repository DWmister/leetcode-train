### 滑动窗口类题的解法总结

#### 注意点

- 具有两个边界，分别为`left`和`right`，[left, right]就构成一个窗口了(一般是左闭右开)；
- 初始位置都为最左侧，窗口大小为0；
- 为了保证时间复杂度为：**O(n)**，窗口永远只能向右移动

#### 窗口如何变化

- `right`变化，则窗口变大：当窗口内的条件未达到题目要求时，移动right
- `left`变化，则窗口变小：当窗口内的条件超过题目要求时(窗口溢出)，移动left

#### 难点

找到窗口变化的条件



例题：

1. 面试题57 - II. 和为s的连续正数序列
2. 无重复字符的最长子串
3. 将数组分成和相等的三个部分
4. 最小覆盖子串
5. 替换后的最长重复字符
