---
layout:     post
title:      "lc200 岛屿数量"
subtitle:   "计算二维网格中岛屿的数量"
date:       2024-06-12 14:42:42
author:     "GanZJ"
header-img: "img/bg-islands.jpeg"
catalog: true
tags:
  - 每日一题
  - 连通分量
  - 岛屿问题
  - dfs
  - bfs
---



## 个人实现

将岛屿 转化成 海面 

```cpp
int numIslands(vector<vector<char>>& grid) {
    int ans = 0;
    for(int i = 0; i < grid.size(); i++) {
        for (int j = 0; j < grid[0].size(); j++){
            if(grid[i][j] == '1'){
                ans++;
                do{
                    grid[i][j] = '0';
                  //
                }while(1);

            }
        }
    }  
    return ans;     
}
```

卡壳： 在`if(grid[i][j] == '1')`后将该岛屿置成海洋，即如何从`(grid[i][j]`出发便利周围。 虽然但是，离谱得是这道题我清晰得记得我当初大一刚学c写过，而且当时写得很顺，那时都没听过算法这个概念。



```cpp
void dfs(vector<vector<char>>& grid,int i, int j){
    if(i < 0 || i >= grid.size() || j < 0 || j >= grid[0].size() || grid[i][j] == '0'){
        return;
    }
    grid[i][j] = '0';
    dfs(grid, i + 1, j);
    dfs(grid, i - 1, j);
    dfs(grid, i, j + 1);
    dfs(grid, i, j - 1);
}

int numIslands(vector<vector<char>>& grid) {
    int ans = 0;
    for(int i = 0; i < grid.size(); i++) {
        for (int j = 0; j < grid[0].size(); j++){
            if(grid[i][j] == '1'){
                dfs(grid, i, j);
                ans++;
            }
        }
    }  
    return ans;     
}
```

通过再实现一个函数递归调用来探索岛屿并将其重制

## 其他思路

### bfs 方法：

- 借用一个队列 queue，判断队列首部节点 (i, j) 是否未越界且为 1：
  - 若是则置零（删除岛屿节点），并将此节点上下左右节点 (i+1,j),(i-1,j),(i,j+1),(i,j-1) 加入队列；
  - 若不是则跳过此节点；
- 循环 pop 队列首节点，直到整个队列为空，此时已经遍历完此岛屿。







