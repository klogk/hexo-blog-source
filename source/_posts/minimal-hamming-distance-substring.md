---
title: 寻找与目标串长度相同且Hamming距离最小的子串
layout: post
tags: ['public', 'post', 'algorithm', 'ACM/ICPC']
keywords: ['FFT', 'Hamming-Distance', '快速傅里叶变换', 'ACM/ICPC', '相似字符串', '编程之美挑战赛']
mathjax: true
time: 2013-04-16 22:35
---



微软2013全国编程之美挑战赛初赛第一场有这么一道[题目](http://programming2013.cstnet.cn/round1a/problem/2):

**对于两个长度相等的字符串(字符串长度不超过 50000),我们定义其距离为对应位置不同的字符数量,同时我们认为距离越近的字符串越相似.** 
   
**例如,“0123”和“0000”的距离为 3,“0123”和“0213”的距离则为 2,所以与“0000”相比,“0213”和“0123”最相似.**
 
**现在给定两个字符串 ``S1`` 和 ``S2``,其中 ``S2`` 的长度不大于 ``S1``.请在 ``S1``中寻找一个与 ``S2`` 长度相同的子串,使得距离最小.** 

简而言之,就是在S1中寻找与S2长度相同,[Hamming距离](http://en.wikipedia.org/wiki/Hamming_distance)最小的子串S1[i,...,i+m-1].一个直接的想法是枚举所有的起始点i,然后比较S1[i,...,i+m-1]和S2,这样的复杂度显然是不能够通过题目的大数据的.

再明确一下我们的目标就是,对函数D[i] = Hamming_dist(S1[i,...,i+m-1], S2),高效计算D[i].

容易想到m-D[i]的含义是S1[i,...,i+m-1]和S2相比,相同位置上相同字符的个数.能够找到相同字符的个数,自然也就能计算Hamming距离.考虑到字符种类比较少,只有数字,再简化一下问题,把D[i]的求解分解成10个子问题

- $D_0[i]$：对于数字0,有多少在S1[i,...,i+m-1]和S2上有相同位置？
- $D_1[i]$：对于数字1,有多少在S1[i,...,i+m-1]和S2上有相同位置？
- ...
- $D_9[i]$：对于数字9,有多少在S1[i,...,i+m-1]和S2上有相同位置？

那么 $D[i]=n-D_0[i]-...-D_9[i]$.

这样分解问题之后,就可以专心考虑其中一个$D_k[i]$了.考虑$D_k[i]$的时候,把S1和S2都做个变形,把等于k的字符换成1,不等于k的字符全部标记成0,记为S和T.这个替换非常重要,因为我们可以得到$D_k[i]$的等价问题：**$D_k[i]$等于,把S[i,...,i+m-1]和T看作m维向量做内积**

这样字符串问题,就变为了一个数学问题了.用数学符号来重写这个问题, 定义两个离散函数

``` latex
s(i) = \left\{
    \begin{align}
        0, & i < 0 ,\\
        S[i], &0 \leq i < n, \\
        0, &i \geq n.
    \end{align}
\right.
```
和
``` latex
t(i) = \left\{
    \begin{align}
        0, & i < 0 ,\\
        T[i], &0 \leq i < m, \\
        0, &i \geq m.
    \end{align}
\right.
```
定义函数$f(x)=\sum\limits_i s(i)t(i+x)$, 函数$f(x)$就是我们之前的$D_k[i]$.对$f(x)$做适当变形,定义函数$t'(i)=t(m-1-i)$), $f(x)$于是就变为了
``` latex
\begin{align}
    f(x) & = \sum_i s(i)t(i+x) \\
         & = \sum_i s(i)t'[m-1-(i+x)] \\
         & = \sum_i s(i)t'[(m-1-x)-i]
\end{align}
```
再定义$f'(x)$

``` latex
\begin{align}
    f'(x) & = f(m-1-x) \\
         & = \sum_i s(i)t'\{[m-1-(m-1-x)]-i\} \\
         & = \sum_i s(i)t'(x-i)
\end{align}
```

这就是离散函数$s(i)$和$t'(i)$的[卷积](http://en.wikipedia.org/wiki/Convolution).直接求离散函数的卷积复杂度是$O(mn)$的,需要用一次循环来计算每一个$f'(x)$,于是就是两重循环.

更快的方法是根据[卷积定理](http://en.wikipedia.org/wiki/Convolution_theorem),利用[快速傅里叶变换](http://en.wikipedia.org/wiki/Fast_Fourier_transform)来做.对$f'(x)$应用卷积定理.

``` latex
\begin{align}
    f'(x) & = \mathbb{F}^{-1}\{\mathbb{F}[\sum_i s(i)t'(x-i)]\} \\
         & = \mathbb{F}^{-1}\{\mathbb{F}[s(i)]\times \mathbb{F}[t'(i)]\}
\end{align}
```

分别求出$s(i)$和$t'(i)$的傅里叶变换,然后对应位置相乘之后,再取逆变换就计算得到了$f'(x)$,进而就能够知道$f(x)$,也就是$D_k[i]$.于是就能够算出D[i],进而解决整个问题.

代码框架如下,复杂度为$O(LlogL)$

``` cpp
    L = max(m, n)
    C = [0...0]
    for(i=0; i<10; ++i){
        for(j=0; j<L; ++j){
            s[j] = (S1[j]==i?0:1)
            t[j] = (S2[j]==i?0:1)
        }
        reverse(t, t+L);
        S = FFT(s, L), T = FFT(t, L)
        for(j=0; j<L; ++j)
            F[j] = S[j] * T[j]; 
        f[i] = IFFT(F, L)
        for(j=0; j<L; ++j)
            C[j] += f[j]
    }
    for(i=0; i<L; ++i)
        ans = min(ans, n-C[i]);
```

    
