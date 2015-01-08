---
title: Randomized Algorithm Problem 1.7
layout: post
tags: ['public', 'post', 'compiler','gcc', 'Randomized Algorithm']
time: 2014-04-06 08:34
mathjax: true
---

Randomized Algorithm一书练习题1.7是这么一个题目

> **1.7 ** 设我们从有序集$N=\{1,2,\cdots,N\}$的所有置换中均匀随机地选择置换$\pi$。令$L(\pi)$表示置换$\pi$中最长递增子序列的长度。

> (a) 对于足够大的$n$和某个常数$c$，证明$E(L(\pi))\geq c\sqrt{n}$。

> (b) (a)中的界是否是紧的?

<del>暂时只搞出来(a)问，(b)先留个坑。<del>

###证明###

(a) 定义$D(\pi)$为$\pi$中最长递降子序列的长度，那么显然有$E(L(\pi))=E(D(\pi))$。

```latex
\begin{align}
E(L(\pi))&=\dfrac{1}{n!}\sum_{p\in\{\pi\}} L(p)\\
E(D(\pi))&=\dfrac{1}{n!}\sum_{p\in\{\pi\}} D(p)
\end{align}
```

那么

```latex
\begin{align}
E(L(\pi))&=\dfrac{1}{2}\left[E(L(\pi))+E(D(\pi))\right]\\
&=\dfrac{1}{n!}\sum_{p\in\{\pi\}} \dfrac{L(p)+D(p)}{2}\\
&\geq \dfrac{1}{n!}\sum_{p\in\{\pi\}} \sqrt{L(p)D(p)}
\end{align}
```

对于任意的一个排列$p$，考察一下$L(p)D(p)$。$L(p)$和$D(p)$可以使用动态规划算法进行计算。记$l_k$为以$k$为结尾的最长递增子序列长度，$d_k$类似。

```latex
\begin{align}
l_0&=d_0=1 \\
l_k&=\max_{i=0}^{k-1}(l_i+\Delta l_i)\\
d_k&=\max_{i=0}^{k-1}(d_i+\Delta d_i)
\end{align}
```

当仅当$p_k > p_i$时候$\Delta l_i=1$，否则为0。当仅当$p_k < p_i$时候$\Delta D_i=1$，否则为0。

由于$p$是全排列，$p_k > p_i$和$p_k < p_i$有且仅有一个会成立，于是$l_k \neq l_i$或者$g_k \neq g_i$，或者说所有的二元组$(l_k, g_k)$都互不相等。

而

```latex
\begin{align}
L(p)&=\max\limits_{i=0}^{n-1}l_i \\
D(p)&=\max\limits_{i=0}^{n-1}d_i
\end{align}
```
于是有

```latex
\begin{align}
(l_k, g_k) &\in \{1,2,\ldots, L(p)\} \times \{1,2,\ldots, D(p)\} \\
\{(l_k, g_k)\} &\subseteq \{1,2,\ldots, L(p)\} \times \{1,2,\ldots, D(p)\} \\
\left|\{(l_k, g_k)\}\right| &\leq \left|\{1,2,\ldots, L(p)\} \times \{1,2,\ldots, D(p)\}\right| \\
n &\leq L(p)D(p)
\end{align}
```

于是证得

```latex
\begin{align}
E(L(\pi))&\geq \dfrac{1}{n!}\sum_{p\in\{\pi\}} \sqrt{L(p)D(p)} \\
&\geq \dfrac{1}{n!}\sum_{p\in\{\pi\}}\sqrt{n} \\
&= \dfrac{1}{n!}\cdot n!\cdot \sqrt{n} \\
&=\sqrt{n}
\end{align}
```

(b) 记$X_k$ 为排列$\pi$的长度为$k$的递增子序列数量。容易得到$X_k=C_n^kA_n^{n-k}$(选择$k$个位置作为递增子序列，然后选$n-k$个数放到剩下的$n-k$个位置上去排列，选出的$k$个位置递增排序)

``` latex
\begin{align}
E(X_k)&= \dfrac{1}{n!}C_n^kA_n^{n-k} \\
	  &= \dfrac{1}{k!}C_n^k
\end{align}
```

由期望的定义$E(X\_k)=\sum\limits\_{i=1}^niP(X\_k=i)\geq\sum\limits\_{i=1}^nP(X\_k=i)=P(X\_k\geq 1)$.

``` latex
\begin{align}
P(L(\pi)\geq k) & = P(X_k \geq 1) \\
				& \leq E(X_k) \\
				& = \dfrac{1}{k!}C_n^k \\
				& = \dfrac{n(n-1)\ldots(n-k+1)}{k!k!}
\end{align}
```

由于$n(n-1)\ldots(n-k+1)\leq n^k$和$k!\geq(\dfrac{k}{e})^k$

``` latex
\begin{align}
 P(L(\pi)\geq k)&= \dfrac{n(n-1)\ldots(n-k+1)}{k!k!} \\
				&\leq \dfrac{n^ke^{2k}}{k^{2k}} \\
				&= (\dfrac{ne^2}{k^2})^k
\end{align}
```

我们固定取$k=\lceil (1+\delta)e\sqrt{n}\rceil, \delta>0$

``` latex
\begin{align}
 P(L(\pi)\geq k)&\leq (\dfrac{ne^2}{k^2})^k \\
				&\leq \left(\dfrac{ne^2}{(1+\delta)^2e^2n)}\right)^k \\
				&= \left(\dfrac{1}{1+\delta}\right)^{2k} \\
\end{align}
```

再来计算$E(L(\pi)\geq k)$

``` latex
\begin{align}
E(L(\pi)) &= \sum_{i=1}^{k-1}iP(L(\pi)=i)+\sum_{i=k}^{n}iP(L(\pi)=i) \\
          &\leq \sum_{i=1}^{k-1}kP(L(\pi)=i) + \sum_{i=k}^{n}nP(L(\pi)=i) \\
		  &= kP(L(\pi)<k)+nP(L(\pi)\geq k) \\
		  &\leq k+n\left(\dfrac{1}{1+\delta}\right)^{2k}
\end{align}
```

注意到$n\left(\dfrac{1}{1+\delta}\right)^{2k}$在$n\rightarrow \infty$时极限为0。于是$n$足够大的时候$E(L(\pi))\leq k$。

也就是$E(L(\pi))=O(k)=O(\sqrt{n})$，而由(a)得到$E(L(\pi))=\Omega(\sqrt{n})$，于是这个界是紧的。



