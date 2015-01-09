title: '[Coursera][ModelThinking][SRT] Section 3-6'
date: 2009-01-01 12:00
tags: ['Coursera', 'MOOC', 'ModelThinking']
---

﻿大家好 在有关聚合的最后一讲里我们来谈谈偏好的聚合
这将会和以往我们看到的内容有所不同
回忆一下 我们讲中心极限定理时我们看到的是数字或行为的聚合
我们讲生命游戏和细胞自动机时我们看到的是规则的聚合
现在我们来谈谈偏好的聚合
偏好将会有一种不同的结构
一种和规则与数字不同的数学结构
为了了解怎样聚合偏好首先我们需要了解什么是偏好
我们是怎样表示偏好的？让我们思考一下
假如我问你：你偏好什么？
你是更喜欢苹果呢还是香蕉呢？你可能会说你更喜欢苹果
而另外一个人可能会说 不 我更喜欢香蕉又或者 我可以问
那么香蕉和椰子呢？你是更喜欢香蕉还是椰子？
你可能回答你更喜欢香蕉
由此可知其中一种记录偏好或考虑偏好问题的方法就是像这样逐个比较
我们可以给人们一系列选择问他们更喜欢哪个
当考虑到总体偏好时
我们可以列出于某人偏好的完整列表
接下来我们将多次谈到的东西与一个叫做“偏好顺序”的概念有关
它是一种对可供选择的选项之间的排序通常而言 这些选项同属一个类别
所以我可能有一个关于水果的偏好顺序
也可能有一个关于蔬菜的偏好顺序
还可以是有关于房子的或车的偏好顺序我可以对同一个类内的不同的东西进行排序
接着我们会问：有多少种偏好顺序呢？
偏好顺序是什么样的呢？
让我们假设现在有三样东西：苹果、香蕉和椰子
对于苹果和椰子 有两种可能性
要么我更喜欢苹果在这儿我画一个大于号来表示
要么我更喜欢香蕉所以这儿有两种可能性
如果换成香蕉和椰子的话我可能更喜欢香蕉
或者我更喜欢椰子所以这儿也是有两种可能性
最后当比较苹果和椰子时我可能更喜欢苹果
或者更喜欢椰子所以这儿又是两种可能性
2 × 2 × 2 = 8
所以现在有八种不同的可能性对于这三种水果可以有八种不同的偏好类型
现在有许多不同的可能性
每一种我都可以由一个大于号来表示
即表示我更喜欢哪种水果我偏好的是哪一种水果
这里有一点小问题让我把这些先擦掉一会儿
这儿有一点小问题让我们看看这些特定的偏好
这些偏好告诉我们我喜欢苹果多过香蕉
喜欢香蕉多过椰子以及喜欢椰子多过苹果
这是不成立的 因为如果我喜欢苹果多过香蕉又喜欢香蕉又多过椰子
那么我应该喜欢苹果多过椰子所以这样是不成立的
正确的应该是这样的这一特性我们叫作偏好传递
所以偏好满足“传递性” 它是可传递的
我们通常假定人们的偏好是可传递的
另一种考虑偏好传递的方式是人是理性的
因此如果说 哦 我喜欢苹果多过香蕉
喜欢香蕉多过椰子 但是喜欢椰子又多过苹果那么这将是不符合理性的
这是绝不可能的 因而我们认为理性偏好作为一种偏好具有传递性
如果我喜欢A超过B 喜欢B又超过C那么我喜欢A多过C
然后就有了一个疑问：这是不是真的呢？
假定苹果大于香蕉 香蕉大于椰子如果这意味着苹果一定大过椰子
那么我可能拥有的偏好数量就有了限制
不是任何一种可能性都是可能的有一些可能性是不可能的 现在我们有了疑问：
这种情况下我可以有多少种偏好可能性呢？实际上只要通过很简单的计算我们就解决这个问题
之前我们也做过类似的计算这意味着将出现一种我最喜欢的水果
它将排在第一 还有一种我第二喜欢的水果
然后是第三喜欢的现在有多少不同的可能性了呢？
我最喜欢的可能是苹果 也可能喜欢香蕉或者是椰子
现在有三种可能性 我选择苹果
一旦我第一种选择了苹果第二种我就只有两种选择：香蕉或椰子
我选择了香蕉 但我本可以两者之中的任何一种
当我选择第三种水果时 我就只剩下一个选项了所以共有3 × 2 × 1 = 6种可能性
针对有三个选项的情况有六种符合理性的偏好可能性
所以当我们考虑理性偏好时
我们要考虑到偏好顺序：哪一种最先 然后是其次 再其次
在一个更为复杂的模型里我们允许相等关系的存在
我可以说对香蕉和椰子的喜欢程度相同
但在这里我们假设你喜欢其中一样胜过另一样
针对这些偏好 我们首先要考虑到的是
如果在偏好中引进理性假设
那么实际得到的偏好可能性会比没有理性假设时要少
现在让我们来玩个游戏
在这个特殊模型里 我们假设存在一群有理性偏好的人
我想要问的问题是他们的偏好应该怎样聚合
思考一下：
每一个人都有偏好 我要知道的是：社会整体或某一个家庭的偏好是什么？
一个家庭中每一个成员对这些水果都有自己的偏好
每个人都有自己的偏好那么我能对整个家庭的偏好做出任何判断吗？
首先要注意的是 如果每个人的偏好都一样那么这个问题就只是小菜一碟
如果说家里每个成员对水果偏好程度排序是：苹果 然后是香蕉 最后是椰子
那我们就可以说这个家庭的偏好顺序是：苹果 然后是香蕉 最后是椰子
如果不同的人喜欢不同的东西那么这个问题就有点棘手了
如果我们中的某个人对水果的偏好顺序是：苹果、香蕉、椰子
而另一个人则是香蕉、椰子和苹果这样一来如果我们在选择顺序上不同
要判断我们的集体偏好是什么就是个问题了
什么才是我们的集体偏好呢？因此这变成了一个聚合问题
我们知道每一个人的偏好然后想知道什么是集体偏好
现在问题开始变得有趣了让我们来仔细看一下
这里有一些偏好 第一个人喜欢苹果多于香蕉 香蕉又胜过椰子
而第二个人最爱香蕉 然后是苹果最后是椰子
第三个人则是苹果、香蕉和椰子
我们顺利掌握了这些偏好那么集体偏好是什么呢？
在这里我们喜欢的东西各有不同但很明显椰子应该是排在最后的
因为每个人把椰子放在最后所以我们把椰子放在这里
也就是最后的位置现在来看一下苹果和香蕉该怎么排
现在 我们可以做的是平等地对待每一个人
不要假设第二个人比第一个人重要一点或者比第三个人重要一点
我们把每个人都平等对待然后我们可以说：我们来投个票吧
如果我们投票的话有两个人最喜欢苹果 有一个人喜欢香蕉
所以我们就可以把苹果放在这里我画苹果的技能可不咋地
苹果比香蕉好一点哦 这香蕉画得真是太糟糕了
最后有一只椰子它们构成了一个偏好集合：
苹果、香蕉、椰子这个问题很简单
让我们来看看偏好顺序更多样化一点的情况
现在第一个人的偏好顺序是苹果、香蕉、椰子第二个人的偏好顺序是香蕉、椰子、苹果
而第三个人的偏好顺序是椰子、苹果 最后是香蕉那么我们想想
现在发生什么事呢？似乎没有可以明显胜出的水果
但我们可以做的是：让我们做个配对比较吧
让我们把这些结果对照一下
首先是椰子和苹果 如果我们要比较椰子和苹果我们注意这一点
让我们再一次把这些人标记为一号、二号和三号如果我们对比椰子和苹果
我们看到二号和三号更喜欢椰子
所以椰子以二比一胜出如果我们对比椰子和香蕉
我们看到一号和二号都喜欢香蕉胜过椰子
所以香蕉将胜出 让我们把椰子和香蕉圈一下椰子将胜过苹果
而香蕉胜过椰子所以我们可以合理地得出结论：
香蕉将胜过苹果
因为香蕉胜过椰子 椰子又胜过苹果
所以香蕉将胜过椰子让我们检查一遍确认一下
我们对比了苹果和香蕉我们看到一号更喜欢苹果而非香蕉
二号则喜欢香蕉胜过苹果但是三号却喜欢苹果胜过香蕉
一号和三号都更喜欢苹果
所以苹果胜出 看看这个组这是一个集体选择
也就是集体偏好这个集体喜欢椰子胜过苹果
喜欢苹果胜过香蕉 但却喜欢香蕉胜过椰子
这是不合理性的 没有显示出传递性这事儿很吊诡
集体中每一个人都是理性的他们的偏好都符合传递性
没有任何矛盾之处 但在投票时
当我们试着将这些偏好聚合在一起时我们得到的结果却并不一致
这是一种聚合悖论 在我们谈论聚合时
一个简单的规则可能创造了一个复杂的现象
我们在这儿要表达的意思是偏好或其他结构聚合时会有一种特殊的属性：
聚合的部分所具有的某些性质可能是聚合结果所没有的
每一个的都是理性的 但聚合结果却是非理性的
专业上称这为孔多塞悖论（投票悖论）每个人都是理性的
每个人都有一个理性偏好集合但当我们投票时
聚合结果却是非理性的让我们返回水果的例子看一下
聚合结果表明 椰子与苹果比较 集体更喜欢椰子苹果与香蕉相比 集体更喜欢香蕉
所以你将认为集体必然喜欢椰子多过香蕉
但事实上如果你让人们投票选择他们将喜欢香蕉多过椰子 这个就是孔多塞悖论
每个人都是理性的 但是集体却是非理性
这意味着投票可能会非常严重后果这一后果是：
当我们想到用投票解决问题时 出乎我们意料的是我们并不一定会得到一个正确的结果
我们可能得到一个几乎是随机的结果这意味着一件事：
人们可能会在投票时使用策略所以在稍后的课中
当我们开始建立人们如何投票的模型时那是在接近课程结束的时候
我们将了解到事实上聚合并不真的有效
聚合还是有一些问题的偏好聚合也有一点问题
但聚合仍将发展出新的动机、机会和情景在这些情境中人们可能会想要控制议程
隐瞒他们的偏好或者故意歪曲他们的偏好
以获得他们想要的结果选水果就是个例子
在这个例子里集体偏好并不能给我们想要的对了彻底明白这一点我们再返回看一下
每个人的偏好都是理性的 具有传递性的
这与你期待的完全一致但当你看这个集体偏好时可以发现它是非理性的
因而聚合是一个有趣的概念这也是社会科学
在这个特殊的例子中 政治如此有趣的原因
因为发生在宏观层面上的东西在逻辑上似乎是自相矛盾的
即使大概它走出宏观层面时就完全没有问题
我们已经看到了几种不同形式的聚合我们看到了数字在中心极限定理中的聚合
我们在生命游戏和一维细胞自动机模型中
看到了规则的聚合我们意识到
可以从简单的部分中得到非常复杂的东西这一节中我们看到了偏好的聚合
我们很好奇在其他数学结构也就是排序中的聚合是怎样的
我们发现有以下两个性质：
即使在数学意义上是可传递的在社会学意义上是理性的
然而排序聚合的结果未必是可传递性的和理性的
我们发现当排序逐渐在宏观上聚合时可能丧失逻辑一致性
这些关于聚合的有趣的方面我们将通过整个课程来了解
这些特殊的模型中没有一个是真实的
但它们却是最为基本的为我们思考问题打下了基础
我希望这些课程至少能教你们一件事
即让你们领略到把事情聚合起来是多么神秘和复杂
以及为什么社会与组成它的部分非常不同谢谢大家