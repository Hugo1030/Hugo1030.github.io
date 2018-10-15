---
layout: post
title: " 动态规划及如何快速学会新算法 "
excerpt: " Oct 13 怼周会分享 "
categories: tech
tags: [怼周会]
author: 沥川
modified:
---

## 动态规划 (Dynamic Programming)
- DP 的相关内容
- 以 DP 为例, 探讨一下, 如何迅速学习一个新算法


## DP 有什么用
```
A : "1+1+1+1+1+1+1+1 =？" 
A : "上面等式的值是多少"
B : 计算 "8!"
A : 在上面等式的左边写上 "1+" 
A : "此时等式的值为多少"
B : quickly "9!"

A : "你怎么这么快就知道答案了"
A : "只要在8的基础上加1就行了"
A : "所以你不用重新计算因为你记住了第一个等式的值为8!动态规划算法也可以说是 '记住求过的解来节省时间'"
```
- DP 的核心就是记住已经解决过的子问题的解
- 很简单, 但是超有用


## 超简单例子 (Fibonacci)

![](https://pics.ibrainbaby.cn/2018-10-13-124448.jpg)

fib(1), fib(2) = 1, 1


## 实际运用
- 其实就是对递归的优化, 本质是种思路
- 总会有一个表, 最终结果可以通过查表直接得到
- 这种思维不止是算法, 而是到处都能用到
    - 建表
    - 查表
    - 递归 

## 一些很棒练习
- [70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/description/)
- [121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/description/)
- [53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/description/)
- [198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/description/)
- [55. 跳跃游戏](https://leetcode-cn.com/problems/jump-game/description/)


## 如何学习一个新算法
- 一大堆代码 >> 看好书 = 听课

## Changelog
* 18.10.15 init.

