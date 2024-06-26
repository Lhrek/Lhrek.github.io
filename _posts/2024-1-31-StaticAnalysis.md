## 静态分析的基本概念

> **静态分析（Static Analysis）** 是指在实际运行程序 𝑃 之前，通过分析静态程序 𝑃 本身来推测程序的行为，并判断程序是否满足某些特定的 **性质（Property）** 𝑄 

我们会关心的程序性质可能有：

- 程序P是否会产生私有信息泄漏（Private Information Leak），或者说是否存在访问控制漏洞（Access Control Venerability）；
- 程序P是否有空指针的解引用(Null Pointer Dereference)操作，更一般的，是否会发生不可修复的运行时错误（Runtime Error）；
- 程序P中的类型转换（Type Cast）是否都是安全的；
- 程序P中是否存在可能无法满足的断言（Assersion Error）；
- 程序P中是否存在死代码（Dead Code, 即控制流在任何情况下都无法到达的代码）；

有些可惜的是，静态分析并不能对于我们上面关心的问题给出一个确切的答案。



## 静态分析的类型

### 完美的静态分析

> 如果一个静态分析 𝑆 能够对于程序 𝑃 的某个非平凡性质 𝑄给出确切的答案，我们就称 𝑆 是 𝑃 关于 𝑄 的 **完美静态分析（Perfect Static Analysis）** 。我们定义程序P的关于Q的真实行为为 **真相（Truth）** ，那么完美静态分析有两层含义：
>
> - **完全性（Soundness）**：真相一定包含在 𝑆 给出的答案中；
> - **正确性（Completeness）**：𝑆 给出的答案一定包含在真相中；
>
> 记这个静态分析程序给出的答案集合 𝐴 ，真相集合为 𝑇 ，则完美的静态分析满足：
>
> 𝑇⊆𝐴∧𝐴⊆𝑇⇔𝐴=𝑇
>
> 其中， 𝑇⊆𝐴 体现了完全性， 𝐴⊆𝑇 体现了正确性

### 妥协的静态分析

因为完美的静态分析并不存在，所以我们通常需要做一些妥协，也就是在 𝑇⊆𝐴 和 𝐴⊆𝑇 中只尽力满足其中一个条件，妥协另一个条件。

于是，我们得到了两种妥协后的静态分析类型

> 记程序 𝑃 的关于性质 𝑄 的静态分析S为 **Sound 的静态分析（Sound Static Analysis）** ，当且仅当 𝑆 给出的答案集合 𝐴 和 𝑃 关于 𝑄 的真相集合 𝑇 之间满足 𝑇⊆𝐴 ，这种分析策略也称作 **过近似（Over-approximation）** 。

> 记程序 𝑃 的关于性质 𝑄 的静态分析 𝑆 为 **Complete 的静态分析（Complete Static Analysis）** ，当且仅当 𝑆 给出的答案集合 𝐴 和 𝑃 关于𝑄的真相集合 𝑇 之间满足 𝐴⊆𝑇 ，这种分析策略也称作 **欠近似（Under-approximation）**

### 现实世界中有用的静态分析

大多数的静态分析会妥协正确性，保证完全性，即 Sound 的静态分析居多，这样的静态分析虽然不是完美的，但是有用的。以 debug 为例，在实际的开发过程中，Sound 的静态分析可以帮助我们有效的缩小 debug 的范围，我们最多只需要暴力排查掉所有的假积极实例（False Positive Instance）就可以了

















## reference

[静态分析 (cuijiacai.com)](https://static-analysis.cuijiacai.com/)

