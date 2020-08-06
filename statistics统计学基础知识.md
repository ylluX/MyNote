# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
* [目录](#目录)
* [1. 常见概念](#1-常见概念)
   * [1. 置信区间](#1-置信区间)
   * [2. 标准差(SD)和标准误(SE)](#2-标准差sd和标准误se)
   * [3. 误差(Error)，偏差(Bias)，方差(Variance)](#3-误差error偏差bias方差variance)
   * [4. 医学统计学中的OR，HR，RR](#4-医学统计学中的orhrrr)
   * [5. 医学统计学中的三大多变量回归分析：Cox 回归、logistic 回归和多元线性回归](#5-医学统计学中的三大多变量回归分析cox-回归logistic-回归和多元线性回归)
   * [6. pearson、spearman和kendall相关性分析](#6-pearsonspearman和kendall相关性分析)
   * [总体方差，样本方差，样本均值方差，样本方差期望](#总体方差样本方差样本均值方差样本方差期望)
   * [稳健的测量值(IQR, MAD, biweight)](#稳健的测量值iqr-mad-biweight)
   * [贝叶斯](#贝叶斯)
* [2. 参考资料](#2-参考资料)
   * [1. 说人话的统计学-协和八](#1-说人话的统计学-协和八)
   * [2. [观察性研究控制混杂因素-医咖会]](#2-观察性研究控制混杂因素-医咖会)
* [3. 各种分布](#3-各种分布)
   * [1. 泊松分布](#1-泊松分布)
   * [2. 二项分布(Binomial distribution, 贝努里分布)](#2-二项分布binomial-distribution-贝努里分布)
   * [3. 负二项分布(negative binomial distribution)](#3-负二项分布negative-binomial-distribution)
   * [4. beta分布](#4-beta分布)
   * [一句话说分布](#一句话说分布)
   * [5. 抽样分布](#5-抽样分布)
* [4. 统计检验](#4-统计检验)
   * [假设检验的4中方法](#假设检验的4中方法)
   * [U检验(Z检验)](#u检验z检验)
   * [T检验](#t检验)
   * [卡方检验](#卡方检验)
   * [多变量逻辑回归分析](#多变量逻辑回归分析)
   * [参数检验和非参数检验](#参数检验和非参数检验)
* [5. 回归](#5-回归)
   * [1. 线性回归](#1-线性回归)
* [6. 各种定理](#6-各种定理)
* [python实现](#python实现)
   * [【U检验/Z检验】已知z统计量，求p值](#u检验z检验已知z统计量求p值)
   * [【T检验】已知t统计量，求p值](#t检验已知t统计量求p值)
* [疑问](#疑问)
* [中英文对照](#中英文对照)
<!--te-->

----

# 1. 常见概念

## 1. 置信区间

* [抽样分布与参数估计](https://wenku.baidu.com/view/df8a35aef90f76c661371ab9.html)
* [一文快速搞懂对95%置信区间的理解](https://blog.csdn.net/pannn0504/article/details/82455934)
* [Python量化统计——『置信区间』全角度解析](https://www.sohu.com/a/116174099_505915)


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


## 3. 误差(Error)，偏差(Bias)，方差(Variance)

误差 = 预测值[h(x)] - 真实值[y]

偏差 = 预测值的均值[mean(h(x))] - 真实值[y]

方差 = 预测值[h(x)] - 预测值的均值[mean(h(x))]

误差 = 偏差 + 方差

误差是指结果与真实值之间的差值，而偏差则是指结果与平均值之间的差值，
都是对单个样本而言，只不过误差的参照物只有一个，而偏差的参照物是群体的平均值，
个体相对群体的平均水平的差值。“偏差” 跟 “平均值” 紧密联系在一起。

Error反映的是整个模型的准确度，Bias反映的是模型在样本上的输出与真实值之间的误差，
即模型本身的精准度，Variance反映的是模型每一次输出结果与模型输出期望（平均值）之间的误差，
即模型的稳定性，数据是否集中。 

方差是多个模型间的比较，而非对一个模型而言的；偏差可以是单个数据集中的，也可以是多个数据
集中的。


解决bias和Variance问题的方法：

1. 在训练数据上面，我们可以进行交叉验证(Cross-Validation)。 一种方法叫做
K-fold Cross Validation (K折交叉验证), K折交叉验证，初始采样分割成K个子样本，
一个单独的子样本被保留作为验证模型的数据，其他K-1个样本用来训练。交叉验证重复K次，
每个子样本验证一次，平均K次的结果或者使用其它结合方式，最终得到一个单一估测。 

当K值大的时候，我们会有更少的Bias(偏差), 更多的Variance。 
当K值小的时候，我们会有更多的Bias(偏差), 更少的Variance。 

cross-validation很大一个好处是避免对test dataset的二次overfitting。

k-fold一般取k=5/10比较常见，当然也可以根据你的需要。 

2. Boosting通过样本变权全部参与，故**Boosting 主要是降低 bias**
（同时也有降低 variance 的作用，但以降低 bias为主）；

而 Bagging 通过样本随机抽样部分参与（单个学习器训练），
故**bagging主要是降低 variance**。 

3. High bias解决方案： 
1）与领域专家交流来获取更多信息，据此增加更多熟人特征 
2）以非线性方式对现有特征进行组合 
3）使用更复杂模型，比如神经网络中的层等 

4. High Variance： 
如果问题是由于我们过度高估模型复杂度而导致的high Variance，
那么可以把一些影响小的特征去掉来降低模型复杂度。此时也无需收集更多数据

高偏差意味着欠拟合；高方差意味着过拟合。


## 4. 医学统计学中的OR，HR，RR

* [AME统计028|OR、HR、RR：三个经常把人弄晕的概念](https://www.cnblogs.com/shuaihe/articles/6580795.html)

在医学统计学中，有三个关于比值的概念，分别为相对危险度（relative risk，RR，也称 risk ratio）、风险比（hazard ratio，HR）
和优势比（odds ratio，OR）。很多同行一看见这三个概念就感觉恶心反胃、头皮发麻、窦性心动过速，大有雾里看花，水中望月的感觉。
在此，笔者拟谈谈如何正确理解这三个概念的区别和联系。

我们以病因学研究为例，先谈谈 OR 与 RR 的区别，因为这两个指标均可以从四格表中衍生出来。我们先来看看两个关于吸烟与肺癌的例子：

例1：为明确吸烟与肺癌的关系，某研究者在 1985 年随机调查了某社区的 10000 名居民，并每年对其进行随访，以观察其肺癌的发生状况
在刚刚进行调查的时候，他就发现这 10000 个居民中有 3000 人吸烟，7000 人不吸烟。在本例中，我们假定吸烟和不吸烟居民之间不存在
交叉污染，即吸烟的 3000 人永远不会戒烟，而不吸烟的 7000人 也永远不会吸烟。且这 10000 个人不会失访。随访 30 年后，吸烟的
 3000 人中有 300 人得了肺癌。相比之下，不吸烟的 7000 人中仅有 70 人患肺癌。如表1所示：

表1 吸烟与肺癌的关系

|  | 患肺癌 | 无肺癌 |
| ---- | ---- | ---- |
| 吸烟 | 300（a） | 2700（b） |
| 不吸烟 | 70（c） | 6930（d） |

RR 的定义是：暴露组发病率或死亡率与非暴露组发病率或死亡率之比。

在本案例中，吸烟人群 30 年内发生肺癌的比例为 0.10（300/3000），而不吸烟人群发生肺癌的比例为 0.01（70/7000）。
因此，与非吸烟人群相比，吸烟人群发生肺癌的相对危险度（RR）为：0.10/0.01=10，即可以认为吸烟人群 30 年内发生肺
癌的风险是非吸烟人群的 10 倍。实际上，不难看出，RR 在四格表中的计算公式就是：RR=（a/（a+b））/（c/（c+d））。

例2：某医生怀疑吸烟与肺癌有关，因为他发现自己经手的很多肺癌患者都有吸烟史。于是他在 2015 年找了 100 名肺癌患者
和 100 名健康对照，回溯了他们的过去 30 年的吸烟史，结果发现：100 名肺癌患者中 90 名患者有吸烟史，100 名健康个
体中仅有20人有吸烟史。如表2所示：

表2 吸烟与肺癌的关系

|  | 吸烟 | 不吸烟 |
| ---- | ---- | ---- |
| 肺癌 | 90（a） | 10（b） |
| 健康个体 | 20（c） | 80（d） |

OR 的定义是：病例组中暴露人数与非暴露人数的比值除以对照组中暴露人数与非暴露人数的比值。这里的“暴露”其实就是指“吸烟”。
在本案例中，肺癌组暴露人数与非暴露人数的比值为 9（90/10），而在健康个体中，暴露人数与非暴露人数的比值为 0.25（20/80）。
因此，OR 为：9/0.25=36。由此我们也不难看出，OR 在四格表中的计算公式为：OR=ad/bc。

部分读者看到这里可能觉得有点糊，按理说 RR 的临床解释最为清晰，说得通俗点就是：吸烟个体发生肺癌的风险是非吸烟个体的多
少倍。相比之下，OR 的临床解释则要复杂得多。为何表1用 RR 来描述吸烟与肺癌的关联强度，表2则要用 OR 来描述呢？按理说，
只要是四格表，都可以计算 RR，为什么流行病学家还搞个 OR 在这里呢？的确，所有的四格表都可以计算 RR，比如我们将表2调整
为如下格式（表3），当然也可以计算 RR：

表3 吸烟与肺癌的关系

|  | 患肺癌 | 无肺癌 |
| ---- | ---- | ---- |
| 吸烟 | 90 | 20 |
| 不吸烟 | 10 | 80 |

RR 的计算过程为：吸烟人群中有 110 名个体吸烟，90 例发生了肺癌，肺癌发生风险约为 0.82（90/110）；不吸烟的 90 名个体中，
仅有 10 人发生肺癌，因此肺癌的发生风险是 0.11（10/90）。因此与不吸烟的个体相比，吸烟个体发生肺癌的风险约为 7.45 倍
（0.82/0.11）。

然而，表2绝对不能转化成表3的格式，这是有研究的性质决定的，表1的数据来源于队列研究，表2的数据来源于病例对照研究。

如前述章节（有病例和对照的研究就是病例-对照研究？、实验组和对照组的样本量一定要“均衡”才行？）所述，队列研究和病例
对照研究有很大的区别，这些区别概括起来就是：队列研究是前瞻性研究，是由因索果的研究；病例对照研究是回顾性研究，是
由果索因的研究。前瞻性研究最大的优势在于：“真实世界”尚未发生，因为研究者可以详尽地描述“真实世界”，体现在：抽取的 
10000 名研究对象实际上就是来自于“真实世界”的，因为研究者是从普通人群中随机抽取研究对象的；研究对象中吸烟个体的比
例为 0.30，也是反映了真实情况，即现实生活中，吸烟个体的比例就是 0.30；随访 30 年后，总共有 370 人发生了肺癌（患
病率为 3.7%），这一患病率也是来源于真实世界的结论。由于其得出的 RR 值是来自于真实世界的，因此具有“外推性”，或者
说“泛化性”，可以直接地告诉人们吸烟的患者发生肺癌的风险是不吸烟患者的多少倍。

相比之下，病例对照研究就没有那么简单了，因为病例对照研究是先知道结局，再去回溯原因，此时，“真实世界”已经一去不复
返了，哪里还能完整地回溯回来？研究者募集了 100 名肺癌患者和 100 名健康个体，实际上就是假定了肺癌的患病率为 0.50，
这一数字显然不是来自于真实世界。在真实世界中，过去 30 年肺癌的发生了是多少呢？没有人会知道这个精确的数字。因此，
如果强行用 RR 来展示病例对照研究结果的话，没有多大的临床价值，因为这个 RR 不是来自真实世界的，不具备“外推性”。
流行病学家不得已，才在这里提出了一个 OR 的概念，用于反映暴露因素与结局事件的关联强度。如前所述，OR 这个指标在四
格表中的计算公式：OR=ad/bc，实际上也可以表示为（a/b）/（c/d）。理论上讲，不管实验组样本为多少例，a/b 是不变的
（当然可能会有一些小的波动，但属于抽样误差）；同理，不管对照组样本量如何变化，c/d 的比例也是固定的。因此，OR 
最大的优势的是不受实验组和对照组比例（或者说患病率）的影响。这也就是为什么在病例对照研究中人们喜欢用 OR 来表示
暴露因素与结局事件关联强度的原因所在。

我们不妨来做一个根本就不存在的假设。我们假设表1中的队列研究的资料是完全存在的，只是没有发表。后来，有人用病例
对照的研究思路来阐述吸烟与肺癌的关系。从表1我们得知，过去三十年，这个社区总共发生了 370 例肺癌，其中 300 个肺
癌患者具有吸烟史，70 个不具有吸烟史。因此如果从中抽取 100 例肺癌的话，理论上说就应该是 81 个肺癌患者有吸烟史，
19 个肺癌患者没有吸烟史。健康个体一共有 9630 个，其中 2700 个吸烟，6930 个不吸烟，如果从这 9630 个健康个体中抽
取 100 人的话，就应该有 28 个人吸烟，72 个人不吸烟。于是可以得出下表（表4）：

表4 吸烟与肺癌的关系

|  | 患肺癌 | 无肺癌 |
| ---- | ---- | ---- |
| 吸烟 | 81 | 28 |
| 不吸烟 | 19 | 72 |

根据表4的内容不难算出，与非吸烟个体相比，吸烟患者发生肺癌的 RR 是 3.56（计算过程略），该 RR 值与表1的 RR 值
（10）相距甚远。假定我们抽取的健康个体不是 100 人，而是 200 人，则可以算出 RR 为 5.07（计算过程略）。
由此可知，RR 在很大程度上受患病率的影响，病例对照研究之所以不能计算 RR，就是因为其患病率是假设的，就算勉强
计算出 RR 也不具备外推性，没啥意思。

OR 的临床解释是什么呢？笔者一般不喜欢去解释，因为解释的文字读起来也很繁琐，且个人认为临床价值不高。对于我
们而言，只需要记住 **OR 大于 1 表示暴露因素是危险因素，OR 小于 1 则表示暴露因素是保护因素即可**。

前述 OR 和 RR 都来源于四格表，即仅仅考虑了一个暴露因素（吸烟）与结局事件（肺癌）的关系。而在现实中，疾病
的发生往往不是单一因素作用的结果。比如：假定吸烟的人都不太喜欢吃水果，而水果摄入过少也可以导致肺癌。因此
很有可能出现一种极端的情况，其实吸烟与肺癌无关，我们之所以在队列研究或病例对照研究中观察到了吸烟与肺癌的
关系，完全是“吃水果”作怪。此时，我们将“吃水果”称为“混杂因素”，即表示他们可能会干扰暴露因素与结局变量之间
的关系。为了排除混杂因素的干扰，需要在统计学上做一些校正，比较常用的方法就是 Cox 风险比例模型和 logistic
 回归模型。一说到 Cox 风险比例模型和 logistic 回归模型，估计很多读者的脑海里马上闪现两个概念，HR 和 OR。
 没错，这里的 OR 和四格表里面的 OR 其实就是一个意思，只是二者的计算方法不同。来自于 logistic 回归的 OR 
 可以校正很多混杂因素，因此是一个多因素校正的 OR，而来自于四格表的 OR 只考虑了单一因素，因此可以简单理解
 为单因素分析的 OR。在撰写论文的过程中，一般认为多因素校正的 OR 更可靠。实际上，如果把四格表的数据用单因
 素的 logistic 回归方程计算，得到的 OR 是一样的，有兴趣的读者可以自己算。

Cox 模型与 logistic 回归有很多相似之处，都可以用于校正混杂因素。根据 Cox 模型可以计算出 HR 值，HR 值的解
释与 RR 几乎一致，即表示暴露组患病的概率为非暴露组的多少倍。但是与 logistic 回归不同的是，Cox 模型除了可
以校正混杂因素外，还考虑了结局事件发生的时间。因此，HR 不能简单等同于 RR，只能说 HR 是考虑了时间因素的 RR。
说得这里，估计部分读者有点糊，啥叫“考虑了时间因素的 RR”？我们不妨来做这样一个假设：在表1中（队列研究）中，
RR 为 10，我们可以理解为：与不吸烟人群相比，吸烟人群在 30 年内患肺癌的风险是不吸烟人群的10倍。注意“30 年内
患肺癌的风险”，这是一个很含糊的说法：有人可能在随访开始第二年就发生肺癌，有人可能到随访快结束时（第三十年）
才发生肺癌。如果构建四格表，这两个肺癌是同等看待的，但实际上，这两种肺癌的“社会危害性”显然是不能相提并论的！
毕竟后者很有可能会多活二十多年。因此，我们在考虑结局事件是否发生的同时，往往还要考虑结局事件发生的时间！这
就是 HR 存在的价值！

总结一下本文，以研究疾病发生机制的研究为例来谈谈 RR，OR 和 HR 的区别，实际上，研究疾病预后的研究也可以类推。

* RR：主要用于队列研究（前瞻性），可以从四格表衍生出来，表示暴露患者发生疾病的风险是非暴露患者的多少倍。
* OR：主要用于病例对照研究（回顾性）和横断面研究，可以从四格表中衍生出来，也可以由logistic回归计算得来，
表示病例组中暴露人数与非暴露人数的比值除以对照组中暴露人数与非暴露人数的比值。
* HR：主要用于队列研究（前瞻性），主要由 Cox 风险比例模型衍生出来，是考虑了时间因素的 RR。

最后留下一个问题给大家思考：对前瞻性队列研究数据的分析，可以用 logistic 回归计算 OR 值吗？为什么？



## 5. 医学统计学中的三大多变量回归分析：Cox 回归、logistic 回归和多元线性回归

* [AME统计016|Cox回归、logistic回归、多元线性回归到底有啥区别](http://kysj.amegroups.com/articles/3251)

简单来说：

* 多元线性回归的因变量是连续变量，而logistic回归和Cox回归的因变量是分类变量；
* Cox回归是与时间有关的(time-dependent)，如果您不仅仅关心结局变量是否发生，而且还关心其何时发生，那就选择 Cox 回归。
* logistic回归与时间无关，如果仅仅是关心结局变量是否发生，不关心其何时发生，那就选择 logistic 回归。



## 6. pearson、spearman和kendall相关性分析

* [三大统计相关系数：Pearson、Spearman秩相关系数、kendall等级相关系数](https://blog.csdn.net/zhaozhn5/article/details/78392220)

计算积距pearson相关系数，连续性变量才可采用;计算Spearman秩相关系数和Kendall秩相关系数，适合于定序变量或
不满足正态分布假设的等间隔数据。

pearson：  积差相关   计算连续变量或是等间距测度的变量间的相关分析   连续数据且总体是正态分布
spearman： 等级相关   计算斯皮尔曼相关，适用于连续等级资料
kendall：  等级相关   计算分类变量间的秩相关，适用于合并等级资料


## 总体方差，样本方差，样本均值方差，样本方差期望

* [样本方差的期望等于总体方差，这个意思是样本要取样很多次吗？多次取样算样本的方差的均值吗？不是一次？](https://www.zhihu.com/question/267716005)

总体方差，样本方差 **略**。

**样本方差期望** 就等于总体方差

**样本均值方差** = 总体方差 / 样本量(n)

随着样本数（或测量次数）n的增大，标准差趋向某个稳定值，即样本标准差s越接近总体标准差σ，而标准误差则随着样本数（或测量次数）n的增大逐渐减小，即样本平均数越接近总体平均数μ.


## 稳健的测量值(IQR, MAD, biweight)

传统的观测值，如平均值和标准差容易受到极值的影响，是不稳健的观测值。

1. MAD：绝对中位差(median absolute deviation)

> MAD = median(|X(i) - median(X)|)

2. biweight midvariance: 双权重中位方差

* [Biweight midcorrelation](https://en.wikipedia.org/wiki/Biweight_midcorrelation)
* [Robust measures of scale](https://en.wikipedia.org/wiki/Robust_measures_of_scale#The_biweight_midvariance)




## 贝叶斯

条件概率公式：

![](http://latex.codecogs.com/gif.latex?P(A|B)=\\frac{P(A\\cap&space;B)}{P(B)})

关于条件概率和联合概率的区别，请参考：[为什么从定义上看，觉得联合概率和条件概率是一个意思？](https://www.zhihu.com/question/278117164)

贝叶斯公式：

![](http://latex.codecogs.com/gif.latex?P(A|B)=\\frac{P(B|A)P(A)}{P(B)}&space;)

贝叶斯定理可表述为：`后验概率 = (似然性*先验概率)/标准化常量`, 也就是说，后验概率与先验概率和相似度的乘积成正比。

![](http://latex.codecogs.com/gif.latex?P(\\theta|X)=\\frac{P(X|\\theta)P(\\theta)}{P(X)})


**似然和概率的区别**

[似然（likelihood）与概率（probability）的区别](https://yangfangs.github.io/2018/04/06/the-different-of-likelihood-and-probability/#%E6%9C%AC%E6%96%87%E4%B8%AD%E6%95%B0%E5%AD%A6%E7%AC%A6%E5%8F%B7%E5%8F%8A%E5%90%AB%E4%B9%89)

[似然函数、最大似然估计简单理解](https://www.cnblogs.com/hejunlin1992/p/7976119.html)

在数理统计学中，似然函数是一种关于统计模型中的参数的函数，表示模型参数中的似然性。似然函数在统计推断中有重大作用，
如在最大似然估计和费雪信息之中的应用等等。“似然性”与“或然性”或“概率”意思相近，都是指某种事件发生的可能性，
但是在统计学中，“似然性”和“或然性”或“概率”又有明确的区分。概率用于在已知一些参数的情况下，预测接下来的观测所得到的结果，
而似然性则是用于在已知某些观测所得到的结果时，对有关事物的性质的参数进行估计。

在英文中，似然（likelihood）和概率（probability）是同义词，都指事件发生的可能性。但在统计中，
似然与概率是不同的东西。概率是已知参数，对结果可能性的预测。似然是已知结果，对参数是某个值
的可能性预测。

** 联合概率和边缘概率**

[贝叶斯估计、最大似然估计、最大后验概率估计](http://noahsnail.com/2018/05/17/2018-05-17-%E8%B4%9D%E5%8F%B6%E6%96%AF%E4%BC%B0%E8%AE%A1%E3%80%81%E6%9C%80%E5%A4%A7%E4%BC%BC%E7%84%B6%E4%BC%B0%E8%AE%A1%E3%80%81%E6%9C%80%E5%A4%A7%E5%90%8E%E9%AA%8C%E6%A6%82%E7%8E%87%E4%BC%B0%E8%AE%A1/)

假设有随机变量A和B，此时P(A=a,B=b)用于表示A=a且B=b同时发生的概率。这类包含多个条件且所有条件
同时成立的概率称为联合概率。请注意，联合概率并不是其中某个条件成立的概率，而是所有条件同时成
立的概率。与之对应地，P(A=a)或P(B=b)这类仅与单个随机变量有关的概率称为边缘概率。

**共轭先验**

在贝叶斯统计中，如果后验分布与先验分布属于同类，则先验分布与后验分布被称为共轭分布，
而先验分布被称为似然函数的共轭先验。

* 二项分布参数的共轭先验是Beta分布，
* 多项式分布参数的共轭先验是Dirichlet分布，
* 指数分布参数的共轭先验是Gamma分布，
* 高斯分布均值的共轭先验是另一个高斯分布，
* 泊松分布的共轭先验是Gamma分布。

**最大似然估计(MLE),最大后验概率估计(MAP),贝叶斯估计**

最大似然估计，英文为Maximum Likelihood Estimation，简写为MLE，也叫极大似然估计，
是用来估计概率模型参数的一种方法。最大似然估计的思想是使得观测数据（样本）发生
概率最大的参数就是最好的参数。

最大后验概率估计，英文为Maximum A Posteriori Estimation，简写为MAP。回到抛硬币
的问题，最大似然估计认为使似然函数P(X|θ)最大的参数θ即为最好的θ，此时最大似然估
计是将θ看作固定的值，只是其值未知；最大后验概率分布认为θ是一个随机变量，即θ具
有某种概率分布，称为先验分布，求解时除了要考虑似然函数P(X|θ)之外，还要考虑θ的
先验分布P(θ)，因此其认为使P(X|θ)P(θ)取最大值的θ就是最好的θ。此时要最大化的函
数变为P(X|θ)P(θ)。在最大似然估计中，由于认为θ是固定的，因此P(θ)=1。

贝叶斯估计最大后验估计的进一步扩展，贝叶斯估计同样假定θ是一个随机变量，但贝叶
斯估计并不是直接估计出θ的某个特定值，而是估计θ的分布，这是贝叶斯估计与最大后
验概率估计不同的地方。在贝叶斯估计中，先验分布P(X)是不可忽略的。回到抛硬币的
例子中，在已知X的情况下，描述θ的分布即描述P(θ|X)，P(θ|X)是一种后验分布。如果
后验分布的范围较窄，则估计值的准确度相对较高，反之，如果后验分布的范围较广，
则估计值的准确度就较低。


**对高斯分布的贝叶斯推断**

* [贝叶斯推断](http://www.jdl.ac.cn/user/lyqing/StatLearning/11_12-bayesian%20inference.pdf)
* [对高斯分布的贝叶斯推断](https://zlearning.netlify.com/computer/prml/prmlch2dot4-bayesian-inference-for-gaussian)
* [Bayesian update of a prior normal distribution with new sample information.](https://www.mhnederlof.nl/bayesnormalupdate.html)
* [正态分布的共轭分布及贝叶斯估计](https://wenku.baidu.com/view/353b9834f111f18583d05a80?ivk_sa=1023194j&fromShare=1)



----

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



## 2. [观察性研究控制混杂因素-医咖会]

* [如何借助图形优势来构建疾病的预测模型？](https://www.mediecogroup.com/method_topic_article_detail/126/)
* [那么多变量，我该选择哪些进入统计模型呢？](https://www.mediecogroup.com/method_topic_article_detail/127/)
* [观察性研究控制混杂因素第一弹：分层分析](https://www.mediecogroup.com/method_topic_article_detail/131/)
* [说道控制混杂因素，怎么能不提多因素分析！](https://www.mediecogroup.com/method_topic_article_detail/133/)
* [大量混杂因素要调整？这4中倾向性分析方法你值得了解！](https://www.mediecogroup.com/method_topic_article_detail/134/)
* [控制混杂因素，再给你支个大招：工具变量分析](https://www.mediecogroup.com/method_topic_article_detail/135/)
* [如何理解回归模型中的"调整"和"独立作用"](https://www.mediecogroup.com/method_topic_article_detail/157/)
* [搞懂传统单因素分析和单因素回归分析的纠葛，有这篇文章就够了！](https://www.mediecogroup.com/method_topic_article_detail/158/)
* [单因素分析和多因素分析的结果不一致，怎么办？](https://www.mediecogroup.com/method_topic_article_detail/159/)
* [我该咋筛选变量进入多因素回归？先教你基础几招！](https://www.mediecogroup.com/method_topic_article_detail/160/)
* [有个可疑的混杂因素Z，要不要放到多因素回归模型中呢？](https://www.mediecogroup.com/method_topic_article_detail/161/)
* [回归模型中的哑变量是个啥？何时需要设置哑变量？](https://www.mediecogroup.com/method_topic_article_detail/162/)
* [想将连续变量转化为哑变量纳入回归模型，咋分组？](https://www.mediecogroup.com/method_topic_article_detail/164/)
* [回归模型中引入连续变量，还有哪些玩法？](https://www.mediecogroup.com/method_topic_article_detail/165/)
* [回归模型中哪个自变量的作用更大？标准化回归系数来解答！](https://www.mediecogroup.com/method_topic_article_detail/166/)


----


# 3. 各种分布

[二项分布 | 泊松分布 | 指数分布 | 负二项分布 | 伽玛分布 | Βeta分布 | 卡方分布 | 正态分布 | 多维高斯分布 | 狄利克雷分布 | 帕累托分布 | 柯西分布 | 持续收集~...](https://blog.csdn.net/weixin_34166847/article/details/86395350)

## 1. 泊松分布

* [概念](https://blog.csdn.net/hhtnan/article/details/62045872)
* [泊松分布的期望和方差](https://baike.baidu.com/item/%E6%B3%8A%E6%9D%BE%E5%88%86%E5%B8%83/1442110?fr=aladdin)
* [近似高斯分布](https://www.ppkao.com/tiku/shiti/5520985.html)
* **[从二项分布推导泊松分布](https://blog.csdn.net/hustqb/article/details/85217313)**
* [不同分布之间的关系图](https://www.zhihu.com/question/21756860)


泊松分布当总体均值lambda值小于5时为偏锋，lambda愈小分布愈偏，随着lambda增大，分布趋向对称。
![](https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1925351379,3516268592&fm=26&gp=0.jpg)
![](https://s7.sinaimg.cn/orignal/0049xj5Jzy7bOvMj3nM56)


## 2. 二项分布(Binomial distribution, 贝努里分布)

* [智库](https://wiki.mbalib.com/wiki/%E4%BA%8C%E9%A1%B9%E5%88%86%E5%B8%83)


二项分布是一种具有广泛用途的离散型随机变量的概率分布，二项分布是指统计变量中只有性质不同的两项群体的
概率分布。所谓两项群体是按两种不同性质划分的统计变量，是二项试验的结果。即各个变量都可归为两个不同性
质中的一个，两个观测值是对立的。因而两项分布又可说是两个对立事件的概率分布。

当试验的次数趋于无穷大，而乘积np固定时，二项分布收敛于泊松分布。
因此参数为λ = np的泊松分布可以作为二项分布B(n, p)的近似，如果n足够大，而p足够小，np不大不小。


比较泊松分布和二项分布：

字面形式：泊松和二项都是描述某一事件发生n次的概率，但是前提却不一样。还是以通过学校大门为例，
泊松分布的描述是每个人独立通过大门（每个人独立，但并不知道每个人通过的概率），一段事件内通过n
人的概率，我们知道的是平均数。二项分布是我知道每个人通过的概率（也必须要独立），我可以知道N人
选择后，其中有n个人选择通过的概率。

所以，重要的区别是每个事件到底是不是等概率发生的！！！



## 3. 负二项分布(negative binomial distribution)

[RNA-seq中的那些统计学问题（一）为什么是负二项分布？](https://www.jianshu.com/p/ad24bb90b972)

“负二项分布”与“二项分布”的区别在于：“二项分布”是固定试验总次数N的独立试验中，成功次数k的分布；
而“负二项分布”是所有到失败r次时即终止的独立试验中，成功次数k的分布。

![](http://latex.codecogs.com/gif.latex?f(k|r,p)=\\binom{k+r-1}{k}\\cdot&space;p^{k}\\cdot&space;(1-p)^r)

r:失败的次数，k:成功的次数，p:成功的概率

该公式描述的是，在合格率为p的一堆产品中，进行连续有放回的抽样，当抽到r个次品时，停止抽样，此时抽到的正品正好为k个的概率

负二项分布的均值和方差分别为：

![](http://latex.codecogs.com/gif.latex?\\mu=\\frac{pr}{1-p})

![](http://latex.codecogs.com/gif.latex?\\sigma^{2}=\\frac{pr}{(1-p)^{2}})

将p用μ表示，得到：

![](http://latex.codecogs.com/gif.latex?p=\\frac{\\mu}{\\mu+r})

![](http://latex.codecogs.com/gif.latex?1-p=\\frac{r}{\\mu+r})

将上一步推出的p和1-p带入到方差的表达式中，得到：

![](http://latex.codecogs.com/gif.latex?\\sigma^{2}=\\frac{\\mu^{2}}{r}+\\mu)

记 1/r=α，则

![](http://latex.codecogs.com/gif.latex?\\sigma^{2}=\\mu+\\alpha\\mu^{2})

负二项分布与泊松分布的关系，可以用α或r推出：

> 当 r -> ∞ 时，α -> 0，此时 σ^2 = μ，为泊松分布；
当 r -> 0 时，α -> ∞，此时over dispersion(过度离散)

负二项分布的参数可以根据平均值μ 和方差 σ2求得：

![](http://latex.codecogs.com/gif.latex?p=\\frac{\\sigma^{2}-\\mu}{\\sigma^{2}})

![](http://latex.codecogs.com/gif.latex?r=\\frac{\\mu^{2}}{\\sigma^{2}-\\mu})



![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1562555993&di=9fe9e1910a87fe25a05a0110ade6bb62&imgtype=jpg&er=1&src=http%3A%2F%2Fa0.att.hudong.com%2F62%2F14%2F01300543364049145939141068886.png)
![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1561961274661&di=d24119fe7ed531d8608aaff8f7a6e957&imgtype=0&src=http%3A%2F%2Fboost.ez2learn.com%2Flibs%2Fmath%2Fdoc%2Fsf_and_dist%2Fgraphs%2Fnegative_binomial_pdf_1.png)
![](https://s16.sinaimg.cn/orignal/001orWlfgy6K9uhYK519f)

## 4. beta分布

[如何通俗理解 beta 分布？](https://www.zhihu.com/question/30269898)

感觉和贝叶斯理论(随着观测而更新概率)很像~


## 一句话说分布

**所有统计分布都是用于描述事件发生概率的，所有事件发生概率之和为1，也就是所有概率分布的面积（积分）为1.**

* 泊松分布: 单位时间或单位面积内随机事件发生次数的概率分布
* 二项分布：n个独立的是/非试验中成功的次数的离散概率分布  [当n=1时，二项分布就是伯努利分布]
* 负二项分布：成功r次的是/非试验中失败次数的离散概率分布 [注意区别二项分布]
* 伽玛分布：发生一次的平均时间为beta的事件发生alpha次所需时间的概率分布 [alpha=1就是指数分布]
* 贝塔分布：随机事件发生概率的概率分布 [与二项分布是共轭先验(先验分布和后验分布都是贝塔分布, 似然分布是二项分布)的, 
参数alpha代表发生次数，beta代表未发生次数]
* 卡方分布：k个独立的标准正态分布变量的平方和服从自由度为k的卡方分布 [卡方分布是一种特殊的伽马分布]
* 指数分布：随机事件的时间间隔的概率分布 [可以从泊松分布推导出来，自然求和得出伽马分布]
* 狄利克雷分布：由2种结果的伯努利试验导出的贝塔分布外推导k种结果的一般化


## 5. 抽样分布

**[三大抽样分布：卡方分布，t分布和F分布的简单理解](https://blog.csdn.net/anshuai_aw1/article/details/82735201)**


**卡方分布**

卡方分布（chi-square distribution[2], χ²-distribution，或写作χ²分布）:k个独立的标准正态分布变量的
平方和服从自由度为k的卡方分布。卡方分布是一种特殊的伽玛分布。

定义：

设X<sub>1<sub>, X<sub>2<sub>, ..., X<sub>n<sub>  i.i.d. ~N(0,1), 令![](http://latex.codecogs.com/gif.latex?X=\\sum_{i=1}^{n}X_{i}^{2}),
则称X是自由度为n的χ<sup>2<sup>变量，其分布称为自由度为n的χ<sup>2<sup>分布，记作 X ~ ![](http://latex.codecogs.com/gif.latex?\\chi_{n}^{2}).


性质：

1. 设随机变量X ~ ![](http://latex.codecogs.com/gif.latex?\\chi_{n}^{2}),则有`E(X)=n`; `Var(X)=2n`。
2. 设X1 ~ ![](http://latex.codecogs.com/gif.latex?\\chi_{n1}^{2})，X2 ~ ![](http://latex.codecogs.com/gif.latex?\\chi_{n2}^{2})，且X1和X2独立，
则`X1+X2 ~ ![](http://latex.codecogs.com/gif.latex?\\chi_{n1+n2}^{2})`。


**t分布**

定义：

设随机变量X ~ N(0, 1), Y ~ ![](http://latex.codecogs.com/gif.latex?\\chi_{n}^{2}), 且X和Y独立，则称

![](http://latex.codecogs.com/gif.latex?T=\\frac{X}{\\sqrt{Y/n}})

为自由度为n的t变量，其分布称为自由度为n的t分布，记为 `T~t<sub>n</sub>`

性质：

1. 若随机变量`T~t<sub>n</sub>`，则当n>=2时，`E(T) = 0`, 当n>=3时，`Var(T) = n/(n-2)`
2. 当n趋于正无穷时，t变量的极限分布为N(0,1)



***F分布*

定义：

设随机变量X ~ ![](http://latex.codecogs.com/gif.latex?\\chi_{m}^{2}), Y ~ ~ ![](http://latex.codecogs.com/gif.latex?\\chi_{n}^{2}),且X和Y独立，
则称：

![](http://latex.codecogs.com/gif.latex?F&space;=&space;\\frac{X/m}{Y/n})

为自由度分别是m和n的F变量，其分布称为F分布，记为 `F ~ F<sub>m,n</sub>`


性质：

1. 若Z ~ F<sub>m,n</sub>，则1/Z ~ F<sub>m,n</sub>
2. 若T ~ t<sub>n</sub>, 则T<sup>2</sup> ~ F<sub>1,n</sub>
3. F<sub>m,n</sub>(1-α) = 1/F<sub>m,n</sub>(α)



----


# 4. 统计检验


## 假设检验的4中方法

[假设检验-U检验、T检验、卡方检验、F检验](https://blog.csdn.net/qq_22592457/article/details/92982170)

1. 有关平均值参数u的假设检验

   根据是否已知方差,分为两类检验：U检验(Z检验)和T检验。

   如果**已知方差**，则使用U检验，如果**方差未知**则采取T检验。

2. 有关参数方差σ2的假设检验

   F检验是对两个正态分布的方差齐性检验，简单来说，就是检验两个分布的方差是否相等

3. 检验两个或多个变量之间是否关联

   卡方检验属于非参数检验，主要是比较两个及两个以上样本率（构成比）以及两个分类变量的关联性分
   析。根本思想在于比较理论频数和实际频数的吻合程度或者拟合优度问题



## U检验(Z检验)

Z检验是一般用于大样本(即样本容量大于30)平均值差异性检验的方法（总体的方差已知）。
它是用标准正态分布的理论来推断差异发生的概率，从而比较两个平均数的差异是否显著。

1. 如果检验一个样本平均数（X）与一个已知的总体平均数(μ0)的差异是否显著。其Z值计算公式为：

   ![](http://latex.codecogs.com/gif.latex?Z=\\frac{\\bar{X}-\\mu_{0}}{\\sigma/\\sqrt{n}})

   其中：X是检验样本的均值；μ0是已知总体的平均数；σ是总体的标准差；n是样本容量。

2. 如果检验来自两个的两组样本平均数的差异性，从而判断它们各自代表的总体的差异是否显著。
其Z值计算公式为：

   ![](http://latex.codecogs.com/gif.latex?Z=\\frac{\\bar{X_{1}}-\\bar{X_{2}}}{\\sqrt{\\sigma_{1}/n_{1}+\\sigma_{2}/n_{2}}})



**注意Z值和Z检验公式的区别**

Z值计算公式：![](http://latex.codecogs.com/gif.latex?Z=\\frac{x-\\mu}{\\sigma})

Z检验公式：![](http://latex.codecogs.com/gif.latex?Z=\\frac{\\bar{x}-\\mu}{\\sigma/\\sqrt{n}})

Z检验公式中，用样本平均值代替了x，用标准误代替了标准差sigma.



## T检验

亦称student t检验（Student's t test），主要用于样本含量较小（例如n<30），
总体标准差σ未知的正态分布。目的是用来比较样本均数所代表的未知总体均数μ和已知总体均数μ0。

T统计量计算公式：

   ![](http://latex.codecogs.com/gif.latex?T=\\frac{\\bar{X}-\\mu_{0}}{S_{\\bar{X}}}=\\frac{\\bar{X}-\\mu_{0}}{s/\\sqrt{n}})
   
   自由度df=n-1


1. 如果要评断一个总体中的小样本平均数与总体平均值之间的差异程度，其统计量T值的计算公式为：

   ![](http://latex.codecogs.com/gif.latex?T=\\frac{\\bar{X}-\\mu_{0}}{S_{\\bar{X}}}=\\frac{\\bar{X}-\\mu_{0}}{S/\\sqrt{n-1}})


2. 如果要评断两组样本平均数之间的差异程度，其统计量T值的计算公式为：

   ![](http://latex.codecogs.com/gif.latex?T=\\frac{\\bar{X_{1}}-\\bar{X_{2}}}{\\sqrt{\\frac{\\sum&space;x_{1}^{2}+\\sum&space;x_{2}^{2}}{n_{1}+n_{2}-2}}\\times&space;\\frac{n_{1}+n_{2}}{n_{1}\\times&space;n_{2}}})


## 卡方检验

* [MBAlib智库百科](https://wiki.mbalib.com/wiki/%E5%8D%A1%E6%96%B9%E6%A3%80%E9%AA%8C)
* [Wikipedia](https://zh.wikipedia.org/wiki/%E5%8D%A1%E6%96%B9%E6%A3%80%E9%AA%8C)
* [Python 卡方检验](https://blog.csdn.net/kk185800961/article/details/79054968)
* [几种常见的滥（乱）用卡方检验的情况](http://paper.dxy.cn/article/78383)
* [三维卡方检验](http://www.dxy.cn/bbs/thread/28440824#28440824) [三维卡方检验](http://www.dxy.cn/bbs/topic/25248045)

* [chi-square卡方检验的理解与应用](http://typename.net/statistics/chi-square/)
* [Does your data violate goodness of fit (chi-square) test assumptions?](https://www.quality-control-plan.com/StatGuide/gf-dist_ass_viol.htm)

* `scipy.stats.chi2_contingency`: 列联表中变量间的独立性卡方检验，如统计收入是否与性别有关。
* `scipy.stats.chisquare`: 单变量卡方检验(适合度卡方检验，卡方适度检验) (零假设：分类数据有相同频率)。
实际执行多项式试验而得到的观察次数，与虚无假设的期望次数相比较，称为卡方适度检验，即在于检验二者接近的程度，
利用样本数据以检验总体分布是否为某一特定分布的统计方法。


## 多变量逻辑回归分析

* **[如何理解回归模型中的"调整"和"独立作用"](https://www.mediecogroup.com/method_topic_article_detail/157/)**
* **[Python实现逻辑回归(Logistic Regression in Python)](https://blog.csdn.net/zj360202/article/details/78688070)**
* [logistic回归介绍](http://f.dataguru.cn/thread-847938-1-1.html)
* [Find p-value (significance) in scikit-learn LinearRegression](https://stackoverflow.com/questions/27928275/find-p-value-significance-in-scikit-learn-linearregression)
* [python logistic回归](https://www.jianshu.com/p/27c8b39c94f9)
* [5 个 W 元素 助你跨过 Logistic 回归分析的阶梯](http://paper.dxy.cn/article/503431)

参数意义
1. Logistic回归中的常数项（b0）表示，在不接触任何潜在危险／保护因素条件下，效应指标发生与不发生事件的概率之比的对数值。
2. Logistic回归中的回归系数（bi）表示，其它所有自变量固定不变，某一因素改变一个单位时，效应指标发生与不发生事件的概率
之比的对数变化值，即**OR或RR的对数值**。需要指出的是，**回归系数β的大小并不反映变量对疾病发生的重要性**，那么哪种因素
对模型贡献较大即与疾病联系最强呢? (InL(t-1)-InL(t))三种方法结果基本一致。
3. 存在因素间交互作用时，Logistic回归系数的解释变得更为复杂，应特别小心。
4. 模型估计出OR，当发病率较低时，OR≈RR，因此发病率高的疾病资料不适合使用该模型。另外，Logistic模型不能利用随访研究中的
时间信息，不考虑发病时间上的差异，因而只适于随访期较短的资料，否则随着随访期的延长，回归系数变得不稳定，标准误增加。



当遇到不均衡数据时，相对较为麻烦。sklearn能够通过weight参数来平衡数据，但不能像statsmodels一样输出p值，置信区间等统计
信息；而statsmodels又没有weight参数可以解决不平衡数据的问题，我们可以使用imblearn模块的过采样技术来平衡数据。

* [stackoverflow - Statsmodels Logistic Regression class imbalance](https://stackoverflow.com/questions/33605979/statsmodels-logistic-regression-class-imbalance)
* [imblearn - Over-sampling(过采样)](https://imbalanced-learn.readthedocs.io/en/stable/over_sampling.html)
* [imblearn - Under-sampling(欠采样)](https://imbalanced-learn.readthedocs.io/en/stable/under_sampling.html)
* [statsmodels-github - SUMM/ENH rare events, unbalanced sample, matching, weights #2701](https://github.com/statsmodels/statsmodels/issues/2701)

其实我们也可以在sklearn中手动去计算p值：
[Find p-value (significance) in scikit-learn LinearRegression](https://stackoverflow.com/questions/27928275/find-p-value-significance-in-scikit-learn-linearregression)


## 参数检验和非参数检验

* [关于显著性检验，你想要的都在这儿了！！（基础篇）](https://www.cnblogs.com/hdu-zsk/p/6293721.html)


| 编号 | 数据正态（参数检验） | 非正态（非参数检验） | 功能 |
| ---- | ---- | ---- | ---- |
| 1 | 单样本T检验 | 单样本Wilcoxon检验 | 与某数字对比差异 |
| 2 | 配对T检验 | 配对Wilcoxon检验 | 配对数据差异 |
| 3 | 独立样本T检验（也称T检验） | Mann-Whitney检验（也称非参数检验） | 2组数据的差异 |
| 4 | 单因素方差分析（也称方差分析） | Kruskal-Wallis检验（也称非参数检验） | 多组数据的差异 |
| 5 | 双因素方差分析(2-way ANOVA) | Friedman's 检验 | 双因素的差异 |

----

# 5. 回归

## 1. 线性回归

[Python环境下的8种简单线性回归算法](https://baijiahao.baidu.com/s?id=1588370178690958985&wfr=spider&for=pc)


----

# 6. 各种定理

* 大数定律：样本数量越多，则其算术平均值就有越高的概率接近期望值。
* 中心极限定理：在适当的条件下，大量相互独立随机变量的均值经适当标准化后依分布收敛于正态分布。

----

# python实现

* `scipy.stats.kstest()`: [python实现正态性检验](https://blog.csdn.net/QimaoRyan/article/details/72861387)
* `scipy.stats.boxcox()`: [python实现box-cox转换](https://blog.csdn.net/jylong1110/article/details/88308984)


## 【U检验/Z检验】已知z统计量，求p值

对于大样本数据（样本量 ≥\geq≥ 30），或者即使是小样本，但是知道其服从正态分布，
并且知道总体分布的方差时，需要用 z 检验。在 python 中，由于 scipy 包没有 z 检验，
我们只能用 statsmodels 包中的 ztest 函数。

1. 单样本z检验

```python
import statsmodels.stats.weightstats as sw

arr=[23,36,42,34,39,34,35,42,53,28,49,39,
46,45,39,38,45,27,43,54,36,34,48,36,
47,44,48,45,44,33,24,40,50,32,39,31]

# 检验数据均值是否是39
sw.ztest(arr, value=39)
(0.3859224924939799, 0.6995540720244979)
```

如果只知道测试统计量等于0.3859224924939799，怎么求p值？

```python
from scipy import stats

p = stats.norm.sf(0.3859224924939799) * 2   # 0.6995540720244979
```

2. 双样本z检验

```python
import statsmodels.stats.weightstats as sw

arr=[23,36,42,34,39,34,35,42,53,28,49,39,
46,45,39,38,45,27,43,54,36,34,48,36,
47,44,48,45,44,33,24,40,50,32,39,31]

arry = [41, 34, 36, 32, 32, 35, 33, 31, 35, 34,
37, 34, 31, 36, 37, 34, 33, 37, 33, 38,
38, 37, 34, 36, 36, 31, 33, 36, 37, 35,
33, 34, 33, 35, 34, 34, 34, 35, 35, 34]

sw.ztest(arr, arr2, value=0)
(3.775645601380307, 0.0001595937672736755)

# 根据统计量求p值：
stats.norm.sf(3.775645601380307) * 2  # 0.0001595937672736755
```



## 【T检验】已知t统计量，求p值

[使用Python scipy做统计检验--Student t-test](https://blog.csdn.net/myairforce1/article/details/78970203?utm_source=blogxgwz6)

1. 独立双样本t检验

知道原始数据，求t和p

```
from scipy import stats

a = [99.3, 98.7, 100.5, 101.2, 98.3, 99.7, 99.5, 102.1, 100.5]
b = [91.1, 93.7, 93.6, 96.1, 94.3, 92.2, 94.0, 95.7, 97.1]

stats.ttest_ind(a, b, equal_var=False)
Ttest_indResult(statistic=7.7232218210389565, pvalue=8.729735059423719e-07)
```

那么如果只知道t统计量，怎么求p呢？

```
t = 7.7232218210389565
dof = len(a) + len(b) - 2
p = (1 - stats.t.cdf(t, dof)) * 2  # 8.729735059423719e-07
# 或者
p = stats.t.sf(t, dof) * 2  # 8.729735059423719e-07
```

2. 配对双样本t检验

知道原始数据，求t和p

```python
from scipy import stats

a = [99.3, 98.7, 100.5, 101.2, 98.3, 99.7, 99.5, 102.1, 100.5]
b = [91.1, 93.7, 93.6, 96.1, 94.3, 92.2, 94.0, 95.7, 97.1]

stats.ttest_rel(a, b)
Ttest_relResult(statistic=10.845107419335658, pvalue=4.617509769582176e-06)
```

那么如果只知道t统计量，怎么求p呢？

```python
t = 10.845107419335658
dof = len(a) - 1
p = (1 - stats.t.cdf(t, dof)) * 2   #  4.617509769582176e-06
# 或者
p = stats.t.sf(t, dof) * 2  # 4.617509769582176e-06
```



----

# 疑问

1. 当独立性卡方检验不满足假设条件时(如最小期望值小于5)，可以使用Fisher's检验，
但是拟合优度卡方检验不满足假设条件时，该怎么办呢？

2. 在PGS中，分析影响胚胎异常率的因素有哪些(孕妇年龄, 排卵障碍, 精子障碍, 用药类型等)？
自变量都是分类变量，因变量是百分比。

3. 逻辑回归怎么校正非处理因素的影响？


----

# 中英文对照

* 连续型因变量 ：continuous dependent variable
* 分类型自变量 ：categorical independent variable
* 混杂变量 ：confounding variables 