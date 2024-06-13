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

> 超时、内存不够。
>
> 优化方向：
>
> - 只向队列中添加有效的和小于等于 n 的状态
>
> - 记录已访问得节点，访问后不再将其加入到队列.使用更有效的数据结构来跟踪访问状态，例如布尔数组而不是集合（这可以减少哈希操作的开销）。
>   - `std::vector<bool> visited(n + 1, false)`记录访问情况 
>   - 反面教材:`set<int> visited;` `if (visited.find(cur.first + squares[i]) != visited.end() || (cur.first + squares[i] > n)) continue;`

```cpp

int numSquares(int n) {
    std::vector<int> squares;
    for (int i = 1; i * i <= n; i++) {
        squares.push_back(i * i);
    }

    std::vector<bool> visited(n + 1, false); 
    std::queue<std::pair<int, int>> q;
    q.push({0, 0});

    while (!q.empty()) {
        auto [curSum, steps] = q.front();
        q.pop();

        for (int square : squares) {
            int nextSum = curSum + square;
            if (nextSum == n) return steps + 1;
            if (nextSum > n) break;
            if (!visited[nextSum]) {
                visited[nextSum] = true;
                q.push({nextSum, steps + 1});
            }
        }
    }
    return -1;
}
```



## 动态规划

将问题转化为相似得子问题，同时记录下子问题的解。

背包问题：[【动态规划/背包问题】那就从 0-1 背包问题开始讲起吧 ... (qq.com)](https://mp.weixin.qq.com/s/xmgK7SrTnFIM3Owpk-emmg)

//todo



[279. 完全平方数 - 力扣（LeetCode）](https://leetcode.cn/problems/perfect-squares/description/)

[CS-Note](https://www.cyc2018.xyz/算法/Leetcode 题解/Leetcode 题解 - 搜索.html#_1-计算在网格中从原点到特定点的最短路径长度)

