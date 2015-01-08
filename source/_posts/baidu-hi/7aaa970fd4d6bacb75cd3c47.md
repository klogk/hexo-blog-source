---
title: PKU1860 Currency Exchange
layout: post
tags: ['public', 'post', 'unber', acm/icpc & algorithm]
time: 2009-02-21 00:13
mathjax: false
---
<b>这篇文章最初发布在本人的百度空间：[http://hi.baidu.com/syncth/item/7aaa970fd4d6bacb75cd3c47](http://hi.baidu.com/syncth/item/7aaa970fd4d6bacb75cd3c47)，后来迁移到此处</b>

<p>题目给了一些货币和兑换点，给出各个兑换点兑换货币的汇率及手续费，要求通过货币兑换的方式，让货币增值。</p><p/><p>明显可以感觉是最短路模型(如果没有兑换点的手续费，和PKU2240 Arbitrage则是一样的做法)，不过重点在建图上：货币对应于节点，兑换点对应于一对有向边。之后进行bellman-ford。</p><p>关键词：图论 最短路 bellman-ford</p><p><a href="http://www.cnblogs.com/unber/archive/2009/02/21/1395224.html">click here to view  my code</a></p>
