---
title: FFT, 卷积, 多项式乘法, 大整数乘法
layout: post
tags: ['public', 'post', 'algorithm', 'ACM/ICPC']
keywords: ['FFT', '快速傅里叶变换', '大整数乘法', 'ACM/ICPC', '多项式乘法']
mathjax: true
time: 2013-06-26 20:35
---

以前总觉得快速傅里叶变换(FFT)是电子才用的东西, 虽然听说过FFT在大整数乘法中的应用, 但总的来说FFT的应用还是非常少的, 从来没有去深究过其中的联系.

直到上次编程之美比赛遇到了[这个题目](/posts/minimal-hamming-distance-substring/), 于是特意又去回顾了一下FFT, 并自己推导了一下其中的联系.

## DFT

一个序列{$x_i$}, $0\leq i<n$的离散傅里叶变换是这么一个东西($j$是虚数单位)

``` latex
\begin{align}
X_i & = \sum_{k=0}^{n-1}x_ke^{-2\pi jik/n} \\
    & = \sum_{k=0}^{n-1}x_k\omega_n^{ik}
\end{align}
```
$\omega_n = e^{-2\pi j/n}$被称为旋转因子, 因为从几何意义讲, $x_ke^{-2\pi jik/n}$就是在复平面上把$x_k$旋转$-2\pi ik/n$. FFT的几何意义也可以如此理解.

算法竞赛中一般是不会遇到复数序列的, 于是$X_i$通常都会是复数序列. 

## FFT

计算这个东西最naive的做法就是按照定义算, 对每一个$i$都做一遍循环, 复杂度是$O(n^2)$的. $O(n^2)$的算法总是让我们看不顺眼的, 要像$O(klogk)$这样才和谐. FFT就是一个$O(nlogn)$的算法.

FFT有很多变体, 最常见的一种做法是分治. 对原定义做一个变化, 把原序列拆分为奇偶序列. 简便起见, 我们设序列的长度为2的幂, 而且一般都是这么做的, 不是2的幂就加0补足.

``` latex
\begin{align}
X_i & = \sum_{k=0}^{n-1}x_{k}\omega_n^{ik} \\
    & = \sum_{k=0}^{n/2-1}x_{2k}\omega_n^{(2k)j} 
      + \sum_{k=0}^{n/2-1}x_{2k+1}\omega_n^{(2k+1)j} \\
    & = \sum_{k=0}^{n/2-1}x_{2k}(\omega_n^2)^{ik} 
      + \omega_n\sum_{k=0}^{n/2-1}x_{2k+1}(\omega_n^2)^{ik} \\
    & = \sum_{k=0}^{n/2-1}x_{2k}\omega_{n/2}^{ik} 
      + \omega_n\sum_{k=0}^{n/2-1}x_{2k+1}\omega_{n/2}^{ik}
\end{align}
```

注意上面的第一项实际是偶数项序列的傅里叶变换, 第二项是奇数项序列乘上一个系数. 于是递归就可以解出来了(这里可以不用递归, 直接自底向上算, 不过得小心注意变换位置).

有本书叫做[Inside the FFT Black Box: Serial and Parallel Fast Fourier Transform Algorithms](http://www.amazon.com/Inside-FFT-Black-Box-Computational/dp/0849302706), 网上很容易找到电子版, 介绍了很多种算法的变化.

还得有逆变换, 逆变换和正变换几乎一样

``` latex
\begin{align}
x_i & = \dfrac{1}{n} \sum_{k=0}^{n-1}X_ke^{2\pi jik/n} \\
    & = \dfrac{1}{n} \sum_{k=0}^{n-1}X_k(\dfrac{1}{\omega})^{ik}
\end{align}
```

也可以采用和正变换几乎一样的分治算法, 只需要除以系数和旋转因子取倒数即可. 一般的实现方法都是用一个tag参数来标记变换的方向.

## 卷积

两个函数的卷积的定义为

``` latex
\begin{align}
    (f*g)(i) & = \int_{-\infty}^{+\infty} f(k)g(i-k)dk
\end{align}
```

对于长度为n的离散序列

``` latex
\begin{align}
    (x*y)[i] & = \sum_{k=0}^{n-1} x[k]y[i-k]
\end{align}
```

著名的卷积定理就是, 卷积的傅里叶变换等于傅里叶变换然后相乘.


``` latex
\begin{align}
    \mathbb{F}[x*y] & = \mathbb{F}[x]\cdot \mathbb{F}[y]
\end{align}
```

## 卷积的应用

算法竞赛中FFT的应用, 通常都是卷积定理的运用.

卷积的现实意义是很多的.

例如, 多项式乘法, 如果把多项式看作是系数序列, 序列的第$i$项为幂次为i的项的系数.具体的说多项式$x[]$, $y[]$, 如果他们的积是$z[]$,那么会有

``` latex
z[i] = \sum x[k]y[i-k]
```

这就是一个卷积. 直接的多项式乘法展开是$O(n^2)$的. 如果用FFT来做, 先对系数序列做FFT, 然后做向量乘法, 再做IFFT, 那么就是$O(nlogn)$的.

再如大整数乘法, 本身和多项式乘法就很类似, 也可以用FFT来优化.

最近在某算法群, 有讨论这个题目, 三个长度在$10^5$以内的正整数序列$x$, $y$, $z$(所有整数也在$10^5$以内), 求满足$x[i]+y[j]=z[k]$的三元组$(i,j,k)$个数. 这也是一个多项式乘法, 先把$x$, $y$都变换成向量形式$X[i]$, $Y[i]$,第i维代表原序列中i的个数. 对$X$, $Y$做多项式乘法, 就能够得到等于每个$k$的$(i,j)$个数, 再筛选一下就可以了.

除了多项式乘法, 上面提到的编程之美的题目也是一个非常有代表性的例子.
