---
layout:     post
title:      "符号执行初入门-CSA"
subtitle:   "记录符号执行的相关信息"
date:       2024-01-31 11:02:00
author:     "GanZJ"
header-img: "img/post-bg-HumanSystem.jpg"
catalog: true
tags:
  - 符号执行
  - 形式化验证
---



> **符号执行**（英语：symbolic execution）是一种[计算机科学](https://zh.wikipedia.org/wiki/计算机科学)领域的[程序分析](https://zh.wikipedia.org/wiki/程序分析)技术，通过采用抽象的符号代替精确值作为程序输入变量，得出每个路径抽象的输出结果。这一技术在硬件、底层程序测试中有一定的应用[[1\]](https://zh.wikipedia.org/wiki/符号执行#cite_note-1)，能够有效的发现程序中的漏洞。[[2\]](https://zh.wikipedia.org/wiki/符号执行#cite_note-2)

> [软件](https://zh.wikipedia.org/wiki/软件)系统的设计过程中，**形式验证**的含义是根据某个或某些形式规范或属性，使用[数学](https://zh.wikipedia.org/wiki/数学)的方法[证明](https://zh.wikipedia.org/wiki/证明)其[正确性](https://zh.wikipedia.org/wiki/正确性)或非正确性。



> **符号状态 σ ，它表示的是一个从变量到符号表达式的映射。其二是符号化路径约束PC（或者叫路径条件），这是一个==[无量词](https://baike.baidu.com/item/谓词逻辑#2)的一阶公式==，**



>符号执行是一种重要的形式化方法和静态分析技术



带状态的**CFG**?



## Q & A & D

Q1：符号化中涉及到的数据结构



Q2：约束求解器的用法



D1: ast cfg expled graph

D2: 收集爆炸图路径中的xxx

