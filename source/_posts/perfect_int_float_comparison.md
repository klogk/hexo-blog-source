---
title: "[译文]int==float的完美实现"
layout: post
tags: ['public', 'post', 'funny']
time: 2014-04-29 08:34
mathjax: true
---

这篇文章翻译自 [The perfect int == float comparison](http://gynvael.coldwind.pl/?id=535)

首先明确一下，这篇文章不是关于如何正确比较两个浮点值，而是如何精确比较一个浮点数和一个整数，也会谈到为什么在一些语言(C, C++, PHP等)中的`int_value == float_value` 会出现错误。这个问题是我最近修改某个库的代码中遇到的。

## 问题解释

首先我们来执行下面的代码，在整型和浮点数之间做比较，将会遇到一个问题。

<script src="https://gist.github.com/klogk/11373752.js"></script>

运行的结果将会是

<script src="https://gist.github.com/klogk/11373769.js"></script>

`99999999`和`100000004`竟然都"等于"`100000000`，根据我们的常识和算术知识这是很荒谬的。但很不幸，在浮点运算中的的确确会出现这样的问题。

我们再来看另外一个例子，在PHP中对一些数值做排序

<script src="https://gist.github.com/klogk/11373786.js"></script>

在64位的PHP下排序的结果是

<script src="https://gist.github.com/klogk/11373814.js"></script>

(注意，必须是64位的PHP，32位的PHP限制了整数是32位，将会把超过范围的整数转换为double)

为什么会出现这样的情况呢？

这都要归结于对于大整数表示成float的时候精度很低(可以参考[这里](http://en.wikipedia.org/wiki/Single-precision_floating-point_format#IEEE_754_single-precision_binary_floating-point_format:_binary32)和[这里](http://en.wikipedia.org/wiki/Double-precision_floating-point_format))。例如32位的浮点数只有23位用于表示有效数字。这就意味着如果一个整数值转换成float需要24位及更多的比特位(注意首位的1是固定省略的)，它就会被截断，也就是说末尾的有效数字会被当做是0。

在上面的C代码中，十进制的`100000001`实际需要27个bit来正确表示:

```
0b101111101011110000100000<del>001</del>
```

由于只有首位的1和后面的23位能够放入到float中，最末尾的1就被截断了。因而，这个数实际就变成了另外的一个数：

```
0b101111101011110000100000<strong>000</strong>
```

转换成十进制就是100000000，所以就被认为等于float常量100000000.0f。

同样的问题也可能会存在于64位整数和64位浮点数，后者只有52位用于存储有效数字。

实际写代码的时候，情况或许会更好一些。我们把第一个C代码用循环重写：

<script src="https://gist.github.com/klogk/11373826.js"></script>

正如看到的，好像没有语义上的本质区别。但编译运行之后却得到如下的结果。

<script src="https://gist.github.com/klogk/11373843.js"></script>

结果竟然惊奇的正确了。但是如果我们加上编译优化选项呢？

<script src="https://gist.github.com/klogk/11373852.js"></script>

为什么会这样？两种情况，编译器都需要把整数转换成浮点数，然后和第二个浮点数做比较。但这一过程可以用两种不同的方式来完成：

1. 把整数转换成浮点数，然后作为32位的float存放到内存中，然后再载入浮点单元(FPU)做比较。如果是整数常量，还可以在编译的时候把整数常量转换为32位float，然后在运行时载入到FPU做比较。

2. 把整数直接载入FPU做比较。

这里的区别在于FPU内部处理大的浮点值的时候会有更高的精度(默认是80位，虽然你可以修改它)所以32位的整数在加载的时候并不会发生截断，而是在转换为32位float的时候(只有实际的24位精度)。

采用哪一种策略，就取决于编译器了————看编译器的心情，版本，编译选项等等。

## 完美的比较

当然，事实上是可以做一个完美的比较的。

最简单最直接的方法就是比较之前把int和float都转换成double。double有足够的有效位来存储所有的32位int值。对于64位整数，你可以使用80位的double，恰好有64位用于存储值。

但这太容易了。我们试试不做类型转换来做比较。

这可以用两种方式来做：数学的方法或者编码相关的方法。下面对两种方法都做了讨论。

## 数学方法

基本的想法是反过来做，也就是说，把float转成整数。有一系列的问题我们需要处理：

1. float的值可能比`INT_MAX`大或者比`INT_MIN`小。那就会发生[这样的问题](http://gynvael.coldwind.pl/n/float2int_overflow)，我们需要处理这种情况。

2. float值的十进制可能有一个非零的小数部分，将会导致转换为int的时候发生截断(例如，(int)1.1f等于1)，我们要避免这种情况。

这种方法的实现代码如下

<script src="https://gist.github.com/klogk/11373872.js"></script>

## 基于编码的方法

这种方法根据对float值比特表示的解码，检查是否它是一个整数，是否在范围内，最后和整数值做比较。我直接给出了代码。如果有疑问，可以参考[这个wiki页面](http://en.wikipedia.org/wiki/Single-precision_floating-point_format#IEEE_754_single-precision_binary_floating-point_format:_binary32)

<script src="https://gist.github.com/klogk/11373883.js"></script>

## 总结

上面的代码可以用于完美的比较，而且都能正确工作(至少在little endian x86架构上)。在此之上做一点补充，修改一下Comparator，就可以解决PHP排序例子中小于号的问题。

但是，说真的，还是直接把整数和float转换成更高精度的数吧。

P.S. 你是否知道只有`75,497,471`个正整数可以精确的用float来表示，而不是`2,147,483,647`?
