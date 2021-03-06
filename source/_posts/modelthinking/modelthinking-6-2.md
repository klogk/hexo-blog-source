title: '[Coursera][ModelThinking][SRT] Section 6-2'
date: 2009-01-01 12:00
tags: ['Coursera', 'MOOC', 'ModelThinking']
---

大家好 在这次的讲座中 我们来讨论一类非常简单的模型 
它们能帮助我们理解数据 名为分类模型
在一个分类模型里 你要把现实放到各个类别之下

以便能更好理解这些数据
它们会对数据的有些偏差作出解释
首先我想描述分类模型是什么样的然后再讨论它们如何帮助我们理解数据
让我来举个例子 很久以前
十年前我出席了Amazon公司的一次会议
他们是个把任何东西都可以摆到网上卖的公司 那时才刚上市
于是就有一次讨论 关于Amazon是否值得投资
有个华尔街投资人说 我觉得完全不值得投资
因为你想想Amazon不过是个快递公司就等于他们有个大仓库
你订东西 它送东西这个产业的利润是很小的
快递行业已经有UPS和EPX了 有UPS 有FedEX 还有DHL等等等等
我可不觉得能赚到钱 这时另一人说 
你知道吗 我要把Amazon放到一个非常不同的盒子里
我要把它放到一个名叫“信息”的盒子里
因为我认为它是新信息经济的一部分 他们会收集有关消费者需求的一切信息
所有信息都会被集中处理这会值一大笔钱
所以说如果你把Amazon归到名为“信息”的盒子里
你很可能会对它进行投资这样你就能赚一大笔钱
如果你把Amazon放到名叫“运输”的盒子里你就不会投资 也就赚不到钱
所以选择哪个盒子反映出你怎样对事物分类的
将会影响你对这些事物的思考 还会影响你所做出的决定
这就像我一个心理学家朋友说过的一句话
为了生活 必须把东西捏成团我朋友的意思是
为了理解世界 我们创造了这些团块、盒子、各种分类

我看到街上有一辆车我不会说 哦那好像是
一台1997福特F150小卡车 我只会说那是辆卡车 或者那是辆车
又或者我看到一件家具我只会说那是个梳妆台

我不会说那是1874年造的齐本德尔梳妆台我不会把事物分得一清二楚
我只会将事物分门别类这些都是为了便捷
它们帮助我们理解世界再想想我们建立模型的原因
原因之一就是用模型帮助我们做出决定、制定策略、进行设计
所以把东西混在一起有助于我们更快作出决定
我们将事物分类说这一件我喜欢 这一件我不喜欢
这一件有风险 这一件没风险让我举几个例子
好玩的例子首先假设你是个小孩 
你要决定吃什么 不吃什么
也许你会使用绿色分类法
可以是任何绿色的东西西兰花是绿色的
蚱蜢是绿的 芦笋也是绿的这些都是绿的 
至于其他东西 香蕉是黄的 糖棒是棕色的 橙子是橙色的
梨子也有绿的 但我们就假设是黄色的吧
草莓是红色的 这些都不是绿的
所以你可以定规矩说 我只吃非绿色的东西不吃任何绿色的东西
这个规矩就让你避开了蚱蜢和芦笋之类的东西
这是个你应该会遵守的规则但它并非理想
因为你可能会遇上绿色的梨子而绿色梨子又是你喜欢吃的

