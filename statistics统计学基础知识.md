# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
* [目录](#目录)
* [1. 常见概念](#1-常见概念)
   * [1. 置信区间](#1-置信区间)
   * [2. 标准差(SD)和标准误(SE)](#2-标准差sd和标准误se)
* [2. 参考资料](#2-参考资料)
   * [1. 说人话的统计学-协和八](#1-说人话的统计学-协和八)
* [3. 各种分布](#3-各种分布)
   * [1. 泊松分布](#1-泊松分布)
* [4. 统计检验](#4-统计检验)
   * [1. 卡方检验](#1-卡方检验)
<!--te-->

----

# 1. 常见概念

## 1. 置信区间

* [抽样分布与参数估计](https://wenku.baidu.com/view/df8a35aef90f76c661371ab9.html)
* [一文快速搞懂对95%置信区间的理解](https://blog.csdn.net/pannn0504/article/details/82455934)


**概念**

最常出现的对置信区间的错误理解：

> 在95%置信区间内，有95%的概率包括真实参数  （错误！！）
在95%置信区下构建的模型，意味着模型参数对于试图近似的函数有95%的概率是真实值的估计值（错误！！）

正确解释应为：

> 95%置信区间，意味着如果你用同样的步骤，去选样本，计算置信区间，那么100次这样的独立过程，
有95%的概率你计算出来的区间会包含真实参数值，即大概会有95个置信区间会包含真值。
而对于某一次计算得到的某一个置信区间，其包含真值的概率，我们无法讨论。

我们平常使用的频率学派（frequentist）95% 置信区间的意思并不是真值在这个区间内的概率是 95%。真值要么在，要么不在。
由于在频率学派当中，真值是一个常数，而非随机变量（后者是贝叶斯学派） ，所以我们不对真值做概率描述。对于这个问题来说，
理解的关键是我们是对这个构造置信区间的方法做概率描述，而非真值，也非我们算得的这个区间本身。

换言之，我们可以说，如果我们重复取样，每次取样后都用这个方法构造置信区间，有 95% 的置信区间会包含真值 。
然而（在频率学派当中）我们无法讨论其中某一个置信区间包含真值的概率。


**样本均值分布于中心极值定理**

* 正态总体中，样本均值的分布仍为正态分布。
* 非正态总体，根据中心极值定理：设从均值为μ,方差为σ<sup>2</sup>的任意一个总体中抽取样本量为
n的样本。当n充分大时，样本均值X近似服从N(μ,σ<sup>2</sup>/n)


**抽样标准误**

在任何一项抽样中，统计量的标准差称为抽样标准误，在利用样本平均数估计总体平均数时，抽样标准误即
为**样本平均数的标准差**,即σ<sup>2</sup><sub>x</sub> = σ<sup>2</sup> / sqrt(n)  [σ为总体标准差，
σ<sub>x</sub>为样本标准差]


**置信度与置信区间的关系**

以正态分布为例，当置信度为P时，置信区间为[μ-tσ, μ+tσ], 其中μ为期望值，σ为标准差，t称为概率度，
一下为对应关系

| 概率度(t) | 概率值(p) | 概率度(t) | 概率值(p) |
| ---- | ---- | ---- | ---- |
| 1.28 | 80% | 1 | 68.27% |
| 1.64 | 90% | 2 | 95.45% |
| 1.96 | 95% | 3 | 99.93% |
| 2.58 | 99% |   |        |

95%的置信区间为：

[μ-1.96σ/sqrt(n), μ+1.96σ/sqrt(n)]

其中1.96为95%置信度对应的概率度，σ为总体标准差，σ/sqrt(n)为抽样标准误, 即样本标准差



## 2. 标准差(SD)和标准误(SE)

* [标准差(Standard Deviation) 和 标准误差(Standard Error)](https://blog.csdn.net/haipengdai/article/details/53715463)
* [关于样本标准差（SD）与样本标准误差（SE）](https://www.jianshu.com/p/bd1cb90568d6)

**标准差(Standard Deviation)**

标准差表达数据的离散程度，然后实际应用中很多数据具有近似正态分布的概率分布，有了SD，我们就可以大致估计数据的范围，
譬如经典的"68-95-99.7法则"，即约 68% 数值分布在距离平均值有 1 个标准差之内的范围，约 95% 数值分布在距离平均值
有 2 个标准差之内的范围，以及约 99.7% 数值分布在距离平均值有 3 个标准差之内的范围。

![](https://upload-images.jianshu.io/upload_images/4025027-bc80f2798e909707.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/403/format/webp)

总体标准差的定义式为:

![](http://latex.codecogs.com/gif.latex?{\\sigma}&space;=&space;\\sqrt{\\frac{1}{N}\\sum_{i=1}^{N}\\left&space;(&space;x_{i}&space;-&space;\\mu&space;\\right&space;)^{2}})

但我们往往不知道总体，所有需要用样本标准差s的值作为总体标准差σ的估计值，样本标准差的计算公式为：

![](http://latex.codecogs.com/gif.latex?s&space;=&space;\\sqrt{\\frac{1}{n-1}\\sum_{i=1}^{n}\\left&space;(&space;x_{i}&space;-&space;\\bar{x}&space;\\right&space;)^{2}})


**标准误(Standard Error)**

SE是什么呢，一般来说，自然界里很难获得总体数据，我们只能用样本（无论是各种实验还是社会调查抽样）去近似估计总体，
这样问题就来了，估计的准不准（平均值）？

我们可以理论上这样做，既然不能获得总体，我们可以尽可能多（无限）的从标准差为σ的总体数据里抽取大小为 n 的样本，
每个样本各有一个平均值，所有样本平均值的标准差就可以用"68-95-99.7法则"评估准不准了（这就是所谓的置信区间），
样本平均值的标准差可以被证明如下公式表达：

![](http://latex.codecogs.com/gif.latex?SD_{\\bar{x}}&space;=&space;\\frac{\\sigma}{\\sqrt{N}})

但由于通常σ为未知，此时可以用研究中取得样本的标准差 (S) 来估计：

![](http://latex.codecogs.com/gif.latex?SE_{\\bar{x}}&space;=&space;\\frac{s}{\\sqrt{n}})

这就是SE的来源，即样本平均值的SD，我们进行代码演示。

以掷硬币为例，掷100次，统计正面的次数(此为1个数据点)，共统计1000次作为一个sample(此为1次采样，即1次采样共
包含1000个数据点)，然后我们这样采1000个sample(采样1000次)。

```python
import numpy as np

samples = np.random.randint(0, 2, size=(1000, 1000, 100)).sum(2) 
# shape:(1000, 1000), 每一行代表1次采样，每一列代表1个数据点

#第1次采样的标准差和标准误
sam1_sd = np.std(samples[0])
sam1_se = sam1_sd / np.sqrt(1000)

#1000次采样平均值的标准差
sam_mean_sd = np.std(samples.mean(1))
```

我们能看到样本平均值的SD基本等于样本的SE！


**结论**

1. 标准差（SD）更能反应离散程度。

paper里需要Mean±SD这个信息，就是便于读者进行判断数据的离散性，
e.g.，一般我们把偏离平均值2或3个SD的值作为outlier（i.e., 异常值）。

2. 标准误则比较适合用于评估精确性或准确性的问题。

paper里根据需要也可以提供Mean±SE这个信息，就是便于读者进行判断数据的不确定性，
e.g.，95%置信区间是用的Mean ± 1.96*SE。

3. SD -> SE -> CI

当我们获得一个样本后，可以计算出该样本的平均值![](http://latex.codecogs.com/gif.latex?\\bar{x})和标准差s,
有了标准差s，我们就可以计算出该样本的标准误e, 进而可以求得该样本平均值的置信区间CI



# 2. 参考资料

## 1. [说人话的统计学-协和八](https://mp.weixin.qq.com/s/9UQ-dXbP9wuOZ5B_TjDstg)

**第1章 高屋建瓴看统计**

* [你真的懂p值吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=207134405&idx=1&sn=8a4e661a0cd0fad97d869845f2e4b1a2&scene=21#wechat_redirect)
* [做统计，多少数据才算够？（上）](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=207643438&idx=1&sn=20fbf90250185008f841fffe28bf4e9b&scene=21#wechat_redirect)
* [做统计，多少数据才算够？（下）](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=207981601&idx=1&sn=ec4235c0df795e858ed99020381473c0&scene=21#wechat_redirect)
* [提升统计功效，让评审心服口服！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=208048284&idx=1&sn=ea3e00da596826b6c0b267bca46e4306&scene=21#wechat_redirect)
* [你的科研成果都是真的吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=208129350&idx=1&sn=734fa50cf19fec17afb7103c11fd6439&scene=21#wechat_redirect)
* [见识数据分析的「独孤九剑」](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=208295028&idx=1&sn=d22dea627fff86bf0daded79959bd019&scene=21#wechat_redirect)
* [贝叶斯vs频率派：武功到底哪家强？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=208453473&idx=1&sn=8d16e540580c3aced266a6c9041f996c&scene=21#wechat_redirect)

**第2章 算术平均数与正态分布**

[数据到手了，第一件事先干啥？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=400430409&idx=1&sn=03b30d4122d177650543f50649195ebd&scene=21#wechat_redirect)
* [算术平均数：简单背后有乾坤](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=400735492&idx=1&sn=dc2b5dae73740cd2841dabf2c420f842&scene=21#wechat_redirect)
* [正态分布到底是怎么来的？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=401781634&idx=1&sn=4cbabdb7191b8d49df95f0988943e18b&scene=21#wechat_redirect)

**第3章 t检验：两组平均数的比较**

* [想玩转t检验？你得从这一篇看起](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=402713181&idx=1&sn=eafb0bd061c6d22fba9582ba230a942c&scene=21#wechat_redirect)
* [就是要实用！t 检验的七十二变](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=403019527&idx=1&sn=9d279713517f96a204d4541e3ff68023&scene=21#wechat_redirect)
* [不是正态分布，t 检验还能用吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=403375449&idx=1&sn=2fb2c79f8b272686d3908c38ad03b6b1&scene=21#wechat_redirect)
* [只有15个标本，也能指望 t 检验吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=403973660&idx=1&sn=e6c513cfde7b47f1c195d401d142f0f2&scene=21#wechat_redirect)
* [样本分布不正态？数据变换来救场！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652548058&idx=1&sn=35f73ef5a627b20c1fd29e3eb3ed8b33&scene=21#wechat_redirect)
* [数据变换的万能钥匙：Box-Cox变换](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652548109&idx=1&sn=0fdd23615447ee8ec27900dbb33a0026&scene=21#wechat_redirect)
* [只讲 p 值，不讲效应大小，都是耍流氓！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652548670&idx=1&sn=93eb1ce6a6b97c21247108db2a868361&scene=21#wechat_redirect)
* [用置信区间，就是这么（不）自信！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652549146&idx=1&sn=94f80df33a0ff425c9884971645a33be&scene=21#wechat_redirect)
* [如何确定 t 检验的置信区间](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652549198&idx=2&sn=b27598a5f93c9d4957c1287be799b374&scene=21#wechat_redirect)
* [优雅秀出你的 t 检验，提升Paper逼格！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652549367&idx=1&sn=6a32c3a96bbf885ebd81c7dd4c52783e&scene=21#wechat_redirect)
* [要做 t 检验，这两口毒奶可喝不得！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652549476&idx=1&sn=d571ebf331f5ad08413f9e9a57c73b3c&scene=21#wechat_redirect)

**第4章 方差分析(ANOVA)：多组平均数的比较**

* [要比较三组数据，t 检验还能用吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652549639&idx=1&sn=877daad6e64e689dfb72b8ab7b95bb18&scene=21#wechat_redirect)
* [ANOVA在手，多组比较不犯愁](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652549791&idx=1&sn=e7079f101ccc4ca5a2f9899d163d2e60&scene=21#wechat_redirect)
* [ANOVA的基本招式你掌握了吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652549926&idx=1&sn=7dc7d10bd57a8833ebe67a2e33f7f0dd&chksm=80bba2fbb7cc2bedc1d37f5b35e2b581479c327bf0edb1a5b39392027c7ee977c8644c8eca7d&scene=21#wechat_redirect)
* [ANOVA做出了显著性？事儿还没完呢！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652550143&idx=1&sn=c3ee5aafdf9404bba3abeb3386ef9f83&chksm=80bba222b7cc2b3436e6e9b5509055d1387ad21eb89c24b26d571452fdfb56cfbeb0e93c011e&scene=21#wechat_redirect)
* [听说，成对t检验还有ANOVA进阶版？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652550306&idx=1&sn=394f7597b8e80f5a20877923094b7663&chksm=80bba57fb7cc2c6979d94982d4e4b10a24c66434ba6ece4deb5a22fe4047720d21f6c0a8cdbc&scene=21#wechat_redirect)
* [重复测量ANOVA：你要知道的事儿都在这里啦](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652550550&idx=1&sn=f86f766ec2b5b883232317fabfb8055b&chksm=80bba44bb7cc2d5dc6b6e222f24c4d63f65cb4570771b30b9c4aee8cae6a9abb5ecd39e39008&scene=21#wechat_redirect)
* [没听说过多因素 ANOVA ？那你就可就 OUT 了！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652550743&idx=1&sn=189408e5db94d3242b599596dd4130cc&chksm=80bba78ab7cc2e9cae8f64f2a69e617efb807899656c1c1156de645ae7a36cb5e2d643b355e4&scene=21#wechat_redirect)
* [多因素ANOVA＝好几个单因素ANOVA？可没这么简单！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652550964&idx=1&sn=1cda6ec54d40aa21c992e7ea61e661ff&chksm=80bba6e9b7cc2fff85ed20d3d7ca637deb2db4c7f8c663f61b6bfeac84aaae0d843395ca3473&scene=21#wechat_redirect)
* [两个因素相互影响，ANOVA结果该如何判读？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652551172&idx=1&sn=4dd852c9460b84e19ccd127ebf34c9ec&chksm=80bba9d9b7cc20cf9726b22576744dc6685065377942977b61a6145fe0952600f8f3c71d8b68&scene=21#wechat_redirect)
* [ANOVA还能搞三四五因素？等等，我头有点儿晕](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652551457&idx=1&sn=be0f338c2e815b770a59f5448416b072&chksm=80bba8fcb7cc21ea085e4c83164b8cd6025f46bf74ab950c861d9fcf3c3b994f04d404b5e2d3&scene=21#wechat_redirect)
* [要做ANOVA，样本量多大才够用](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652551560&idx=1&sn=3d30bf3068bc9fe0f26692d50c038a5a&chksm=80bba855b7cc2143ec7575a46dff0dda8e773e040bc1b8f37fc2c4c47fd19e6f25acc9aa873a&scene=21#wechat_redirect)

**第5章 线性回归：统计建模初步**

* [车模航模你玩过，统计学模型你会玩吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652551691&idx=1&sn=ae8993277c68a1f660c0fbeb81f1b7ef&chksm=80bbabd6b7cc22c0b63ef0ef1e541a59003d10241cba7687ea26eb2b8640371782e514ed927e&scene=21#wechat_redirect)
* [如果只能学习一种统计方法，我选择线性回归](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652551811&idx=1&sn=d441953a14d4a09be4c62f982924f3bb&chksm=80bbab5eb7cc224832626ff58860f72a3fd93e7407d5c04285d2c9574306183667a779f22a1c&scene=21#wechat_redirect)
* [回归线三千，我只取这一条](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652552010&idx=1&sn=cdaf7103bb6bdb81d3e65ce5a5d65610&chksm=80bbaa97b7cc2381a7d17dd2b878df07809507377f60093dde7f90533391840d6083c0274b6f&scene=21#wechat_redirect)
* [三千回归线里选中了你，你靠谱吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652552220&idx=1&sn=717e5c741d6e9ce30c255975bb94cfd8&chksm=80bbadc1b7cc24d75a4d57539d0da20e1c23963b49622d8fa4cfc27d3b595cebc4812a7b03a2&scene=21#wechat_redirect)
* [自变量不止一个，线性回归该怎么做？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652552402&idx=1&sn=e2096d4e2763e019d7d735efa9e010f7&chksm=80bbad0fb7cc2419afc931720e3abc48ce608a0c11e978163983f95542e54377a5f4ff1ba467&scene=21#wechat_redirect)
* [找出「交互效应」，让线性模型更万能](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652552648&idx=1&sn=aa0dfdf3adac2e5ff4a7c7ffad0bfaee&chksm=80bbac15b7cc2503a308fd8827a83b55ec94db24a67265e7907f08a2fccf2f09e33ec88018a7&scene=21#wechat_redirect)
* [天啦噜！没考虑到混杂因素，后果会这么严重？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652552738&idx=1&sn=da201510bafb95b2f4156b04694a0cc3&chksm=80bbafffb7cc26e95bd08befdc70f2f5e245a7de84df55bffdb23a2d6b2c49789a6531549aa4&scene=21#wechat_redirect)
* [回归系数不显著？也许是打开方式不对！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652552927&idx=1&sn=243075854a7d9c428a9c81ff196d005c&chksm=80bbaf02b7cc2614607329bcfa335e9eeb01b708a074a35270474fde64ed83c1002b761083e6&scene=21#wechat_redirect)
* [评价线性模型，R平方是个好裁判吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652553119&idx=1&sn=d7ed15b0516269b74457afb05fe92ae1&chksm=80bbae42b7cc275469485a52d8b1a7daf94f09aa319dd138fc2732eadf72be9eb3e0a478f044&scene=21#wechat_redirect)
* [如果R平方是砒霜，本文教你三种解药！](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652553213&idx=1&sn=e3b41220fd001f33964168cc9b0aebe4&chksm=80bbae20b7cc2736c231d9409ff2f8b33397d9df773356ef38ed1d2e07b96fb8bd63e2d9b607&scene=21#wechat_redirect)
* [线性模型生病了，你懂得怎样诊断吗？](https://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652553278&idx=1&sn=911872deb951e3cb2df16f5a422a1517&chksm=80bbd1e3b7cc58f580c4e4aa9c66054ad7baa841f8222fc3ab99ba24d1798d300936de1c24a9&scene=21#wechat_redirect)
* [「脱离群众」的数据点，是「春风化雨」还是「秋风扫落叶」](https://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652553348&idx=1&sn=e48000f41aad9e8b011cd142a6d90adb&chksm=80bbd159b7cc584f50c1379ce244c48a57028dfa4e8e2c99045c5c47da8efe2e0e0492c4c7fb&scene=21#wechat_redirect)

**第6章 广义线性模型：统计建模进阶**

* [你在 或者不在 需要逻辑回归来算](https://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&amp;mid=2652553458&amp;idx=1&amp;sn=cd3eafdf82243346642fe57234d64d73&amp;chksm=80bbd12fb7cc58394bea5b4ca24dead48d9def51a9f0ad20aa89458d14be944c83ceb51ab72e&scene=21#wechat_redirect)
* [逻辑回归的袅娜曲线，你是否会过目难忘？](https://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652553605&idx=1&sn=048729536703ad7ec08032b0a7d15ff4&scene=21#wechat_redirect)
* [逻辑回归的统计检验，原来招数辣么多？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652554118&idx=2&sn=e14d82806e74fb37f3acfdb6c6d13aee&chksm=80bbd25bb7cc5b4d692c18ba181060b7e59f2a80b71683478da797a1314add1949a48486daad&scene=21#wechat_redirect)
* [线性回归能玩多变量，逻辑回归当然也能!](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652554118&idx=1&sn=422b68cd453032109bea73a37496793b&chksm=80bbd25bb7cc5b4d7e6cd9c6aad28e180f721fa65c1dd1b21858e4c46c0c854d4f22d9442f2b&scene=21#wechat_redirect)
* [喂，你的逻辑回归模型该做个体检啦](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652554302&idx=1&sn=085df8a05c5f51847ae94151e85e2d25&chksm=80bbd5e3b7cc5cf55fcfa83d3584869d3c32c633885af53f59d029e2fe636c15b225d3455f93&scene=21#wechat_redirect)
* [逻辑回归能摆平二分类因变量，那……不止二分类呢？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652554469&idx=1&sn=6f06c3485f31bbacf66616848bbf4295&chksm=80bbd538b7cc5c2e7f118601387af4d7606f1b92df0979e338abb339d20a0743c799d8846d9f&scene=21#wechat_redirect)
* [让人眼花缭乱的多项逻辑回归，原来是这么用的](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652554542&idx=1&sn=c28757c48aecb04b099fcedc229cc7a9&chksm=80bbd4f3b7cc5de5cfe95901d8142925f32baccc1624dc10c884ed79fa7dd1c8992dbbbd72ae&scene=21#wechat_redirect)
* [只问方向，无问远近，定序回归的执念你懂吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652554613&idx=1&sn=e7ad742318c22bb7a251880768f7e4c1&chksm=80bbd4a8b7cc5dbee17bbfe90c850b5bafa28ea89ea2beb010af590dc66c75e88d99367753af&scene=21#wechat_redirect)
* [包教包会：定序回归实战](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652554707&idx=1&sn=d5103ca376456d79d233c5526182e6e0&chksm=80bbd40eb7cc5d186992f93842d8d94d968da5715d82047a3158b13fe595c7d5ef9998fa5550&scene=21#wechat_redirect)
* [「数」风流人物，还靠泊松回归](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652554788&idx=1&sn=14d43bcf154646a2f2f1483b73ce104d&chksm=80bbd7f9b7cc5eefe1acea860cb7568be0d12d770b0cc1896996717aa9fc5a773e115c99076a&scene=21#wechat_redirect)
* [广义线性模型到底是个什么鬼？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=2652554925&idx=1&sn=c8ee808dfcca76afb9f39178fabfbf66&chksm=80bbd770b7cc5e6697f9aed47680ec241cbaa0c9028e7327a19c939562b6e3cd55b4b1a34463&scene=21#wechat_redirect)

**自检**

* [妈妈说答对的童鞋才能中奖](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=208295028&idx=2&sn=a403c7f96021fed41edd3084b5a50f50&scene=21#wechat_redirect)
* [统计学的十个误区，你答对了吗？](http://mp.weixin.qq.com/s?__biz=MzAxMDA4NjU3OA==&mid=208453473&idx=2&sn=05bd3906de45598dd8f05584e39f352e&scene=21#wechat_redirect)


# 3. 各种分布

## 1. 泊松分布

* [概念](https://blog.csdn.net/hhtnan/article/details/62045872)
* [泊松分布的期望和方差](https://baike.baidu.com/item/%E6%B3%8A%E6%9D%BE%E5%88%86%E5%B8%83/1442110?fr=aladdin)
* [近似高斯分布](https://www.ppkao.com/tiku/shiti/5520985.html)


# 4. 统计检验

## 1. 卡方检验

* [MBAlib智库百科](https://wiki.mbalib.com/wiki/%E5%8D%A1%E6%96%B9%E6%A3%80%E9%AA%8C)
* [Wikipedia](https://zh.wikipedia.org/wiki/%E5%8D%A1%E6%96%B9%E6%A3%80%E9%AA%8C)
* [Python 卡方检验](https://blog.csdn.net/kk185800961/article/details/79054968)
* [几种常见的滥（乱）用卡方检验的情况](http://paper.dxy.cn/article/78383)
* [三维卡方检验](http://www.dxy.cn/bbs/thread/28440824#28440824) [三维卡方检验](http://www.dxy.cn/bbs/topic/25248045)

* `scipy.stats.chi2_contingency`: 列联表中变量间的独立性卡方检验，如统计收入是否与性别有关。
* `scipy.stats.chisquare`: 单变量卡方检验(适合度卡方检验，卡方适度检验) (零假设：分类数据有相同频率)。
实际执行多项式试验而得到的观察次数，与虚无假设的期望次数相比较，称为卡方适度检验，即在于检验二者接近的程度，
利用样本数据以检验总体分布是否为某一特定分布的统计方法。