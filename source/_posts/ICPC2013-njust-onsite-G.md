---
title: HDU4808-2013年ACM/ICPC南京赛区现场赛G题
layout: post
tags: ['public', 'post', 'algorithm', 'ACM/ICPC']
keywords: ['2013年南京赛区', '积分', '数学期望', 'HDU4808']
mathjax: true
time: 2013-11-23 17:52
---
> Jenny is initially located at the origin of the N-dimension Euclidean space. Each step can be represented by a random N-dimension vector$(x_1, x_2, \ldots, x_n)$ chosen uniformly from possible positions satisfying $x_i\geq 0$ and $x^2_1 + x^2_2 + \ldots + x^n_2 \leq R^2$. Assume the expectation of his coordinate after his first step is $(y_1, y_2, \ldots, y_n)$. He wants to know the minimum $y_i$ .

题目简单的说，在$\mathbf{R}^n$上均匀随机地取满足$x_i\geq 0, x_1^2+x_2^2+\ldots+x_n^2\leq R^2$的点$(x_1,x_2,\ldots,x_n), x_i \geq 0$，求期望坐标$(y_1,y_2,\ldots,y_n)$的最小的$y_i$。

题目说得很绕，其实期望坐标$(y_1,y_2,\ldots,y_n)$的每个分量肯定都是相等的，所以任意求一个维度的分量就好了。

设这个值为$C_n(R)$，那么根据多维随机变量的概率，得到积分式：

``` latex
\begin{align}
C_n(R) & = \dfrac{S_n(R)}{V_n(R)}
\end{align}
```

其中

``` latex
\begin{align}
S_n(R) & = \int\cdots\int_{x_1^2+x_2^2+\cdots+x_n^2\leq R^2, x_i\geq 0}x_1 dx_1dx_2\cdots dx_n \\
V_n(R) & = \int\cdots\int_{x_1^2+x_2^2+\cdots+x_n^2\leq R^2, x_i\geq 0}dx_1dx_2\cdots dx_n
\end{align}
```

其实$V\_n(R)$就是这个n维体的体积，而$C\_n(R)$就是$n$维体重心的坐标值。

## $V\_n(R)$的递推式

先来看看$V\_n(R)$这个n维球体积的积分式的计算(如果记住最好了，不过很多人模板里面都没这个)，对于$n>1$的情况

``` latex
\begin{align}
V_n(R) & = \int\cdots\int_{x_1^2+x_2^2+\cdots+x_n^2\leq R^2, x_i\geq 0}dx_1dx_2\cdots dx_n
\end{align}
```

先剥离最外一层积分式

``` latex
\begin{align}
V_n(R) & = \int_0^R\left\{\int\cdots\int_{x_1^2+x_2^2+\cdots+x_{n-1}^2\leq R^2-x_n^2, x_i\geq 0}dx_1dx_2\cdots dx_n\right\}dx_n
\end{align}
``` 

内层积分就是$V\_{n-1}$

``` latex
\begin{align}
V_n(R) & = \int_0^RV_{n-1}(\sqrt{R^2-x_n^2})dx_n
\end{align}
```

很容易想到$V_n(R)$的通项应该是如下的形式

``` latex
\begin{align}
V_n(R) & = p_nR^n
\end{align}
```

代入之前的递推关系

``` latex
\begin{align}
V_n(R) & = p_{n-1}\int_0^R(\sqrt{R^2-x_n^2})^{n-1}dx_n
\end{align}
```

使用三角函数进行换元，$x_n = R\sin\theta, \theta\in[0,\pi/2]$

``` latex
\begin{align}
V_n(R) & = p_{n-1}\int_0^{\pi/2}(R\cos\theta)^{n-1}R\cos\theta d\theta \\
& = p_{n-1}R^n\int_0^{\pi/2}\cos^n\theta d\theta
\end{align}
```

## $S\_n(R)$的递推式

对于$S_n(R)$，和$V_n(R)$类似地处理，把最外面的一维剥离开，对于$n>1$的情况

