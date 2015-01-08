---
title: A bug of the GCC 4.8's O2 option
layout: post
tags: ['public', 'post', 'compiler','gcc']
time: 2014-04-06 08:34
mathjax: false
---

There is a blog on Codeforces.com metioning a bug of GCC 4.8, whose link is [http://codeforces.com/blog/entry/11450](http://codeforces.com/blog/entry/11450).

In a simple word, there will be a stupid bug when executing the following code compiled with `-O2`.

<script src="https://gist.github.com/klogk/9994725.js"></script>

The expected output will be `4 3 2`, while the result is in fact `-1`. Not using `-O2` or using older version compiler, this error will not occurs.

I made an simple analysis of the code. I changed all the input and output with C's `printf` and `scanf`. The main instructions are listed below

<script src="https://gist.github.com/klogk/9994674.js"></script>

From the assembly code, the program directly checks if `n` is equal to 3, outputs `2 1 0` if yes and outputs `-1` otherwise. This optimization is totally wrong.

After a few trying, I found that if modifying the condition from `n == x + (x + 1) + (x + 2)` to `n == 3*(x+1)`, the optimized code will be:

<script src="https://gist.github.com/klogk/9994690.js"></script>

It is funny that `imull   $-1431655765, %esi, %edx` calculates `n/3`.

So the `-O2` option makes bugs when evaluating `if`'s conditional statement.

**Update:**

yeputons pointed out that we could avoid assembly analysis by using `-fdump-tree-optimized` option[http://codeforces.com/blog/entry/11450#comment-163925](http://codeforces.com/blog/entry/11450#comment-163925). This option will generate the optimized C++ style code, which is much more friendly.

 <script src="https://gist.github.com/klogk/10000867.js"></script>
