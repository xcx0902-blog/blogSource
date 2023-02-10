---
title: XCX Round 2 Overall Editorial
date: 2023-01-19 10:10:02
tags:
  - XCX Round 2
  - Editorial
mathjax: true
---

## Problem A

概率与期望 + `DP`

令 $f_i$ 为 $i$ 张卡的合成概率，显然
$$f_i=a\% \times f_{i-5}+ \frac{1-a\%}{4} \times (f_{i-1}+f_{i-2}+f_{i-3}+f_{i-4})$$

初值：$f_5 = a\%$

答案：$f_b \times 100$

暴力转移即可。

时间复杂度：$O(b)$ per test case

空间复杂度：$O(b)$ per test case

## Problem B

高精度 + 二分

二分每一位的值，并使用高精度乘法判断即可。

令 $T = 120$，即保留的位数。

时间复杂度：$O(\log_2 x + T \times \log_2 10 \times T^2)$ per test case

空间复杂度：$O(T)$ per test case

## Problem C

01 Trie 树

令 $d_i$ 为点 $i$ 到树根的权值异或和，则 $f(i, j) = d_i \oplus d_j$。

只需做一个 Trie 树，将 $d$ 数组所有值加入，然后对于每个 $d_i$，求 Trie 树中与其异或最大的值即可。

时间复杂度：$O(n \log_2 \max_{w_i})$

## Problem D

模拟

由于是大模拟，不再赘述。细节详见代码。

## Problem E

组合数学 + 二项式定理

------

$20$ pts：暴力（不再赘述）

------

$50$ pts：

前置知识：二项式定理：

$$\sum_{i=0}^m x^i \cdot y^{m-i} \cdot C_m^i=(x+y)^m$$

然后，我们发现原来的式子中就有这个东西，于是把它提取出来后得：

$$\sum_{i=1}^m \sum_{j=1}^n \sum_{k=1}^n (j+k)^i$$

可以发现，上面这个式子与 $j, k$ 无关，只与 $j+k$ 有关。

然后，我们就可以枚举 $j+k$，将 $O(n^3)$ 优化为 $O(n^2)$。

新式子如下：

$$\sum_{i=1}^m \sum_{j=1}^{2 \times n} T \times j^i$$

其中，$T = n-|j-n-1|$。

原因如下：

当 $j=2$ 时，$1$ 次计算，

当 $j=3$ 时，$2$ 次计算，

当 $j=n+1$ 时，$n$ 次计算，

当 $j=2 \times n - 1$ 时，$2$ 次计算，

当 $j=2 \times n$ 时，$1$ 次计算。

------------

$100$ pts：

我们可以交换式子的两层循环，答案不变，即为

$$\sum_{j=1}^{2 \times n} T \times \sum_{i=1}^m j^i$$

我们需要快速计算

$$\sum_{i=1}^m j^i$$

将该式乘 $j$ 再减去该式，得到

$$j^{m+1}-j=(j-1)*\sum_{i=1}^m j^i$$

即

$$\sum_{j=1}^{m} j^i=\frac{j^{m+1}-j}{j-1}$$

带入原式，得到

$$\sum_{j=1}^{2 \times n} T\times\frac{j^{m+1}-j}{j-1}$$

由于 $10^9+7$ 是质数，所以求出 $j-1$ 的逆元即可。

时间复杂度：$O(n^2)$
