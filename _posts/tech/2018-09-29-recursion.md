---
layout: post
title: " 学写递归必看 "
excerpt: " Sep 29 怼周会分享 "
categories: tech
tags: [怼周会]
author: 沥川
modified:
---

## 继续刷算法
- 痛并快乐
- 有点痛苦
- 有点上瘾

## 心情和状态
```
if h <= 5min and idea is None:
    return look up answer and it`s ok.
if h < 1h and solve:
    return good and happy!
if h < 5h and some ideas and not solve:
    return don`t want talk
if h > 5h and much ideas and not solve:
    return let me die
```
## 学写递归必看
- 算法题里面递归问题, 必须要掌握, 没法绕开
- 本周 32h 40+题, 其中有 20+ 递归问题 (因为树型结构天生递归)
- 从不理解 => 熟练运用
- [写递归函数的正确思维方法](https://blog.csdn.net/vagrxie/article/details/8470798) 给了很大的启发
- 关键 Paul Graham, 我总结成下面的一般解法:

```
递归两步骤
1. 解决基本问题. (0, 1, null...)
2. 解决一般情况. 一般情况 => 更小子集 (用有限步骤)

解决这两个问题就搞定了, 大大的简化了问题, 而且很容易写
```

## 一些递归练习题 
- [144. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/description/)
- [94. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/description/)
- [145. 二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/description/)
- [104. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/description/)
- [101. 对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/description/)
- [112. 路径总和](https://leetcode-cn.com/problems/path-sum/description/)
- [98. 验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/description/)
- [236. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)

## Changelog
* 18.9.29 init.

