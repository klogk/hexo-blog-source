---
title: PRIM算法的证明 
layout: post
tags: ['public', 'post', 'algorithm','proof', 'prim algorithm']
time: 2010-11-10 12:34
mathjax: true
---
## 证明思路

对算法执行步数归纳,证明前$k$步选择的边都包含在某个最小生成树中.

## 证明过程

** 归纳基础, $k=1$ **

不妨设Prim算法选择的是$(1,a)$. 反证法, 如果$(1,b)$不在任何和最小生成树中, 取任意一棵最小生成树$T$.

1. $(1,a)$如果在$T$中, 那么直接得证;
2. $(1,a)$不在$T$中,用$(1,a)$去交换1在T中相连的任意一边$(1,b)$,即$T'=T-\\{(1,a)\\} + \\{(1,b)\\}$, $(1,a)$是1相连的所有边中最短的,所以$T'$的权值小于$T$的权值,和$T$是最小生成树发生矛盾.
于是$(1,a)$存在于某棵生成树中.

** 归纳过程: Prim算法前$k$步选择的边都被包含在某个最小生成树中. **

仍然使用反证法,假设Prim算法第$k+1$步选择的边$(a,b)$ 和前 $k$ 步选择的边不包含在任何最小生成树中.

设包含前$k$步选择边的一棵最小生成树为T, 记前$k$步选择的边构成的点集合为$S$,设$S$和$V-S$之间的边是$(a',b')$,由Prim算法的选择过程,显然有$(a',b')$的权值大于$(a,b)$(否则就Prim算法就选择$(a',b')$).

用$(a,b)$去替换换$(a',b')$,得到新的生成树$T-\\{(a',b')\\}+\\{(a,b)\\}$具有更小的权值,和$T$是最小生成树矛盾.于是Prim算法第$k+1$步选择的边$(a,b)$和前$k$步选择的边一起包含在某棵最小生成树里面.

由数学归纳法,Prim算法得证.
