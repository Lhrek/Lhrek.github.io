---
layout:     post
title:      "lc17 电话号码的字母组合"
subtitle:   "给定一个仅包含数字2-9的字符串，返回所有它能表示的字母组合"
date:       2024-06-14 09:35:39
author:     "GanZJ"
header-img: "img/africa.jpg"
catalog: true
tags:
  - dfs
  - 每日一题
---

Backtracking（回溯）属于 DFS。

- 普通 DFS 主要用在 **可达性问题** ，这种问题只需要执行到特点的位置然后返回即可。
- 而 Backtracking 主要用于求解 **排列组合** 问题，例如有 { 'a','b','c' } 三个字符，求解所有由这三个字符排列得到的字符串，这种问题在执行到特定的位置返回之后还会继续执行求解过程。

因为 Backtracking 不是立即返回，而要继续求解，因此在程序实现时，需要注意对元素的标记问题：

- 在访问一个新元素进入新的递归调用时，需要将新元素标记为已经访问，这样才能在继续递归调用时不用重复访问该元素；
- 但是在递归返回时，需要将元素标记为未访问，因为只需要保证在一个递归链中不同时访问一个元素，可以访问已经访问过但是不在当前递归链中的元素。



### 构建树

例如`23`,问题转化为这棵树所有空节点的路径

![image-20240614135320748](/img/in-post/image-20240614135320748.png)



todo











[17. 电话号码的字母组合 - 力扣（LeetCode）](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/description/)
