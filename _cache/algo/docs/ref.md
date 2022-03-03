# 相关代码实现

## 11.二分查找

前提：有序
简单的二分查找：无重复元素

4 种变形：

- 查找第一个 x
- 查找最后一个 x
- 查找大于 x 的第一个
- 查找小于 x 的最后一个

## 20.字符串算法

- BF
- RK
- BM
- KMP

### BF 算法

BF: Brute Force 暴力匹配算法、也叫朴素匹配

A 中查找 B,A 叫主串，长度为 n，B 叫模式串，长度为 m。 将 A 中的 n -m + 1 个子串与 B 进行比较。

BF 理论上时间复杂度是 `O(n*m)`，但是在实际中很常用，因为：

- 实际中大部分情况下 n、m 不会太长，另外匹配到就停止了，所以一般会小于 `O(n*m)`
- 思想简单，代码不容易出错。在工程中，满足性能要求前提下，简单是首选。即 kiss(keep it simple and stupid) 设计原则。

### RK 算法

Rabin-Karp 算法，由两位发明人的名字命名, 是 BF 的升级版。

是将 n-m+1 个子串求 hash，然后和 B 的 hash 进行比较。hash 是一个数字，数字比较是非常快的。不过，通过哈希算法计算子串的哈希值的时候，我们需要遍历子串中的每个字符。尽管模式串与子串比较的效率提高了，但是，算法整体的效率并没有提高。

所以需要提高子串 hash 的计算效率。

比如只包含 a-z 可以转化为 26 进制， 而两个相邻字串是有关系的：

```
abc -> a* 26^2 + b * 26 ^1 + c * 26 ^ 0
bcd -> b* 26^2 + c * 26 ^1 + d * 26 ^ 0
```

![](imgs/2020-10-19-11-22-17.png)`

这样可以直接通过 `h[i-1]` 计算出 `h[i]`，所以加快了计算 hash 的时间。另外 26^x 可以提前计算好，存放在数组里，这样可以省去计算的时间。

RF 时间复杂度是 O(n)，但 hash 冲突多时，会退化到 `O(n*m)`。哈希冲突少时，可以直接先比较 hash，如果 hash 一样则再将子串和模式串进行比较。一般情况下 RF 效率都是要比 BF 高的。

计算机是如何比较数字的大小的？

比较两个数的指令计算机一般是做减法，然后有一个 condition code 寄存器，里面记录最近一次算数或逻辑操作的一些影响，比如是否有进位，是否有溢出，是否结果为 0， 是否结果为负等。逻辑比较时将两个数相减，然后检查上述标准，确定是大数减小数还是反之还是相等。有兴趣可以阅读计算机组成原理方面的书，《深入理解计算机系统》是一本不错的书。

## 动态规划

将问题分解为相互重复的子问题。

### 斐波那契数列

F(0) = 0
F(1) = 1
定义子问题：F(n) = F(n-1) + F(n-2)
反复执行：从 2 循环到 n，执行上面公式

与分而治之：将问题分解为相互独立的子问题。

### 70.爬楼梯

> [https://leetcode-cn.com/problems/climbing-stairs](https://leetcode-cn.com/problems/climbing-stairs)

- 子问题：`f(n) = f(n-1) + f(n-2)`
- 反复执行：从 2 开始循环，执行上面公式

### 198.打家劫舍

> [https://leetcode-cn.com/problems/house-robber](https://leetcode-cn.com/problems/house-robber)

子问题: `f(n) = max(f(n-1) , f(n-2) + v)`，`v` 表示当前家的打劫金额。

## 贪心算法

贪心算法：期望每个阶段的局部最优解，从而达到全局最优。结果并不一定是最优。

### 零钱兑换

### 455.分饼干

> [https://leetcode-cn.com/problems/assign-cookies/](https://leetcode-cn.com/problems/assign-cookies/)

1. 首先对 2 个数组进行排序，注意排序不传递参数是按字符来比较的 10 排在 2 前面。
2. 遍历饼干，如果饼干大于孩子值，则 i++。

### 122. 买卖股票的最佳时机 2

> [https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii)

- 只要后一天比前一天大，就买卖
- 注意边界索引越界，从 i = 1 开始遍历

### 392. Is Subsequence

题目：给定两个字符串 s 和 t, 问 s 是不是 t 的子序列

- 如 s = "abc", t = "ahbgdc"，则 s 是 t 的子序列，算法返回 true
- 如 s = "axc", t = "ahbgdc"，则 s 不是 t 的子序列，算法返回 false

实现如下： [代码实现](../leetcode/L392.h)

## 回溯算法

- 有很多路
- 有的路通，有的不通

### 46.全排列


## 学习资料