``` latex
\begin{align}
S_n(R) & = \int_{0}^{R}\left\{\int\cdots\int_{x_1^2+x_2^2+\cdots+x_{n-1}^2\leq R^2, x_i\geq 0}x_1 dx_1dx_2\cdots dx_{n-1}\right\}dx_n
\end{align}
```

得到$S\_n(R)$、$S\_{n-1}(R)$的递推关系

``` latex
\begin{align}
S_n(R) & = \int_{0}^{R}\left\{S_{n-1}(\sqrt{R^2-x_n^2})\right\}dx_n
\end{align}
```

$S_n(R)$是如下的形式

``` latex
\begin{align}
S_n(R) & =q_nR^{n+1} 
\end{align}
```

于是

``` latex
\begin{align}
S_n(R) & = \int_{0}^{R}q_{n-1}(\sqrt{R^2-x_n^2})^{n}dx_n
\end{align}
```

使用正弦函数进行换元，$x_n=R\sin\theta, \theta\in[0,\pi/2]$

``` latex
\begin{align}
S_n(R) & = q_{n-1}\int_{0}^{\pi/2}(R\cos\theta)^{n}R\cos\theta d\theta \\
& = q_{n-1}R^{n+1}\int_{0}^{\pi/2}\cos^{n+1}\theta d\theta
\end{align}
```

## $\int_0^{\pi/2}\cos^n\theta d\theta$的计算

根据以上推算，$S\_n(R)$和$V\_n(R)$的递推关系都和一个积分式子有关

``` latex
\begin{align}
V_n(R) & = p_nR^n \\
p_n & = p_{n-1}\int_0^{\pi/2}\cos^n\theta d\theta \\
S_n(R) & =q_nR^{n+1} \\
q_n & = q_{n-1}\int_{0}^{\pi/2}\cos^{n+1}\theta d\theta
\end{align}
```

现在单独求这个积分式

``` latex
\begin{align}
t_n & = \int_0^{\pi/2}\cos^n\theta d\theta
\end{align}
```

要求的结果已经可以表示为

``` latex
\begin{align}
C_n(R) & = \dfrac{S_n(R)}{V_n(R)} \\
       & = \dfrac{q_nR^{n+1}}{p_nR^n} \\
       & = \dfrac{q_n}{p_n} \cdot R \\
       & = \dfrac{q_{n-1}t_{n+1}}{p_{n-1}t_n} \cdot R (n>1)\\
       & = \cdots \\
       & = \dfrac{q_1t_{n+1}\cdots t_3}{p_1t_n\cdots t_2} \cdot R \\
       & = \dfrac{q_1t_{n+1}R}{p_1t_2}
\end{align}
```

对$t_n$进行变形

``` latex
\begin{align}
t_n & = \int_0^{\pi/2}\cos^n\theta d\theta \\
    & = \int_0^{\pi/2}\cos^{n-1}\theta d\sin\theta
\end{align}
```

$n>1$时，用分部积分公式变换一下，就又可以得到递推关系

``` latex
\begin{align}
t_n & = \cos^{n-1}\theta\sin\theta\bigg|_0^{\pi/2}-\int_0^{\pi/2}\sin\theta d\cos^{n-1}\theta \\
& = \int_0^{\pi/2}(n-1)cos^{n-2}\theta\sin^2\theta d\theta \\
& = (n-1)\int_0^{\pi/2}cos^{n-2}\theta(1-\cos^2\theta) d\theta \\
& = (n-1)(t_{n-2}-t_n)
\end{align}
```

于是有

``` latex
\begin{align}
t_n & = \dfrac{(n-1)t_{n-2}}{n} 
\end{align}
```

现在有了$t\_n(R)$的递推关系，计算出初值，就可预处理算出所有$t_n$。

``` latex
\begin{align}
p_1 & = 1 \\
q_1 & = \dfrac{1}{2} \\
t_0 & = \dfrac{\pi}{2} \\
t_1 & = 1 \\
t_n & = \dfrac{(n-1)t_{n-2}}{n}, n > 1
\end{align}
```

最终的$C\_n(R)$也就迎刃而解。
