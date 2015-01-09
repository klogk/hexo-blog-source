title: '[Coursera][ModelThinking][SRT] Section 2-1'
date: 2009-01-01 12:00
tags: ['Coursera', 'MOOC', 'ModelThinking']
---

﻿大家好 在接下来的课程里 我们要了解一系列模型 它们可以帮助
我们理解一种经验现象 这个经验现象是：
如果你观察这个世界 你会发现成群在一起交往的人
往往看起来相似 想法相似 行为相似 所以我们
想弄清楚为什么是这样 首先 让我先解释一下
我是什么意思 如果你看看像底特律这样的城市 这是底特律的人口调查图
你看到的每个蓝色的点代表一个非洲裔美国人居住的
居住的街区 这类街区、人口普查区域里 居住的主要
是非洲裔美国人 红点是大部分为白种人的街区
你在底特律这座城市看到什么 难以置信的种族隔离 这显示
人们实际选择跟外形与自己相像的人住在一起 但
不止存在这类分类效应 人们与常在一起的人从外貌到举止都相似 还有另一个原因
我们改变自己的行为
我们调整自己的行为以适应我们周围的人
比如吸烟 可能你不吸烟 但你开始常与一群吸烟的人外出游逛
所以你可能偶尔也来上一支 相反
你可能一生都是个烟鬼 但现在你跟一群不吸烟的人在一起
所以你说 “你知道吗？我准备戒烟了 “
所以 如果这两种力量 其中一个 产生分类的效果
或者像社会学家说的：同质性  你知道 我们往往选择跟我们相似的人在一起
而另一种效应是 我们选择
在行为上、信念上模仿跟我们常在一起的人 这两个因素
都会一群人看起来彼此很像 好的 我们想做的是
在某种程度上理解这类过程是怎么实现的
方式通过一些简单的模型 现在 这些现象可能看起来相当明显
但当我们构建模型之后 我们会发现一些
非常有趣的、出乎意料的结果 好 让我们开始吧
这些模型是什么样的？本节讲座如何运用模型？
我们先介绍一位著名的模型设计者
托马斯·谢林  这里是一个种族隔离的模型 有时
它也叫做”谢林倾斜模型“ 这个模型会让我们看到
导致底特律隔离模式的原因比我们认为的更微妙
之后 我们将看到一个由马克·格兰诺维特设计的模型
他的目标是观察人们参与某些集体行为的意愿
这些行为可能包括骚乱 政治起义
和社会活动等 这是一个非常、非常简单的模型
之后 我们要把格兰诺维特的模型进一步延伸 成为一个我称之为”起立鼓掌“的模型
这个模型是我和我的朋友约翰·米勒为了好玩设计的
但它抓到一个要点 这是一个同群效应模型
体现你如何改变行为适应周围的人 这个”起立鼓掌“模型有趣的地方在于
它提供给我们一个非常好的框架
在其中可以思考同群效应的问题 我们会再次看到一些出乎意料的结果
是的 最后 在我们研究完这些模型之后
我们要聊一聊”识别问题“
假设 我们观察一群人 他们全部很相似
这里的问题是 他们是分类吗？
我的意思是 他们是否因为相似所以选择彼此交往？或者这里体现的是某种同群效应？
他们彼此交往...他们的外形、言谈、举止全都一样吗？
这是一个有趣的问题 值得探索 这几个模型能帮我们在一定程度上理解
怎么区分这两类情况 OK 让我们开始吧！
在开始之前 我们先简单评论一下我们要使用的模型
很多时候 但人们想到模型就会想到以方程为基础的模型
所以 我教这门课之前
当我教本科生时 他们中的一些人关心的一件事是分数
不是所有人 但很多人都关心分数 我要对他们说
我们有一个以方程为基础的模型 用于为你评分 它开起来有点像这样
你期末考试的分数是50+你学习时间的五倍
如果你根本不学习 你就没有投入学习时间
你可能在考试时只得50分 这门课程不及格
如果你为考试投入十个小时 你知道该为考试学习 你可能
考试得个A 这门课程得A
这是一个线性模型 可以部分解释这个世界怎么基于等式运作
在本单元中 我们要学习的模型不是线性模型
它们被称为基于代理人模型(agent-based models) 基于代理人模型是什么？
基于代理人模型的运作原理如下 你有一大把智能体 他们可能是人、公司
可能是国家、组织 但他们都是代理人
都是这个模型的对象 这些代理人都有行为 就是他们所做的事 他们遵守的规则
有些规则是最优化规则 它们可能已经尽可能完善
这时它就成为我们说的”博弈模型" 或理性选择模式
在这类模型的环境里 个体从事最优化的活动
在我们学习的模型中 它们不会尽量优化
它们将遵循相当简单的规则 模型的第三方
一旦你让所有代理人遵守所有这些规则
就会在宏观层面创造出一些情况 产生一些结果
我们能做的就是探索 我们会得到什么样的结果
我们能在这些模型中发现的是 这些结果是令人惊奇的
这再次体现了模型的用处 因为我们按逻辑思考可以以为
如果我们假设中介遵守行为规范 就会得到确定的结果 但当我们利用模型推导
你会发现 通过所有我们发现的逻辑的运作
我们实际可能得到相反的结果 或者令人惊奇的结果
好 这就是我们的计划 我们要观察几个分类模型
还要观察几个同群效应的模型
我们还要学习两者的区别和一点相似性 就是这样
谢谢你们