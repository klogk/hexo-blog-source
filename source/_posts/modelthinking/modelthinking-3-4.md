title: '[Coursera][ModelThinking][SRT] Section 3-4'
date: 2009-01-01 12:00
tags: ['Coursera', 'MOOC', 'ModelThinking']
---

﻿大家好 这一节我们将讨论“生命游戏（The Game of Life）”
这是非常简单的聚合(aggregation)模型
在介绍生命游戏之前 我们先将其放入具体的情景中给大家做个铺垫
还记得我们为什么要上这堂课吗？
其中一个原因就是成为更睿智的世界公民理解我们周边的事物
二是为了更好、更清晰地思考问题三是为了使用和理解数据
四是为了更好地设计、制定战略和决定那么我们能用生命游戏做什么？
生命游戏是一个非常简单的模型展示了事物是如何聚合的
并能给我们一些令人惊喜的结论这是一个玩具模型
它非常的简单 真的不是关于任何事的模型它无关气候变化
无关金融系统无关如何根除贫穷
它就是一个告诉我们聚合可以变得多复杂的模型
我们应该如何看待这个模型呢？就好比是钢琴的音阶(scales)之类的东西
如果你和我一样喜欢篮球的话这就像练习运球一样
这个模型能帮助我们锻炼思维
了解聚合的微妙之处
在学习了生命游戏和一维细胞自动机模型之后
你们就会为聚合过程的复杂程度而惊讶了
然后我们再去看这个包含大量聚合的世界
我们就能够更深地体会到
为什么想要通过宏观层面的现象来推断微观层面发生了什么 是那么困难
就像我们之前在“谢林(Schelling)的模型”中看见的一样
而现在我们将在生命游戏里通过一种更极端的形式 去体会这个道理
生命游戏实际上是不久前由一个数学家发明的
由剑桥大学的数学家John Conway发明
他是一个才华横溢的数学家主要研究群体理论
这个模型是他用围棋的棋盘建立的
围棋就是在矩形网格里放白色或黑色石子的游戏你可以将这些石子放置在棋盘上
生命游戏的工作原理很像谢林的模型
每个细胞(比如这个)拥有八个邻居 细胞们可以是活的或者是“活着(on)”(用黑色表示)
也可以是死的或者是“死了(off)”(颜色相反 用白色)
所以黑色表示“活着”白色表示“死了”生命游戏的规则相当简单直白
默认都处于死亡状态细胞只能在3个邻居都活着的时候活过来
因此需要身边有3个细胞都活着才能活过来所以这个现在死了的细胞不会活过来
因为它只有两个邻居是活着的
如果细胞现在活着但是只有少于两个邻居(0或1个) 活着
细胞将会因无聊而死因为这里不会发生任何事
如果有3个以上的邻居活着你会因为周边有太多人而受限制
因为他们占用了太多的资源你会死
但是如果附近只有2个或3个邻居活着那么你就可以继续活着
这些规则很简单吧 我们再总结一遍细胞可以是活的也可以是死的
如果你现在死了但是恰好有3个邻居活着就可以活过来
而如果你现在活着 只要还有2个或3个邻居活着就能继续活下去
所以死亡需要3个以上的邻居活着继续活着需要有2个或者3个邻居
我们来看这个细胞(标记为X)你能看到它有3个邻居
他们都活着这意味着下一时刻他会活过来
就是这样 再看那个细胞
在这张图里我们再来看看那个细胞会怎么样
现在这里有1个、2个、3个、4个邻居活着
所以这个细胞会死
当我们观察生命游戏的时候我们不是仅仅关注单个细胞
我们可以观察所有细胞的整体情况这里有一个初始模式
我们来看这个只有2个细胞的世界左边的这个没有活着的邻居
再看右边这个也没有活着的邻居
那么这个世界会发生什么呢?它将会以死亡结束
什么都不会发生的再来看看这个3个细胞连成一行的世界
左边的这个人有1个活着的邻居
中间的这个人有2个活着的邻居
右边的这个人有1个活着的邻居这意味着左右的2个细胞将死去
但是中间这个细胞将活下来
但是我们另外还有2个细胞需要考虑
看看这个在顶部的细胞
它有三个活着的邻居1 2 3
这个也一样  1 2 3所以这两个细胞将会活过来
我们让这个系统运行到下一个时刻我们将会看到中间的细胞仍然活着
那个细胞上下的2个细胞也活过来了
现在我们的3个细胞排成了一列
让我们再这个系统继续运行下去会发生什么呢？
像之前一样中间的细胞会继续存活
而上下的2个细胞将会死去因为它们只有一个活着的邻居
但是现在左右的2个细胞就是这一个和这一个
他们会活过来因为它们每一个都有3个活着的邻居
这就是之后会发生的事情那么再让时间继续走下去
一开始图像是这样的 但是之后它会变成那样变成那样之后  它又会变成这样
所以我们会得到一个信号灯所以说生命游戏很有意思
因为我们是从最简单的规则开始的如果你活着
并且你有2或3个邻居也活着你就能活下去
如果你死了 那么只有当恰好有3个邻居活着的时候你才能复活
我们可以看的这些微观层面的规则可以创造宏观层面的图像(比如这个闪光灯)
让我们再试试别的东西从更为复杂一点的图形开始
让我们看向这个图形从这个细胞开始数
这个细胞有2个活着的邻居这个细胞也有2个活着的邻居
这个细胞只有拥有1个 再看周围我们就会发现这个细胞有3个邻居活着
而这个细胞也有3个没有其他细胞有3个活着的邻居了
在下一阶段我们将获得这样的一幅图像
所以生命游戏不只可以创造“灭绝”和“闪光灯”它也能够拥有一个能够不断变大的系统
我们所需要做的 就是不断地尝试
然后弄明白生命游戏能够创造什么图像
让我们看一些经典案例我们将使用NetLogo软件来做这件事
我们将看三个案例图像
首先是警示灯(Beacon)它由2个方块(每个方块4个细胞)组成
然后再看这个我称作“8字形(figure eight)”的图案它由2个方块(每个方块9个细胞)组成
最后是这个我称为“F型青椒(F-pimento)”的图像它由一列三格的细胞和一个在右边的细胞
左边还有一个细胞让我们看看这三个图像在生命游戏中的变化
但是我们不用人工计算那样要花太多时间
我们用在谢林的模型中使用过的NetLogo程序
先来做“警示灯”我们需要做的就是把细胞画出来
我们要画一个“警示灯”画1 2 3 4
之后我们再画1 2 3 4现在我们可以按这个“运行一次”按钮
它先变成了这样之后又变成了那样
如果你考虑每条的规则并想出每个细胞将怎么变化 你就会知道图像会如何变化
我们会让它永久进行下去稍稍慢一点
我们就能看到这个小警示灯在不停闪烁
这和我们之前的“闪光灯”很像只不过它是上下变换
垂直、水平、垂直、水平那是个不错的小图像
现在让我们停下来让它变得更有趣一点
画上更多的细胞让它变成3*3大小的方块
现在这些都是3*3的方块了
我们来看看会发生什么 再次重申每个细胞都遵从生命游戏的那些规则
那么我们让它运行一次、两次、三次四次、五次、六次、七次、八次
是不是很不可思议？
它看起来像个8如果你把头斜着看一下
它看起来就像个8这种情况就是这个图像的奇妙之处
1、2、3、4、5、6、7、8生命游戏的魅力就在于
非常简单的结构能创造出这些精细的图像而且每个细胞只服从自身的简单规则
我们能从中学到
当遵循着简单规则的简单图像聚合在一起时可以形成非常复杂的图像
好了这就是“8字形”的变化
让我们再来试试“F型青椒” 记住它有一列三格的细胞 就像这样
中间还有一个一个在左边一个在右边
让我们慢慢地运行程序1、2、3、4、5、6、7、8、9
它就像是获得了生命一样我们让它一直运行下去
你就能看到它在产生一些看起来像小滑翔机一样的东西
它在产生一些能够进行空间移动的东西
这些东西几乎就像是活的一样你可以开始思考一些非常有意思的事情
想想人类的大脑
人脑的神经元遵从简单规则而通过遵从这些规则
神经以某种方式进行连接从而创造出全新的模式
这就诞生了记忆、思维、认知、个性等东西
生命游戏显然不能用来解释认知之类的东西
但是它向我们表明了
遵循简单规则的简单事物能够创造出难以置信的复杂模式
因为我们从…让我们重新来一次
我们从非常简单的图像开始我们有排成一列的三个细胞
顶上有一个 还有一个在左边当我没点击一次这个图像就向外展开一点
我们所能看到了非常复杂的变换模式
让程序自己运行下去你可以看到这些有意思的东西
里面这些图像在平面上“滑翔”
这里我们有一组“滑翔机”图像这是零时刻
从这一行开始看我们就能知道下一时刻会发生什么
当然你也可以根据每个图片中的每个细胞自己判断接下来会发生什么
我们来看这个细胞就是这个
它有一、二、三个邻居所以它下一刻会活过来
我们接着往下看这就是接下来会发生的事情
在T等于1时是这样的在T等于2时是这样
因为之前活过来的细胞只有1个活着的邻居所以它将死去
我们再接着看T等于3和4的时候
你发现到T等于4的图像看起来和T等于0(老师口误)时一样
只不过它又向右下角移了一格
所以如果我以这种设置开始它将划过这个空间
这其实是一个我们称为的“浮现(emergence)”或是“自组织(self-organized)”的模式
因为它看起来像是自己在移动如果你从这个起始时刻开始播放
你会看到有东西在平面上划动
你可能以为它在飞但它并不是在飞
但是其实每个细胞仅仅是在遵从一个特定的规则而已 所以生命游戏很好玩
我们建立模型的原因之一是为了理解结果的种类
那么生命游戏让我们得到了什么？我们得到了固定不变的点阵吗？
整个系统始终出现同一种图像吗？它不停地闪烁？
这些结果我们都在生命游戏中看到了这个模型是完全随机的吗？
就像下面这个图像一样这些复杂的模式图像是怎么来的呢？
有趣的是：这四种结果都会出现在生命游戏中
我们已经看到过其中的三个了我们看到过所有细胞都死去
还有“闪光灯”和非常复杂的图像你也可以把它当作是完全随机的
你也能用它生成随机数
在非常简单规则约束下能聚和成这么复杂的图像 很有趣
这也是个有趣的宏观现象 你可能想问：有没有什么图像是它不能做出来的？
答案是：几乎没有
任何你能用电脑做的事都能在生命游戏中完成这是一件非常神奇的事
这是一件美妙的事这里有一种特殊的细胞布局
想自己尝试的话可以在Netlogo之中操作不过画这些细胞要花上一点时间
这是一个滑翔机发射器它每隔一段时间就会发射一架滑翔机
一般是朝右下方发射 最终你会看到一个信号(像心跳一样的脉冲图像)
不停地发射出滑翔机 非常有趣
每个细胞只是各自遵从同样的规则而已
但是我们却得到了非常精妙的图形
那么我们从生命游戏中学到了什么？很多东西
1、我们得到了自组织模型
没有人设计过这些图像这些滑翔机、闪光灯和滑翔机发射器
没人设计过这些图像
这些只是每个细胞都遵循规则的结果
当把细胞摆成特定图形时它们就会产出特定的图像
这些图像是自发形成的2、我们得到了“浮现”模式
浮现意味着这些图像有某种功能
比如滑翔机、滑翔机发射器、计数器你可以用生命游戏做一个计数器
如果你给这些细胞赋予特殊意义或数值你也可以用它们来进行计算
所以当这些图案具有功能时我们能将其它视作“浮现”
你可以认为意识和认知也是一种“浮现”现象
生命的游戏能够产生这两种模式
我们可以认为有些模式是拥有功能的
生命游戏的另一个奇妙之处是：它能帮助我们理清逻辑
要是没有使用模型又不借助计算机来计算
我们永远无法理解到底在发生什么事情
我们也已经看到了如何从简单的图形获得很复杂的图形
在你的逻辑中你可能没想到会有这样的事
我在这节课刚开始的时候就说过这些规则很简单
我相信你也觉得这些规则很无聊只是一堆规则和一个棋盘而已
但是我们在生命游戏中看到了这些神奇的东西
你开始意识到：简单的规则能创造出难以置信的现象
如果不建立模型 你可能就不会知道
这就是生命游戏
它是细胞自动机模型的一种
它只是一种细胞自动机模型
下一讲我们会介绍所有种类的细胞自动机模型但是在形式上要更简单些(是一维的)
从而帮助我们理解这个系统为什么这么神奇
为什么这个系统能形成均衡？为什么它会有复杂的结果？
我们会介绍所有类型的细胞自动机模型让大家至少能对这些问题有一些理解
谢谢大家