---
layout:     post
title:      "lc279 完全平方数"
subtitle:   "返回和为n的完全平方数的最少数量"
date:       2024-06-13 10:13:17
author:     "GanZJ"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
  - bfs
  - 动态规划
  - 每日一题
---

## BFS 

> - 可以将每个整数看成图中的一个节点，如果两个整数之差为一个平方数，那么这两个整数所在的节点就有一条边。
>- 要求解最小的平方数数量，就是求解从节点 n 到节点 0 的最短路径。
>   - 那么图中的边长是下限为1上限为sqrt(n)的完全平方数 
>   - 最短路径适合BFS，维护一个搜索队列。队列中的数据结构记录层数信息

![Pasted image 20240516110427](/img/in-post/Pasted image 20240516110427.png)

### 个人实现

```cpp
vector<int> getSquaresEdge(int n) {
  vector<int> ans;
  int i = 1;
  while (i * i <= n) {
    ans.push_back(i * i);
    i++;
  }
  return ans;
}

int numSquares(int n) { 
    vector<int> squares = getSquaresEdge(n);
    queue<pair<int, int>> q; 
    q.push(make_pair(0, 0)); 
    while(!q.empty()){
      pair<int,int> cur = q.front();
      q.pop();
      if(cur.first == n) return cur.second;
      for(int i = 0; i < squares.size(); i++){
          q.push(make_pair(cur.first + squares[i], cur.second + 1));
      }
    }
    return -1;
}
```

> 超时、内存不够

## 动态规划

//todo



[279. 完全平方数 - 力扣（LeetCode）](https://leetcode.cn/problems/perfect-squares/description/)

[CS-Note](https://www.cyc2018.xyz/算法/Leetcode 题解/Leetcode 题解 - 搜索.html#_1-计算在网格中从原点到特定点的最短路径长度)