可如果你决心不吃任何绿色的东西你可能会决定
还是别冒这个险 这也是个简单规则的例子
现在看看怎样利用类似这样的规则去理解数据
假设我得到一堆数据各种不同的食物
这个表格右边代表卡路里
标明每种食物都有多少卡路里而我要做的就是
试图搞清楚为什么有些东西所含卡路里高有些则不高
于是我便得到了这个清单首先要做的就是
我需要知道这些数据的偏差值有多大
为了知道有多少偏差值首先要找出平均值是多少
偏差值就能告诉我们这些数据偏离平均值多少
把这些都加起来100+250=350，440，550，900
900除以5 所以平均值就是180
所以这组里每样东西平均有180卡路里
有些东西更高 这个有350有些东西更低 这个才90
我想知道这些数据里有多少偏差
方法之一就是把平均值从所有东西中扣除
用100减去180就是-80250-180=70 90-180=-90
110-180=-70 350-180=170
所以我再把它们加起来
最会就会是0 因为它等于平均值
我需要所有差值都是正数方法之一就是取绝对值
所有对象的绝对值 然后对所有绝对值求和
80+70=150 150+90=240 240+70=310
310+170=480 所以与平均值的差值总和为480
就像我们在统计学里的那样 我想用一个不同的方法 
我们实际上在更倾向使用方差我们对它平方的原因有两个 
一个是这样可以使所有的数据都是正的 就像它一贯所做的
另一个原因就是它会放大偏差 
因为我们实际上想做的是避开那些大的偏差 这样会放大这些大的偏差值
我们看看梨子的数据 用100减去180 就得到80
平方以后就是6400 这就是方差的大小 
也就是梨子与平均数平方的差别
如果是蛋糕 我会得到250-180=70 对它作平方
就会得到4900 现在我可以对所有的数作这种计算
那么对于梨来说 我得到6400 对于蛋糕来说 我得到4900
对于苹果来说 我得到8100 香蕉是4900 饼是28900 
这就是离平均数很远 如果你平方了就会产生巨大的影响
所以平方可以使大错误放得更大现在如果我把这些数都加起来
我会得到53200 这也就是我们所说的总方差
我把这些数据画出来  这告诉我这个数据有多少方差
我想要做的是把数据分成不同的类型来减少方差
这样能某种程度解释为什么有高有低 
所以明显的分类是什么这里明显的分类是
梨子、苹果和香蕉是水果 蛋糕和饼是甜点
所以我们有水果类别和甜点类别 
在水果里我得到一个是90 一个是100 一个是110
在甜点里 我得到一个是250 一个是350
让我们看得更细些 我有90，100，110 平均值是100
总方差是多少
90减去100是10 所以我将其平方得到100 100减去100得到0
如果我平方得到0 这里110减去100还是10 平方得到100
这里总方差是100+100 也即200 
现在我得到了均值100和总方差200
如果我看这边的甜点 平均值是300总方差是多少呢
蛋糕是250-300 得到50再平方 得到2500
对于饼是350-300 也得到50再平方 得到2500
把它们加起来 我得到5000 我们把它整理一下
我想做的是要产生两个类别 一个水果类别 
一个甜点类别 现在我有一个水果的均值是100和总方差200 
甜点类别的均值300和总方差5000
现在我们想想我是怎么开始的当所有的东西都在一堆时 
我得到一个180的均值 我得到一个方差53200 现在看看我的方差降下来多少
从53000到5000 就是这样
这些类别可以把方差显著的降低下来
所以把这些方差当作没能解释的 一开始我说
一共有180卡路里的均值和53000的方差是没有解释的
现在我说 等一下 我将会产生一个分类模型
一个水果类和甜点类 水果类比甜点有更少的卡路里
你说 好像是这样 水果有100的均值 甜点有300的均值
水果的方差只有200而甜点的方差有5000 
所以我把方差减少了很多 
我们想要的是一个正式的降低方差的方法 那实际上很简单
一共有5300的方差 水果是200 甜点是5000
所以总和是5200 从开始的53000最后我得到了5200
我们想问我们到底解释了多少 这才是关键
我到底解释了多少离散性 我以53200开始
现在我剩5200 所以我解释的是53000减去5000
是48000除以53200 所以我解释的百分比是48000除以53000
是一个巨大的数字 
我可以把这个写得更简单些 1减去我剩下的量
1减去5200与53000的商因为这是更简单的一个方法
所以当我得到我解释了90%的差异
90.2% 所以这是我解释了多少的方差
这等于48000 除以53200我解释的方差量
它正式的名字叫做R平方
它表示我通过那个简单的分类解释的方差的百分比
所以R平方接近1 那就是说我解释了差不多整个方差
所以这个模型可以解释很多 如果R平方接近0
那就意味着我其实没有解释方差模型并没有解释多少 
模型越好 R平方越大
但是有时数据可能有很大的变化 
即使一个很好的模型 也只能得到大概5%或10%的R平方 
也会有这样的情况 你想解释的情况很好理解
一个好的模型这时就应该给你接近90%的R平方 所以没有固定的规则
R平方是否足够好 这取决于数据是怎样的
但是对于模型类型或者某种数据类型
你大概可以根据经验知道这是好的模型 那是不好的模型
让我们再进一步 我们有水果和甜点
这是两个类别 但是如果我有
一整厨房的食物 我可能会想要有更多的类别
所以我有蔬菜类、谷物类
然后我可以把所有的东西放到4个盒子里去 
专家和非专家之间的一个区别是专家倾向于更多的盒子 
他们一般会把东西放到正确的盒子里去 他们更可能有有用的盒子
所以如果你想在预测事情或理解世界方面变得更出色
你需要的是很多的类别 你需要那些类别是正确的类别
它们能够解释很多的这种方差
我们可以测量你的模型解释了多少方差用R平方 
最后一点 即使你解释了很多方差
也不一定意味这你有一个好模型 让我们回到学校的例子
假设我想找到什么成就一个好的学校 
什么导致好的学校的成就 我会试各种的盒子
我看到有学校花费很多的钱 有些学校不怎么花钱
学校有小的班级的和大的班级的 大的学校和小的学校
没有哪个似乎能够解释学校间的差距
然后我建了一个盒子 叫做马术盒子
我把所有有马术队的学校放在这里 然后我发现 天啊
每个有马术队的学校都很棒 而实际上
这并不意味着马术队就让学校更好 
所以统计学家会区分相关性和因果关系 
即是马术队和好学校间有统计上的关系呢（相关性）
还是马术队让学校变好（因果关系） 
当我们画图时 你想把它放在盒子里 比如这个盒子里都是一堆好的结果
这个盒子差不多都是坏的结果
这并不一定意味着这个盒子如果是马术队盒子
是学校好的原因可以是其他的原因
所以为什么你要有一个马术队呢
你不会有一个马术队除非你很有钱 或者只有有很多父母的参与你才可能有马术队
等等类似的情况例如社区的大力支持 
你没有足够的空地也不可能有马术队
所以你有一个马术队可以是因为
有钱、父母参与、空地
这些确实能够让学校变好的东西 所以即使你的盒子有用
并不会保证他们确实是原因 
我们学了什么？你可以有的最简单的模型是分类模型 
你可以把事物分成不同的类别然后根据数据的类型把它们装进不同的盒子
所以可以有信息公司和快递公司 
可以是水果和甜点通过产生这些盒子
我们可以减少数据产生的偏差

所以有一个总方差 就是世界中还没有解释的偏差
通过把它们放到盒子里你可以减少方差
这减少的方差叫做R平方那是解释了的方差占所有方差的百分比
你解释了越多的方差说明你的分类越好
当然 如果你产生更多的盒子你能解释更多的方差
我们接下来要讲的是 如果你有线性模型那就可以为每个因变量x值产生一个盒子
好的 谢谢