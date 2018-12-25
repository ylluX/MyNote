# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [基本概念](#基本概念)
      * [灵敏度/特异度](#灵敏度特异度)
      * [损失函数(Loss function)/代价函数(成本函数)(Cost function)](#损失函数loss-function代价函数成本函数cost-function)
      * [分类/回归](#分类回归)
   * [模型](#模型)
      * [scikit-learn算法选择](#scikit-learn算法选择)
      * [数据预处理(归一化)](#数据预处理归一化)
      * [不均衡数据集处理](#不均衡数据集处理)
      * [核密度函数](#核密度函数)
      * [PCA](#pca)
      * [逻辑回归](#逻辑回归)
      * [梯度下降](#梯度下降)
      * [SVM](#svm)
      * [HMM](#hmm)
   * [深度学习](#深度学习)
      * [TensorFlow](#tensorflow)
   * [分布](#分布)
      * [泊松分布](#泊松分布)
   * [学习资料](#学习资料)
      * [视频资料](#视频资料)

<!-- Added by: luyl, at: 2018-12-25T17:38+08:00 -->

<!--te-->

----

# 基本概念

## 灵敏度/特异度

[Sensitivity and specificity](https://en.wikipedia.org/wiki/Sensitivity_and_specificity)

* 真阳性率(true positive rate, TPR)，又称为灵敏度(sensitivity)，即有病诊断阳性的概率   TPR = TP/(TP+FN)
* 真阴性率(true negative rate)，又称为特异度(specificity, SPC), 即有病诊断阳性的概率   SPC = TN/(TN+FP)
* 假阳性率(false positive rate, FPR)，又称为"误诊率"   FPR = FP/(FP+TN) = 1 - SPC
* 假阴性率(false negative rate, FNR)，又称为"漏诊率"   FNR = FN/(TP+FN) = 1 - TPR
* 阳性预测值(positive predictive value, PPV), 即诊断为阳性中有病的概率    PPV = TP/(TP+FP)
* 隐性预测值(negative predictive value, NPV), 即诊断为阴性中无病的概率    NPV = TN/(TN+FN)
* 准确率(accuracy)  = (TP+TN) / (TP+TN+FP+FN)
* 精确率(precision): P = TP / (TP+FP)
* 召回率(recall): R = TP / (TP+FN)

灵敏度：实际实际无病的人正确判断为真阳性的比例

特异度：实际有病的人正确判断为真阴性的比例


## 损失函数(Loss function)/代价函数(成本函数)(Cost function)

损失函数(Loss function)是定义在单个训练样本上的，也就是就算一个样本的误差，比如我们想要分类，就是预测的类别和实际类别的区别，
是一个样本的哦，用**L**表示

代价函数(Cost function)是定义在整个训练集上面的，是所有样本的误差的总和的平均，也就是损失函数的总和的平均，用**J**表示，有没
有这个平均其实不会影响最后的参数的求解结果。


## 分类/回归

* [机器学习中的回归(regression)与分类(classification)问题](https://blog.csdn.net/wspba/article/details/61927105)
* [回归(regression)与分类(classification)的区别](https://blog.csdn.net/u011630575/article/details/58676160)

输入变量与输出变量均为连续变量的预测问题是回归问题。输出变量为有限个离散变量的预测问题成为分类问题。

分类模型和回归模型本质一样，分类模型是将回归模型的输出离散化。

如果从training角度来看，分类模型和回归模型的目标函数不同，分类常见的是 log loss(对数损失函数), hinge loss(铰链损失函数), 
而回归是 square loss(平方损失函数)。



----


# 模型

## scikit-learn算法选择

![原文](https://scikit-learn.org/stable/_static/ml_map.png)
![中文](https://img-blog.csdn.net/20170624105439491?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZ3VhbmdfbWFuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

## 数据预处理(归一化)

* [处理离散型特征和连续型特征共存的情况 归一化 论述了对离散特征进行one-hot编码的意义](https://blog.csdn.net/lujiandong1/article/details/49448051)
* [利用python对包含离散型特征和连续型特征的数据进行预处理](https://blog.csdn.net/wotui1842/article/details/80697444)

拿到获取的原始特征，必须对每一特征分别进行归一化，比如，特征A的取值范围是[-1000,1000]，
特征B的取值范围是[-1,1].如果使用logistic回归，w1*x1+w2*x2，因为x1的取值太大了，所以x2
基本起不了作用。所以，必须进行特征的归一化，每个特征都单独进行归一化。

**连续型特征归一化的常用方法**

1. 线性放缩到[-1,1]
2. 线性放缩到[-1,1]

**离散型特征的处理方法**

离散型特征就是该特征对应的值不能进行大小比较，比如：职业，性别，国家等等

对于离散的特征基本就是按照one-hot编码，该离散特征有多少取值，就用多少维来表示该特征。
为什么使用one-hot编码来处理离散型特征，这是有理由的，不是随便拍脑袋想出来的！！！具体原因，
分下面几点来阐述： 

1. 使用one-hot编码，将离散特征的取值扩展到了欧式空间，离散特征的某个取值就对应欧式空间的某个点。
2. 将离散特征通过one-hot编码映射到欧式空间，是因为，在回归，分类，聚类等机器学习算法中，
特征之间距离的计算或相似度的计算是非常重要的，而我们常用的距离或相似度的计算都是在欧式
空间的相似度计算，计算余弦相似性，基于的就是欧式空间。
3. 离散型特征使用one-hot编码，确实会让特征之间的距离计算更加合理。比如，有一个离散型特征，
代表工作类型，该离散型特征，共有三个取值，不使用one-hot编码，其表示分别是x_1 = (1), 
x_2 = (2), x_3 = (3)。两个工作之间的距离是，(x_1, x_2) = 1, d(x_2, x_3) = 1, d(x_1, x_3) = 2。
那么x_1和x_3工作之间就越不相似吗？显然这样的表示，计算出来的特征的距离是不合理。那如果使用
one-hot编码，则得到x_1 = (1, 0, 0), x_2 = (0, 1, 0), x_3 = (0, 0, 1)，那么两个工作之间的距
离就都是sqrt(2).即每两个工作之间的距离是一样的，显得更合理
4. 将离散型特征进行one-hot编码的作用，是为了让距离计算更合理，但如果特征是离散的，并且不用
one-hot编码就可以很合理的计算出距离，那么就没必要进行one-hot编码，比如，该离散特征共有1000
个取值，我们分成两组，分别是400和600,两个小组之间的距离有合适的定义，组内的距离也有合适的定
义，那就没必要用one-hot 编码
 
离散特征进行one-hot编码后，编码后的特征，其实每一维度的特征都可以看做是连续的特征。就可以跟对
连续型特征的归一化方法一样，对每一维特征进行归一化。比如归一化到[-1,1]或归一化到均值为0,方差为1

基于树的方法是不需要进行特征的归一化，例如随机森林，bagging 和 boosting等。基于参数的模型或基
于距离的模型，都是要进行特征的归一化。


## 不均衡数据集处理

* [不平衡数据集下的SVM算法研究](https://blog.csdn.net/u011414200/article/details/47310795)
* [数据不均衡问题的解决](https://blog.csdn.net/sunflower_sara/article/details/81055033)
* [SVM训练时候样本不均衡怎么设置惩罚项](https://blog.csdn.net/qq_22625309/article/details/76256381?locationNum=8&fps=1)

从技术角度上说，任何在不同类之间展现出不等分布的样本集都应该被认为是不均衡的，并且应该展现出
明显的不平衡特征。具体来说，这种不均衡形式被称为类间不均衡，常见的多数类与少数类比例是100:1，
1000:1，10000:1

有时对少数类错分情况的后果很严重，比如癌症患者被误诊为健康人。所以需要的分类器应该是在不严重
损失多数类精度的情况下，在少数类上获得尽可能高的精度

同时也暗示着使用单一的评价准则，例如全局精度或是误差率，是不能给不均衡问题提供足够的评价信息。
因此利用含有更多信息的评价指标，例如接收机特性曲线、精度-recall曲线和代价曲线

样本不均衡的程度不是阻碍分类学习的唯一因素，样本集的复杂度也是导致分类性能恶化的重要因素，
另外相对不平衡比例的增大也可能使分类性能进一步恶化 。其中样本集复杂度是广义的术语，它包括重叠、
缺少代表性样本、类别间分离程度小等

```
在sklearn的SVC中，可用通过class_weight参数来处理不均衡数据集，该参数的值为字典类型或者
'balanced'字符串，默认为None.

每个类别分别设置不同的惩罚参数C，如果没有给，则会给所有类别都给C=1，即前面参数指出的参数C.
如果给定参数'balanced'，则使用y的值自动调整与输入数据中的类频率成反比的权重。
```


## 核密度函数

* [核密度估计 Kernel Density Estimation(KDE)](https://blog.csdn.net/unixtch/article/details/78556499)

![核函数的图形](https://img-blog.csdn.net/20171116222009645?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdW5peHRjaA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## PCA

* [sklearn_PCA实践](https://blog.csdn.net/Huangyi_906/article/details/76438885)
* [Python scikit-learn 学习笔记—PCA+SVM人脸识别](https://blog.csdn.net/leo_is_ant/article/details/45766315)


## 逻辑回归

* [逻辑回归（Logistic Regression, LR）简介](https://blog.csdn.net/jk123vip/article/details/80591619)
* [逻辑回归的理解](https://blog.csdn.net/t46414704152abc/article/details/79574003)
* [logistic回归与判别分析](https://www.jianshu.com/p/8afbf60156d2)
* [逻辑回归（Logistic Regression）](https://blog.csdn.net/liulina603/article/details/78676723)

逻辑回归虽然名字叫做回归，但实际上却是一种分类学习方法。 

线性回归完成的是回归拟合任务，而对于分类任务，我们同样需要一条线，但不是去拟合每个数据点，而是把不同类别的样本区分
开来。

对于二分类问题，y∈{0,1}，1表示正例，0表示负例。逻辑回归是在线性函数θ<sup>T</sup>x输出预测实际值的基础上，
寻找一个假设函数hθ(x)=g(θ<sup>T</sup>x)，将实际值映射到到0，1之间，如果hθ(x)>=0.5，则预测y=1，及y属于正例；
如果hθ(x)<0.5，则预测y=0，即y属于负例。

逻辑回归中选择对数几率函数（logistic function）作为激活函数，对数几率函数是Sigmoid函数（形状为S的函数）的重要代表


## 梯度下降

* [深入浅出--梯度下降法及其实现](https://www.jianshu.com/p/c7e642877b0e)
* [一文看懂常用的梯度下降算法](https://blog.csdn.net/u013709270/article/details/78667531/)
* [最清晰的讲解各种梯度下降法原理与Dropout](https://baijiahao.baidu.com/s?id=1613121229156499765&wfr=spider&for=pc)

## SVM

* [SVM支持向量机分类模型SVC理论+python sklean.svm实践](https://blog.csdn.net/SummerStoneS/article/details/78551757)
* [SVM详解(包含它的参数C为什么影响着分类器行为)-scikit-learn拟合线性和非线性的SVM](https://blog.csdn.net/xlinsist/article/details/51311755)
* [用实验理解SVM的核函数和参数](https://blog.csdn.net/sigai_csdn/article/details/80693951)
* [sklearn-SVC实现与类参数](https://www.cnblogs.com/xiaotan-code/p/6700290.html)

**核映射与核函数**

* [核函数的由来](https://blog.csdn.net/huang1024rui/article/details/51510611)

通过核函数，支持向量机可以将特征向量映射到更高维的空间中，使得原本线性不可分的数据在映射之后的
空间中变得线性可分。假设原始向量为x，映射之后的向量为z，这个映射为：

> z = φ(x)

在实现时不需要直接对特征向量做这个映射，而是用核函数对两个特征向量的内积进行变换，这样做等价于
先对向量进行映射然后再做内积：

> K(x<sub>i</sub>, x<sub>j</sub>) = K(x<sub>i</sub><sup>T</sup>x<sub>j</sub>) = φ(x<sub>i</sub>)<sup>T</sup>φ(x<sub>j</sub>)

在这里K为核函数。常用的非线性核函数有多项式核，高斯核（也叫径向基函数核，RBF）。下表列出了各种
核函数的计算公式：

| 核函数 | 计算公式 |
| ---- | ---- |
| 线性核(linear) | K(x<sub>i</sub>, x<sub>j</sub>) = x<sub>i</sub><sup>T</sup>x<sub>j</sub> |
| 多项式核(poly) | K(x<sub>i</sub>, x<sub>j</sub>) = (γx<sub>i</sub><sup>T</sup>x<sub>j</sub> + b)<sup>d</sup> |
| 径向基函数(高斯)核(RBF) | K(x<sub>i</sub>, x<sub>j</sub>) = exp(-γ\|\|x<sub>i</sub> - x<sub>j</sub>\|\|<sup>2</sup>) |
| sigmoid核 | K(x<sub>i</sub>, x<sub>j</sub>) = tanh(γx<sub>i</sub><sup>T</sup>x<sub>j</sub> + b) |


其中，γ(核系数), b(独立项)，d(深度)为人工设置的参数，d是一个正整数，为正实数，b为非负实数。

尽管最佳核函数的选择一般与问题自身有关，但对普遍问题还是有规律可循的，建议初学者在通常情况下，
优先考虑径向基核函数（RBF）.主要基于以下考虑：

1. 作为一种对应于非线性映射的核函数，RBF 能够处理非线性可分的问题

2. 线性核函数时 RBF 核函数的一种特例，即通过适当地选择参数 (γ,C)(γ,C)，RBF 核函数总可以得到与错误代价参数 
C 的线性核函数相同的效果，反之当然不成立

3. 在选择某些参数的情况下，Sigmoid 核函数的行为也类似于 RBF 核函数,而且选择 Sigmoid 核函数就有 2 个与之有
关的参数 b、c 需要确定。

4. 多项式核函数需要计算内积，而这有可能产生溢出之类的计算问题。


**罚分因子**

C越大，我们越倾向于没有松弛变量，即模型会尽可能分对每一个点，反之，C越小，模型的泛化能力越强。


## HMM

* [一文搞懂HMM（隐马尔可夫模型）](https://www.cnblogs.com/skyme/p/4651331.html)
* [隐马尔可夫模型（一）](https://www.cnblogs.com/bigmonkey/p/7230668.html)
* [隐马尔可夫模型](https://blog.csdn.net/u011630575/article/details/79140106)
* [隐马尔可夫模型攻略](http://www.leexiang.com/hidden-markov-model)

**隐马尔可夫模型作了两个基本假设**

1. 齐次马尔可夫性假设，即假设隐藏的马尔可夫链在任意时刻t的状态只依赖于其前一时刻的状态，与其他时刻的状态及观测无关。
2. 观测独立性假设，即假设任意时刻的观测只依赖于该时刻的马尔可夫链的状态，与其他观测及状态无关。

**隐马尔可夫模型5元组**

一个 HMM 可用一个5元组 { N, M, π，A，B } 表示，其中：

* N 表示隐藏状态的数量，我们要么知道确切的值，要么猜测该值；
* M 表示可观测状态的数量，可以通过训练集获得；
* π={πi} 为初始状态概率；代表的是刚开始的时候各个隐藏状态的发生概率；
* A={aij}为隐藏状态的转移矩阵；N*N维矩阵，代表的是第一个状态到第二个状态发生的概率；
* B={bij}为混淆矩阵，N*M矩阵，代表的是处于某个隐状态的条件下，某个观测发生的概率。

**隐马尔可夫模型的3个基本问題**

1. 概率计算问题。给定模型和观测序列,计算在模型下观测序列出现的概率。 [遍历法、向前算法、向后算法]
2. 学习问题。己知观测序列,估计模型参数，使得在该模型下观测序列概率最大。 [鲍姆-韦尔奇算法(EM算法)]
即用极大似然估计的方法估计参数。
3. 预测问题，也称为解码（decoding)问题。已知模型和观测序列，求对给定观测序列条件概率最大的状态序列。
即给定观测序列，求最有可能的对应的状态序列。[近似算法、维特比算法(Viterbi)]

----

# 深度学习

## TensorFlow

* [Simple and ready-to-use tutorials for TensorFlow](https://github.com/osforscience/TensorFlow-Course#why-use-tensorflow)


----

# 分布

## 泊松分布

* [如何通俗理解泊松分布？](https://blog.csdn.net/ccnt_2012/article/details/81114920)

----

# 学习资料

## 视频资料

* 斯坦福大学机器学习-吴恩达, [学习笔记](https://blog.csdn.net/hujingshuang/article/category/3277895)
