title: '[Coursera][ModelThinking][SRT] Section 5-1'
date: 2009-01-01 12:00
tags: ['Coursera', 'MOOC', 'ModelThinking']
---

大家好 这节课我们来讨论一下如何为人建模
因为很多模型都会涉及到我们
涉及到人或一群人的模型 譬如公司 政府 机构
要为这些对象建立好的模型
就必须对其中的组成部分——人——建立好的模型 而为人建模可不简单
物理学家默里·盖尔曼（Murray Gell-Mann）曾说过一句很有名的话：  
“想象一下，如果电子能够思考的话，那么物理学该有多难呀！” 
他的意思是说 如果考察电子 或者是碳原子抑或是水分子
它们都不会思考 不会感知世界
也不会有任何动机或目标 更谈不上信念什么的
因此为这些东西的运作而建模是件很直截了当的事情
而人可就复杂得多了 不是吗？我们有意图 有动机 有目标
我们有我们想做的事情 有信念体系 还挺乱的
因为这些全部的原因 我们并不清楚我们会做什么
这还不算完 我们是彼此不同的 我们想要的东西不同 我们的动机和目标也不同
而这些有意图 会思考 又彼此不同的个体组合在一起
就意味着想弄清楚他们要做什么和怎么做是件非常困难的事情
那我们怎么办呢？下面我们来看看三个基础框架
第一个框架称为“理性行为者模型”（rational actor model）
它假定人们的行为是寻求最优的 这当然不现实 下节课我会更多地谈谈这点 
不过 这是一个不错的基准
就让我们从这个假设入手 假设人们的行为是有目标的
并且会优化他们的目标 第二个框架称为“行为模型”（behavioral model）
在这里我们需要收集真实的人们做决策和采取行动的数据
然后尽可能接近地建立起
描述人们真实行为的模型
当然你不能弄得太复杂 我们会包含一、两个完美理性假设下没有的因素
譬如 人们可能有的倾向或偏见
第三个框架更简单
它们是 “规则模型”（rule based model）
我们不会去深入挖掘人的心理 而是假设人们会遵循某些规则
然后来研究这些规则作用下的结果
在一些情况下 什么是我们假设最重要的三件事
在另一些情况下 什么是我们认为无足轻重的三件事
我们如何为人建模 准确与否
与我们所使用的模型密切相关
现在 我们先看看理性行为者模型的原理
在理性行为者模型中 我们假设存在一个目标函数
它是一个被试图最大化的数学函数
譬如 如果这代表一个人，这可能会最大化他的幸福值或是个人价值
如果这代表一家公司，可能是最大化公司的利润或市场份额
又或者是你在竞选一个政府职位 这就是会最大化你的选票数
你所做的假设是 人们是寻求最优解的：给定目标 你会做最优的事
你会做出让你感到最开心的选择
你会做出让你获得更多选票的政治决策
你会生产那些最能让你赚钱的产品
让我们更具体一点 假设你在思考 一个人应该选择工作几个小时？
你要做的，是写下一个函数——效用函数（utility function）
效用取决于消费和闲暇
这个函数可以这样写：
消费的平方根乘以闲暇的平方根 为什么是这个样子呢？
我们知道 平方根函数的初始斜率比较大 之后就变得比较平缓
这就意味着 刚开始消费的效用很高 之后就越来越低
休息也是一样：第一个小时非常愉快
但一周过后 你恐怕已经迫不及待要返回工作了 所以休息的效用也是下降的
它们都具有所谓的“收益递减”（diminishing returns）特点
因此 这个函数是说 消费是好的 但时间长了就不那么好了
休息也是好的 但时间长了也没那么好了 这就是你的函数
而你现在要做的 是根据消费和休息的成本来决定工作和休息的时长
也即 最大化效用函数 你可能不会真的这么做
比如坐在家里写下什么函数 然后去解什么方程
但经济学家们假定你就是这么做的
或者说 这是近似于你所做的
理性行为者模型受到了很多质疑
特别是与一些基本数据不符 因此 经济学中发生了一场长达百年之久的 
称之为"行为主义革命"（behavioral revolution）的运动
心理学中也在发生类似的事情
它假定人们的行为是非理性的
如果观察人们的行为举止
你会发现他们不是理性的 而且这种非理性是系统化的
最近 神经科学的发展提供了支持这种学说的证据
你可以亲眼观察大脑结构
观察人们在特定条件下如何思考
你可以观察到 实际上人们会按照“理性行为者模型”所认为的非理性方式进行思考
这样 我们就有了两个基准：
一方面我们假定人们是理性的
另一方面又假定人们按照人的方式去做事
而这种所谓“人”的方式可就复杂多了
而第三个办法也来自于社会科学
还有计算机科学以及一些心理学
它假定人们遵循一些规则 它更像是谢林模型（Schelling Model）
我们并没有一个描述人们行为的精确模型 我们仅需要假定人们会搬离一个社区——
如果邻里街坊们与他们不是同类人
这是一个很简单的规则 如果这个规则与人们的行为很接近的话
那这个模型也许够用
我们现在有了三个基本框架：人们会最优化；
人们会按『人』的方式做事；人们遵循规则
在给定条件下 这三个模型对于人们行为所做出的预测会有所不同
而当我们把这三个框架结合在一起时
会得到各种迥异的结论
在某些情况下 我们的假设无足轻重
在接下来的几堂课里 
我们将深入思考理性行为者模型背后的逻辑
聊聊几个心理学家们所观察到的人们行为的倾向性
然后了解一下基于规则的模型
然后通过在一些设定下比较这几个模型的结果
来看看什么情况下这些假设很关键 什么情况下则无所谓
谢谢！