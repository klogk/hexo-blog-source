title: '[Coursera][ModelThinking][SRT] Section 4-6'
date: 2009-01-01 12:00
tags: ['Coursera', 'MOOC', 'ModelThinking']
---

﻿大家好 在本模块的最后一节课中我们来看看
所谓的 信息价值上一节课中
我们学习了如何在不确定性情况下做决定按照定义
你不知道接下来会发生什么那就是不确定性的意思
在那些模型中 我可以提这么一个问题如果我知道答案 会怎么样？
这些信息对我有多少价值？这就是运用形式化模型 形式化结构的好处之一
一旦掌握了形式结构 我们就可以计算出来
我们就真的能知道 那些信息的价值
我来举个例子 轮盘赌(Roulette)这个游戏
轮盘赌有一个转盘美国的轮盘赌转盘上有38个不同的
数字可供下注从1到36的数字 加上另外的两个点数
所以总共就是38个可供下注的数字如果你在[某个点]下注
若这是个古典概率问题假设我随便猜某个数字 我的胜率
就是1/38 我要问信息的价值是多少？
如果有人知道接下来要发生什么会怎样？此处我们有两种
不同的问题可以问 第一 我们会问如果有人说
我总是押17 17是我的幸运数字
押17点的胜率是多少？有人告诉你说 我可以
在转盘开转之前就回答你这对你有什么价值呢？
那样一条信息的价值会是多少？首先 假设我说你会输了那盘轮盘赌
如果你知道自己会输你就不会下任何注
如果你没有信息 你什么都不会赢因此你的获益是零
但这个消息对你来说值多少？假设他们告诉你 你可以赢100美元
你想 好呀这个信息很棒 它对我来说值100美元
这并不十分正确 因为只有当他告诉你你的数字会出 这才值100美元
所以 如果他说17这个数字不会出 你就不会下注
但如果他说 接下来就是要出17你下注了 你赢了
但是你只有在1/38的时间里会赢所以那个信息的价值
只是100美元除以38份这么多或者 假设有人说
我能告诉你 会赢的那个号假设 你每轮最多能赢
100美元 但此人说我可以告诉你能赢的数字
如果他们告诉你 赢得赌注的号码你就会赢到100美元
如果你赢得了100美元这个信息的价值就是100美元
所以赢得赌注的号码的价值就是100美元
知道你押的号码是否能赢钱 这个信息的价值是100美元除以38 大概就是这个意思
但现在我们想要把它用于更复杂一点的情境中
在我们有决策树之类的东西的时候我们举个例子 假设
你考虑买辆车 并且你现在就有能力买 但是你
担心将会有现金回馈活动你听到了一些传闻
说未来的一个月内 将会有现金回馈活动并且 这次现金回馈活动
将返现1,000美元我们假设你已经对
他们在过去几年中的现金回馈活动做了频率分析
得出他们有40%的概率将做现金回馈活动
这样你现在可以花500美元租一辆车 然后等待
希望将有现金回馈活动那么我们现在想确定的是
如果有人能告诉你信息 这对你来说值多少钱假设你有认识的人在汽车公司
他们说 没问题 我会告诉你是否会有现金回馈活动
但你要花钱买这个信息那么 这个信息价值是多少呢？
你愿意花多少钱来知道他们是否有现金回馈活动呢？
这就是我们要确定的问题首先 我想说
这不是一个容易的问题这对你来说值多少？
我不知道 50美元 100美元 200美元 300美元？谁知道呢 那就是我们要尝试解答的
为了确定信息的价值 我们需要做
三件事 第一 我们要计算出没有信息时的价值
假设我就是要做一个决定我的最佳选择是什么？
我怎样做出决定？第二 我要算出如果我有信息 价值是多少
我知道接下来会发生什么 我会怎么做？我的净收益是多少？接下来
第三 计算两者的差值我将得到信息时的价值减去
没有信息时的价值 得到一个差值这个值将告诉我
这个信息的价值是多少很直截了当 很容易做
只要我们有决策树模型如果没有决策树模型
就会变得非常困难 那么 我的选择是租还是买呢？
如果买 我只是支出 什么也得不到只有净值
我们把它设作基准值 如果我租车就可能有现金返还活动
也有可能没有现金返还活动我们把这个写正规一点
如果我买 我的收益是零如果我租车 要是后来没有
现金返还活动 我这个月就浪费了500美元租车但如果有
现金返还活动 我净赚500为什么是500呢？因为现金返还1000美元
减去500美元的租金 就是500美元
现金返还活动发生的概率是40%没有现金返还活动的概率就是60%
现在 我需要得出一个方案我该不该租车？
看 我将40%乘以50060% 把小数点打在这儿 乘以
-500 把它乘出来 0.4乘以500得到2000.6乘以-500得到-300
最终结果为-100如果我要租车 我就负100
我的决策树就很直观了 如果我买车 我得到0如果租车 我负100美元
我该怎么做呢？当然是买了所以 没有信息时 我要考虑到
在没有信息的情况下 在这样零收益的案例中我应该买车
我已计算过没有信息的情况
现在我要计算一下 在有信息的情况下会怎样
假设我知道接下来要发生什么那么我要画另一个决策树
这和第一棵树看起来不同因为事情将变成这样
首先 这个机会节点会被透露给我有人会告诉我
是否会有现金返还活动40%的几率他们会告诉我
是的 会有 60%的情况下他们会告诉我 不 没有
我们来思考下会发生什么如果他们告诉我 会有一个现金返还活动
那么我就会去租车 就会节省500美元如果他们告诉我 不会有现金返还活动
我就会买车 那我就的情形就和之前一样
如果我事先就有消息 我做决定就会很简单
因为一旦信息被透露 就没有不确定性了
当有信息的时候 我不再是在不确定性下做决定所以 很显然
如果会有现金返还活动 我租车 我赚500美元如果没有现金返还活动
我就买车 我就回到基准点 收益为零那么我预先知道信息价值是多少？
也就是说 我有40%的概率赚500美元
60%的概率不赔不赚 所以 信息的价值200美元在有信息时
我的期望价值是200美元 回到这里计算在没有信息时的价值 等于0
计算有信息时的价值 是200美元
计算它们的差值 是200美元你可以更清楚的看到
有信息时 200美元 没有信息时 什么都没有所以 这个信息的价值是200美元
这是一个相当简单的例子 那我们回到
我们上讲课讲的两个例子中一个是有关买火车票的
另一个是关于写论文的我们可以说 假设我们知道
接下来要发生什么 假设我们知道我们是否能赶得上火车 假设我们知道
是否会赢得奖学金 我们可以计算出那些信息的价值是多少
我们愿意花多大价钱去知道 接下来要发生什么
你只需要做同样的事 遵循同样的方法
在不确定的情况下 假设有信息 计算价值就当你知道答案
然后对比两种价值之间的差异那么 我们在这儿学到了什么？
我们学了 可以用一个专为一个目的研究出来的模型
决策树模型 我们开发它来解决如何在不确定的情况下做出决定
我们把这个模型用于别的目的我们能用它确定信息的价值
我们能计算出 我们值得付出多少去知道这个信息
知道未来会发生什么 怎样发生并且 它真的
很容易解决 就是个三步的过程第一 我们要知道
没有信息会怎么样有信息时我们怎么做
然后我们可以得出有了这些信息后我们的境况会好多少
而这就告诉我们了 信息的价值这本来 在很多情况下
是一个我们在头脑中难以解决的事但用这个简单的决策树模型
这就真的变成一件直接又简单的事了所以 我们再一次看到了模型的力量
它能帮助我们做出更好的决定谢谢大家