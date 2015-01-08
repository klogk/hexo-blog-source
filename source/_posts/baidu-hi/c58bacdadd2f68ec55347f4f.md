---
title: PKU1635 Subway tree systems有根树的同构判定
layout: post
tags: ['public', 'post', 'unber', acm/icpc & algorithm]
time: 2009-08-04 21:36
mathjax: false
---
<b>这篇文章最初发布在本人的百度空间：[http://hi.baidu.com/syncth/item/c58bacdadd2f68ec55347f4f](http://hi.baidu.com/syncth/item/c58bacdadd2f68ec55347f4f)，后来迁移到此处</b>

<p>按照IOI集训队ahyangyi大牛的论文,有根树的hash可以由子树的hash值递归计算得到,计算前,先对子树的hash值进行排序.论文中介绍了一种hash函数 hash[v]= (....((((a*p^hash[1])*p^hash[2])*p^hash[3]....),中间异或后每一步都取模.</p><p><a href="http://www.cnblogs.com/unber/archive/2009/08/04/1539096.html">click here to view  my code</a></p>
