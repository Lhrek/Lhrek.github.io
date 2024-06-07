---
layout:     post
title:      "CS106B Assignments2"
subtitle:   "Fun with collections(22.winter)"
date:       2024-06-04 22:22:09
author:     "GanZJ"
header-img: "img/post-bg-cs106b.jpeg"
catalog: true
tags:
  - cs106b
---

## Rosetta Stone

通过三元组判断语言类型

```cpp
Map<string, double> kGramsIn(const string& str, int kGramLength) {
    /* TODO: Delete this comment and the other lines here, then implement
     * this function.
     */
    if(kGramLength <= 0)
        error("kGramLength less than zero");
    if(kGramLength > str.length())
        return {};
    Map<string, double> result;
    for(int i = kGramLength-1;i< str.length();i++){
        string tmp = str.substr(i- kGramLength + 1, kGramLength);
        result[tmp]++;   
    }
    return result;
}
```

> 记录某个字符串出现得次数，直接使用map结构的result[tmp]++，若是第一次出现，则会初始化并计数加一。



```cpp
//采用cosine similarity进行标准化
Map<string, double> normalize(const Map<string, double>& input) {
    if(input.isEmpty())
    {
        error("the input is empty");
        return {};
    }
    double quadratic_sum = 0;
    for(auto i : input){
        quadratic_sum += input[i] * input[i];
    }
    double squareRoot = sqrt(quadratic_sum);
    if(squareRoot == 0.0)
    {    error("at least one nonzero value");
        return {};
    }
    Map<string, double> result;
    for(auto i : input){
        result[i] = input[i]/squareRoot;
    }
    return result;
}
```

```cpp
//保留numToKeep个数据
Map<string, double> topKGramsIn(const Map<string, double>& source, int numToKeep) {
    PriorityQueue<string> pd;
    for(auto i : source){
        pd.enqueue(i,source[i]);
    }
    if(source.size() - numToKeep < 0)
        return source;
    if(numToKeep < 0){
        error("numToKeep is negative");
        return {};
    }
    for(int i = 0; i < source.size() - numToKeep; i++){
        pd.dequeue();
    }
    Map<string, double> result;
    while(!pd.isEmpty()){
        string temp = pd.dequeue();
        result[temp] = source[temp];
    }
    return result;
}
```

```cpp
//计算两个频率列表的相似度
double cosineSimilarityOf(const Map<string, double>& lhs, const Map<string, double>& rhs) {
    double res = 0.0;
    for(auto i : lhs){
        res +=  lhs[i]*rhs[i];
    }
    return res;
}
```



