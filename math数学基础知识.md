
# 目录
<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [1. 线性代数](#1-线性代数)
      * [1.1 矩阵的运算及其运算规则](#11-矩阵的运算及其运算规则)
   * [2. 常见概念](#2-常见概念)
      * [2.1 微积分](#21-微积分)
      * [2.2 卷积](#22-卷积)
      * [2.3 傅里叶变换](#23-傅里叶变换)
      * [2.4 欧拉公式](#24-欧拉公式)
      * [2.5 泰勒公式](#25-泰勒公式)
      * [2.6 多项式](#26-多项式)
      * [2.7 内积和外积](#27-内积和外积)
   * [3 常见问题](#3-常见问题)
      * [3.1 范数与距离的关系](#31-范数与距离的关系)
   * [LaTeX](#latex)
      * [常见问题](#常见问题)
         * [latex 加减号堆积，放在一起](#latex-加减号堆积放在一起)
         * [latex 写矩阵](#latex-写矩阵)
      * [latex输入斜体](#latex输入斜体)
   * [参考资料](#参考资料)
      * [1. 华夏大地教育网](#1-华夏大地教育网)
      * [2 python线性代数](#2-python线性代数)
      * [3. 马同学高等数学](#3-马同学高等数学)
   * [希腊字母](#希腊字母)

<!-- Added by: luyl, at: 2018-12-25T17:38+08:00 -->

<!--te-->

----


# 1. 线性代数


> 首先得先弄清矩阵的概念：一个矩阵代表的是一个线性变换规则，而一个矩阵的乘法运行代表的是一个变换。


## 1.1 矩阵的运算及其运算规则

[6.5 矩阵的运算及其运算规则](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0605.html)

**基本概念**

1. 方阵的`单位阵`(`E`)

    三阶单位阵：![](http://latex.codecogs.com/gif.latex?\\textit{E}=$$\\begin{Bmatrix}1&0&0\\\\0&1&0\\\\0&0&1\\end{Bmatrix}$$)

    方阵`A`和它同阶的单位阵作乘积，结果仍为`A`，即`AE = EA = A`. 单位阵在矩阵乘法中的作用相当于数1在我们普通乘法中的作用．

2. 对称矩阵

    如果方阵满足![](http://latex.codecogs.com/gif.latex?{A^\'}=A), 则称`A`为对称矩阵.

    对称矩阵的特点是：它的元素以主对角线为对称轴对应相等．

3. 可逆矩阵与逆矩阵(A<sup>-1</sup>)

    矩阵A为n阶方阵，若存在n阶矩阵B，使得矩阵A、B的乘积为单位阵(E)，则称A为可逆阵，B为A的逆矩阵
    (![](https://latex.codecogs.com/gif.latex?A^{-1}))。
    若方阵的逆阵存在，则称为`可逆矩阵`或`非奇异矩阵`，且其逆矩阵唯一。

    性质：
    * 若A为可逆矩阵，则A的逆矩阵是唯一的。
    * 设A、B是数域P上的n阶矩阵，![](https://latex.codecogs.com/gif.latex?k\in&space;P)。
        * 若A可逆，则![](https://latex.codecogs.com/gif.latex?A^{-1})和![](http://latex.codecogs.com/gif.latex?A^T)也可逆,
且![](https://latex.codecogs.com/gif.latex?((A)^{-1})^{-1}=A), ![](https://latex.codecogs.com/gif.latex?(A^{T})^{-1}=(A^{-1})^{T})
        * 若A可逆，则kA可逆 <=> k!=0,且![](https://latex.codecogs.com/gif.latex?(kA)^{-1}=\frac{1}{k}(A)^{-1})
        * A、B均可逆 <=> ![](https://latex.codecogs.com/gif.latex?(AB)^{-1}=(B)^{-1}(A)^{-1})。

4. 奇异矩阵
    [百度百科](https://baike.baidu.com/item/%E5%A5%87%E5%BC%82%E7%9F%A9%E9%98%B5/9658459?fr=aladdin)
    奇异矩阵是线性代数的概念，就是该矩阵的秩不是满秩。首先，看这个矩阵是不是方阵（即行数和列数相等的矩阵。
    若行数和列数不相等，那就谈不上奇异矩阵和非奇异矩阵）。然后，再看**此矩阵的行列式|A|是否等于0，若等于0，
    称矩阵A为奇异矩阵；若不等于0，称矩阵A为非奇异矩阵**。 同时，由**|A|≠0可知矩阵A可逆**，这样可以得出另外一个
    重要结论:**可逆矩阵就是非奇异矩阵，非奇异矩阵也是可逆矩阵**。 如果**A为奇异矩阵，则AX=0有无穷解，AX=b有无穷解
    或者无解。如果A为非奇异矩阵，则AX=0有且只有唯一零解，AX=b有唯一解**。


5. 伴随矩阵(A*)

    [百度百科](https://baike.baidu.com/item/%E4%BC%B4%E9%9A%8F%E7%9F%A9%E9%98%B5/10034983)

    在线性代数中，一个方形矩阵的伴随矩阵是一个类似于逆矩阵的概念 。如果二维矩阵可逆，那么它的逆矩阵和它的伴随矩阵之间
    只差一个系数，对多维矩阵不存在这个规律。然而，伴随矩阵对不可逆的矩阵也有定义，并且不需要用到除法

6. 矩阵的行列式(|A|)

    [百度百科](https://baike.baidu.com/item/%E7%9F%A9%E9%98%B5%E8%A1%8C%E5%88%97%E5%BC%8F/18882017?fr=aladdin)

    矩阵行列式(determinant of a matrix)是指矩阵的全部元素构成的行列式，设A=(aij)是数域P上的一个n阶矩阵，
    则所有A=(aij)中的元素组成的行列式称为矩阵A的行列式，记为|A|或det(A)。若A，B是数域P上的两个n阶矩阵，
    k是P中的任一个数，则|AB|=|A||B|，|kA|=kn|A|，|A*|=|A|<sup>n-1</sup>，其中A*是A的伴随矩阵；
    若A是可逆矩阵，则|A<sup>-1</sup>|=|A|<sup>-1</sup>。

***可逆矩阵(满秩矩阵) = 非奇异矩阵：行列式det(A) != 0 ***
***不可逆矩阵(欠秩矩阵) = 奇异矩阵：行列式det(A) == 0 ***

**矩阵的加法与减法**

1. 运算法则

    设矩阵

    ![](http://latex.codecogs.com/gif.latex?\\textit{A}=$$\\begin{Bmatrix}a_{11}&a_{12}&\\cdots&a_{1n}\\\\a_{21}&a_{22}&\\cdots&a_{2n}\\\\\\vdots&\\vdots&\\ddots&\\vdots\\\\a_{m1}&a_{m2}&\\cdots&a_{mn}\\end{Bmatrix}$$)    ![](http://latex.codecogs.com/gif.latex?\\textit{B}=$$\\begin{Bmatrix}b_{11}&b_{12}&\\cdots&b_{1n}\\\\b_{21}&b_{22}&\\cdots&b_{2n}\\\\\\vdots&\\vdots&\\ddots&\\vdots\\\\b_{m1}&b_{m2}&\\cdots&b_{mn}\\end{Bmatrix}$$)

    , 则

    ![](http://latex.codecogs.com/gif.latex?\\textit{A}\\pm\\textit{B}=$$\\begin{Bmatrix}a_{11}{\\pm}b_{11}&a_{12}{\\pm}b_{12}&\\cdots&a_{1n}{\\pm}b_{1n}\\\\a_{21}{\\pm}b_{21}&a_{22}{\\pm}b_{22}&\\cdots&a_{2n}{\\pm}b_{2n}\\\\\\vdots&\\vdots&\\ddots&\\vdots\\\\a_{m1}{\\pm}b_{m1}&a_{m2}{\\pm}b_{m2}&\\cdots&a_{mn}{\\pm}b_{mn}\\end{Bmatrix}$$)

    简言之，两个矩阵相加减，即它们相同位置的元素相加减！

    注意：只有对于两个行数、列数分别相等的矩阵（即同型矩阵），加减法运算才有意义，即加减运算是可行的．

    </br>

2.  运算性质 （假设运算都是可行的）

    满足交换律和结合律

    * **交换律** : `A + B = B + A`
    * **结合律** : `( A + B ) + C = A + ( B + C )`


**矩阵与数的乘法**

1. 运算规则

    数`λ`乘矩阵`A`，就是将数`λ`乘矩阵`A`中的每一个元素，记为`λA`或`Aλ`

    特别地，称`-A`称为![](http://latex.codecogs.com/gif.latex?A=(a_{ij})_{m{\times}s})的负矩阵．

2. 运算性质 

    满足结合律和分配律

    * **结合律**： `(λμ)A=λ(μA)` ； `(λ+μ)A =λA+μA`．
    * **分配律**： `λ(A+B)=λA+λB`．


**矩阵与矩阵的乘法**

1. 运算规则

    设![](http://latex.codecogs.com/gif.latex?A=(a_{ij})_{m{\times}s})，![](http://latex.codecogs.com/gif.latex?B=(b_{ij})_{s{\times}n})，则`A`与`B`的乘积是这样一个矩阵：
    * 行数与（左矩阵）`A`相同，列数与（右矩阵）`B`相同，即![](http://latex.codecogs.com/gif.latex?C=(c_{ij})_{m{\times}n})．
    * `C`的第`i`行第`j`列的元素由`A`的第`i`行元素与`B`的第`j`列元素对应相乘，再取乘积之和．

2. 运算性质

    矩阵乘法不满足交换律, 即`AB`不一定等于`BA`

    两个非零矩阵的乘积可以是零矩阵．由此若`AB=0`，不能得出`A=0`或`B=0`的结论．

    * **结合律** : `(AB)C = A(BC)`; `(λA)B = λ(AB) = A(λB)`
    * **分配律** : `A(B±C) = AB ± AC`(左分配律); `(B±C)A = BA ± CA`(右分配律)

3. 方阵的幂

    ![](http://latex.codecogs.com/gif.latex?A^k)表示`k`个`A`的连乘积

    ![](http://latex.codecogs.com/gif.latex?A^0=E)


**矩阵的转置**

1. 定义

    将矩阵`A`的行换成同序号的列所得到的新矩阵称为矩阵`A`的`转置矩阵`，记作![](http://latex.codecogs.com/gif.latex?A^\')或![](http://latex.codecogs.com/gif.latex?A^T)

2. 运算性质（假设运算都是可行的）

    * `(A')' = A`
    * `(A+B)' = A' + B'`
    * `(AB)' = B'A'`
    * `(λA)' = λA'`



----

# 2. 常见概念

## 2.1 微积分

* [微分和导数的关系是什么？两者的几何意义有什么不同？为什么要定义微分?](https://www.zhihu.com/question/22199657?rf=35793939)
* [帮你理解积分与求导到底是什么](https://blog.csdn.net/songkai320/article/details/51920514)

## 2.2 卷积

* [理解图像卷积操作的意义](https://blog.csdn.net/chaipp0607/article/details/72236892)
* [如何理解卷积：信号处理、图像处理中的应用](https://blog.csdn.net/u011447369/article/details/53515003)
* [最容易理解的对卷积(convolution)的解释](https://blog.csdn.net/bitcarmanlee/article/details/54729807)

## 2.3 傅里叶变换

![傅里叶变换](https://gss2.bdstatic.com/-fo3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D223/sign=9bd514392a34349b70066987faeb1521/203fb80e7bec54e78829ef3dbb389b504ec26ac8.jpg)

* [深入浅出的讲解傅里叶变换（真正的通俗易懂）](https://blog.csdn.net/l494926429/article/details/51818012)
* [如何理解傅里叶变换公式？](https://www.zhihu.com/question/19714540/answer/14738630)
* [告诉你一个真实的傅里叶](http://baijiahao.baidu.com/s?id=1584947709400738822&wfr=spider&for=pc)

**傅里叶级数**在时域是一个周期且连续的函数，而在频域是一个非周期离散的函数。

**傅里叶变换**则是将一个时域非周期的连续信号，转换为一个在频域非周期的连续信号。


## 2.4 欧拉公式

> e^x = cosx + isinx

令x=π 带入上式，则可以得出欧拉恒等式：

> e^πi + 1 = 0

其中e是自然指数的底， i是虚数单位， π是圆周率

欧拉公式是数学里最令人着迷的公式之一，它将数学里最重要的几个常数联系在一起，两个超越数：自然对数的底e，圆周率π；两个单位：虚数单位i和自然数的单位1，以及数学里常见的0.

欧拉公式将指数函数的定义域扩大到了复数域，建立了三角函数和指数函数的关系，被誉为“数学中的天桥”。形式简单，结果惊人，欧拉本人都把这个公式刻在皇家科学院的大门上，看来必须好好推敲一番。 

* [如何通俗地解释欧拉公式](https://www.matongxue.com/madocs/8.html)
* [欧拉公式——真正的宇宙第一公式](http://www.360doc.com/content/17/1212/10/2633_712327701.shtml)

## 2.5 泰勒公式

> 泰勒公式一句话描述：就是用多项式函数去逼近光滑函数。

泰勒公式最直接的一个应用就是用于计算，计算机一般都是把`sin(x)`进行泰勒展开进行计算的

* [如何通俗地解释泰勒公式？](http://www.matongxue.com/madocs/7.html)

## 2.6 多项式

* [wikipedia - Polynomial](https://en.wikipedia.org/wiki/Polynomial)
* [多项式ppt](https://wenku.baidu.com/view/720b07a0d4bbfd0a79563c1ec5da50e2534dd160.html)


## 2.7 内积和外积

* [向量内积（点乘）和外积（叉乘）概念及几何意义](https://www.cnblogs.com/gxcdream/p/7597865.html)


----

# 3 常见问题

## 3.1 范数与距离的关系

[范数与距离的关系](https://www.cnblogs.com/wt869054461/p/5935961.html)

**范数**

向量的范数可以简单形象的理解为向量的长度，或者向量到零点的距离，或者相应的两个点之间的距离。

向量的范数定义：向量的范数是一个函数||x||,满足非负性||x|| >= 0，齐次性||cx|| = |c| ||x|| ，三角不等式||x+y|| <= ||x|| + ||y||。

常用的向量的范数：
* L1范数:  ||x|| 为x向量各个元素绝对值之和。
* L2范数:  ||x||为x向量各个元素平方和的1/2次方，L2范数又称Euclidean范数或者Frobenius范数
* Lp范数:  ||x||为x向量各个元素绝对值p次方和的1/p次方
* L∞范数:  ||x||为x向量各个元素绝对值最大那个元素的绝对值
* 椭球向量范数: ||x||A  = sqrt[T(x)Ax]， T(x)代表x的转置。
	定义矩阵C 为M个模式向量的协方差矩阵， 设C’是其逆矩阵，则Mahalanobis距离定义为||x||C’  = sqrt[T(x)C’x], 这是一个关于C’的椭球向量范数。

**距离**
*欧式距离（对应L2范数）*：最常见的两点之间或多点之间的距离表示法，又称之为欧几里得度量，它定义于欧几里得空间中。n维空间中两个点x1(x11,x12,…,x1n)与 x2(x21,x22,…,x2n)间的欧氏距离：

![欧式距离公式](http://img.my.csdn.net/uploads/201211/20/1353399644_3809.png)

也可以用表示成向量运算的形式：

![欧式距离公式](http://img.my.csdn.net/uploads/201211/20/1353399664_2255.png)

*曼哈顿距离*：曼哈顿距离对应L1-范数，也就是在欧几里得空间的固定直角坐标系上两点所形成的线段对轴产生的投影的距离总和。例如在平面上，坐标（x1, y1）的点P1与坐标（x2, y2）的点P2的曼哈顿距离为：
![曼哈顿距离公式](http://img.my.csdn.net/uploads/201211/20/1353398955_7627.png)，要注意的是，曼哈顿距离依赖座标系统的转度，而非系统在座标轴上的平移或映射。

*切比雪夫距离*，若二个向量或二个点x1和x2，其坐标分别为(x11, x12, x13, ... , x1n)和(x21, x22, x23, ... , x2n)，则二者的切比雪夫距离为：d = max(|x1i - x2i|)，i从1到n。对应L∞范数。

*闵可夫斯基距离(Minkowski Distance)*，闵氏距离不是一种距离，而是一组距离的定义。对应Lp范数，p为参数。
闵氏距离的定义：两个n维变量（或者两个n维空间点）x1(x11,x12,…,x1n)与 x2(x21,x22,…,x2n)间的闵可夫斯基距离定义为： 

![闵可夫斯基距离定义](http://img.my.csdn.net/uploads/201211/20/1353400356_6225.png)

其中p是一个变参数。

	当p=1时，就是曼哈顿距离，

	当p=2时，就是欧氏距离，

	当p→∞时，就是切比雪夫距离，       

根据变参数的不同，闵氏距离可以表示一类的距离。 

*Mahalanobis距离*：也称作马氏距离。在近邻分类法中，常采用欧式距离和马氏距离。


----

# LaTeX

[LaTeX在线编辑器](https://www.codecogs.com/latex/eqneditor.php)

## 常见问题

### latex 加减号堆积，放在一起

latex 加减号放在一起，经常用来表示上下波动，命令为：`\pm`

### latex 写矩阵

[[CSDN_Markdown] 使用LaTeX写矩阵](https://blog.csdn.net/bendanban/article/details/44221279)

## latex输入斜体

LaTeX的每种字体有5种属性：编码、族，形状，系列和尺寸。

下面讨论常用的几个：形状，系列，尺寸。

1. 形状指的是倾斜和高矮。

* `\upshape` 切换成直立的字体
* `\itshape` 切换成意大利斜体
* `\slshape` 切换成成为 slanted 的斜体
* `\scshape` 切换成小体大写

2. 系列是指字体的宽度和权重。权重刻画了笔画的粗细。

* `\mdseries` 切换到中等权重
* `\bfseries` 切换到粗体

以上这些皆为声明，在遇到新的声明前一直起作用。

为了限定其作用，可以放到一个环境中，如：`\begin{upshape}使用该属性的文本\end{upshape}`

还有一个非常重要的声明\normalfont，它把除了字体尺寸以外的属性都设置成默认值，即中等权重的直立的罗马字体。

下面是相应的字体命令。

* 显示直立文本： `\textup{文本}`
* 意大利斜体： `\textit{美元符 文本 美元符}`
* slanted斜体： `\textsl{文本}`
* 显示小体大写文本： 　`\textsc{文本}`
* 中等权重： `\textmd{文本}`
* 加粗命令： `\textbf{文本}`
* 默认值： `\textnormal{文本}`

这些命令可以组合使用, 例如需要加粗和斜体, 则使用`\textbf{\textbf{文本}}`

注意：上述命令中的“文本”不能位于两个段落中。最常用的就是`\textup`、`\textsl`和`\textbf`了。

3. 设置字体大小命令由小到大依次为：

`\tiny`,`\scriptsize`, `\footnotesize`, `\small`, `\normalsize`, `\large`, `\Large`, `\LARGE`, `\huge`, `\Huge`


----

# 参考资料

## 1. 华夏大地教育网

* [1.1 预备知识](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0101.html)
* [1.2 函数概念及基本初等函数](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0102.html)
* [1.3 函数的几种特性](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0103.html)
* [1.4 反函数和复合函数](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0104.html)
* [1.5 初等函数](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0105.html)
* [2.1 数列及其极限](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0201.html)
* [2.2 数项级数的基本概念](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0202.html)
* [2.4 无穷小量和无穷大量](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0204.html)
* [2.5 函数的连续性](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0205.html)
* [3.1 导数的概念](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0301.html)
* [3.2 求导数的公式与法则](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0302.html)
* [3.3 几类特殊函数的求导方法](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0303.html)
* [3.4 高阶导数](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0304.html)
* [3.5 微分及其运算](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0305.html)
* [4.1 微分中值定理](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0401.html)
* [4.2 洛比达法则](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0402.html)
* [4.3 函数的单调性](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0403.html)
* [4.4 函数的极值及其求法](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0404.html)
* [4.5 函数的最大值最小值及其应用](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0405.html)
* [4.6 曲线的凹凸性和拐点](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0406.html)
* [4.7 函数的渐近线](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0407.html)
* [5.1 原函数与不定积分的概念](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0501.html)
* [5.2 不定积分的换元法](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0502.html)
* [5.3 分部积分法](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0503.html)
* [5.4 微分方程初步](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0504.html)
* [5.5 定积分的概念及其几何意义](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0505.html)
* [5.6 定积分的基本性质](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0506.html)
* [5.7 定积分的基本公式(牛顿－莱布尼兹公式)](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0507.html)
* [5.8 定积分的换元法与分部积分法](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0508.html)
* [5.9 无穷限反常积分](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0509.html)
* [5.10 定积分的应用](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0510.html)
* [5.11 原函数与不定积分的概念](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0511.html)
* [6.1 二阶和三阶行列式](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0601.html)
* [6.2 行列式的性质和计算](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0602.html)
* [6.3 矩阵的概念及矩阵的初等行变换](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0603.html)
* [6.4 解线性方程组的消元法](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0604.html)
* [6.5 矩阵的运算及其运算规则](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0605.html)
* [6.6 逆矩阵](http://www2.edu-edu.com.cn/lesson_crs78/self/j_0022/soft/ch0606.html)

## 2 python线性代数

* [1 矩阵操作](https://jingyan.baidu.com/article/acf728fd277fe5f8e410a353.html)
* [2 矩阵乘法](http://jingyan.baidu.com/article/e8cdb32b65978837042bad5b.html)
* [3 矩阵转置](http://jingyan.baidu.com/article/49ad8bce73ee325835d8fa5b.html)
* [4 方阵的迹](http://jingyan.baidu.com/article/e9fb46e19329177520f7665b.html)
* [5 方阵的行列式计算方法](http://jingyan.baidu.com/article/f54ae2fcd9bcb91e93b8495c.html)
* [6 逆矩阵/伴随矩阵](http://jingyan.baidu.com/article/6dad5075cea061a122e36e5f.html)
* [7 解多元一次方程](http://jingyan.baidu.com/article/f3e34a128c93aef5eb653502.html)
* [8 计算矩阵距离](http://jingyan.baidu.com/article/f3ad7d0ff84b1609c3345b03.html)
* [9 求矩阵的秩](http://jingyan.baidu.com/article/86fae346b49d653c49121a05.html)
* [10 求方阵的特征值特征向量](http://jingyan.baidu.com/article/4665065801c624f549e5f80f.html)
* [11 判断正定矩阵](http://jingyan.baidu.com/article/48a42057c71ddaa92425040f.html)
* [12 求协方差矩阵](http://jingyan.baidu.com/article/e4d08ffdd1d66b0fd2f60d0f.html)
* [13 求相关矩阵](http://jingyan.baidu.com/article/a378c9609b5849b328283093.html)
* [14 计算向量夹角](http://jingyan.baidu.com/article/f54ae2fc2704a71e92b849e4.html)
* [15 从协方差阵计算相关阵](http://jingyan.baidu.com/article/ae97a646c0c0c4bbfc461d78.html)
* [16 线性组合均值协方差阵](http://jingyan.baidu.com/article/7908e85c8dd030af491ad279.html)
* [17 线性组合的协方差](http://jingyan.baidu.com/article/d2b1d10288b8b25c7f37d463.html)
* [18 线性规划求最优解](http://jingyan.baidu.com/article/e2284b2b5800e6e2e6118d97.html)
* [19 行列式求解](http://jingyan.baidu.com/article/380abd0a6869711d90192cb5.html)
* [20 求逆序数](http://jingyan.baidu.com/article/1974b28986b4baf4b1f774b8.html)
* [21 1.5解方程](http://jingyan.baidu.com/article/5d368d1ef811d93f60c057ba.html)
* [22 习题1.10求逆矩阵](http://jingyan.baidu.com/article/a948d6517ac8e40a2dcd2e94.html)


## 3. 马同学高等数学

* [马同学高等数学](https://me.csdn.net/ccnt_2012)

* [为什么会有弧度制](https://www.matongxue.com/madocs/5.html)
* [数学中以e为底的指数函数f(x)=e^x求导后为什么还是它本身？](https://www.matongxue.com/madocs/6.html)
* [如何通俗地解释泰勒公式？](https://www.matongxue.com/madocs/7.html)
* [如何通俗地解释欧拉公式（e^πi+1=0）？](https://www.matongxue.com/madocs/8.html)
* [知乎：虚数i是真实存在的吗？](https://www.matongxue.com/madocs/9.html)
* [二阶行列式的几何意义](https://www.matongxue.com/madocs/10.html)
* [如何理解洛必达法则？](https://www.matongxue.com/madocs/11.html)
* [洛必达法则失效的情况？](https://www.matongxue.com/madocs/22.html)
* [如何理解对数?](https://www.matongxue.com/madocs/12.html)
* [为什么调和级数1/n是发散的，而P级数1/n^2是收敛的？](https://www.matongxue.com/madocs/13.html)
* [为什么“1+1=2”，需要“证明”？](https://www.matongxue.com/madocs/14.html)
* [微分和导数的关系是什么？两者的几何意义有什么不同？为什么要定义微分 ?](https://www.matongxue.com/madocs/15.html)
* [如何通俗地理解群论？](https://www.matongxue.com/madocs/16.html)
* [三角函数公式多，怎么记忆？](https://www.matongxue.com/madocs/17.html)
* [如何能更好的理解（ε-δ）语言极限的定义？](https://www.matongxue.com/madocs/18.html)
* [函数连续和一致连续有什么区别？开区间上的连续函数不一定是一致连续的，为什么？](https://www.matongxue.com/madocs/21.html)
* [请用通俗的语言解释一下海涅定理~？](https://www.matongxue.com/madocs/23.html)
* [无穷小量究竟是否为零？](https://www.matongxue.com/madocs/24.html)
* [连续与可导](https://www.matongxue.com/madocs/25.html)
* [f(x)在x=a处可导的一个充要条件是？](https://www.matongxue.com/madocs/26.html)
* [复合函数的连续性](https://www.matongxue.com/madocs/27.html)
* [柯西中值定理的几何意义是什么？](https://www.matongxue.com/madocs/30.html)
* [如何通俗地理解卷积？](https://www.matongxue.com/madocs/32.html)
* [柯西中值定理与拉格朗日中值定理的关系](https://www.matongxue.com/madocs/34.html)
* [实数0的下一个实数是什么？](https://www.matongxue.com/madocs/42.html)
* [向量基本操作(数乘和加法)](https://www.matongxue.com/madocs/469.html)
* [如何通俗地理解傅立叶变换？](https://www.matongxue.com/madocs/473.html)
* []()
* []()
* []()
* []()
* []()
* []()





----

# 希腊字母

|大写|小写|汉译|英译|
|----|----|----|----|
Α|α|阿尔法|Alpha|
Β|β|贝塔|Beta|
Γ|γ|伽玛|Gamma|
Δ|δ|德尔塔|Delte|
Ε|ε|艾普西龙|Epsilon|
Ζ|ζ|捷塔|Zeta|
Ε|η|依塔|Eta|
Θ|θ|西塔|Theta|
Ι|ι|艾欧塔|Iota|
Κ|κ|喀帕|Kappa|
∧|λ|拉姆达|Lambda|
Μ|μ|缪|Mu|
Ν|ν|拗|Nu|
Ξ|ξ|克西|Xi|
Ο|ο|欧麦克轮|Omicron|
∏|π|派|Pi|
Ρ|ρ|柔|Rho|
∑|σ|西格玛|Sigma|
Τ|τ|套|Tau|
Υ|υ|宇普西龙|Upsilon|
Φ|φ|fai|Phi|
Χ|χ|器|Chi|
Ψ|ψ|普赛|Psi|
Ω|ω|欧米伽|Omega
