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

通过子字符串出现的频率判断语言类型，相同的语言，子字符串出现得频率会更接近，通过比较被测文本与标准文档的[余弦相似性](https://zh.wikipedia.org/wiki/余弦相似性)确定语言类型。

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

` Map<string, double> result;`

`result[tmp]++; `



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



```cpp
string guessLanguageOf(const Map<string, double>& textProfile,
                       const Set<Corpus>& corpora) {
    if(corpora.isEmpty() || textProfile.isEmpty())
    {
        error("corpora or textProfile is empty");
            return "";
    }
    string res = "";
    double max_similarity = 0.0;
    for(auto i : corpora){
        if(max_similarity < cosineSimilarityOf(textProfile,i.profile)){
            res = i.name;
            max_similarity = cosineSimilarityOf(textProfile,i.profile);
        }
    }
    return res;
}
```

## Rising Tides

模拟海平面上升，分析二维表格中的海拔信息，判断在特定水面高度下被淹没的位置。

![image-20240615195117238](/img/in-post/image-20240615195117238.png)

参照（[lc279 完全平方数 - GanZJ's Blog](https://lhrek.github.io/2024/06/13/numSquares/)），同样是bfs。
