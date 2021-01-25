# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
* [目录](#目录)
* [常见问题](#常见问题)
   * [PhD;MD;MSc;MPhil;BSc](#phdmdmscmphilbsc)
   * [gtf和gff中，exon, UTR, 和CDS区别？](#gtf和gff中exon-utr-和cds区别)
   * [序列比对时，E值是什么？为什么E值越小越好？](#序列比对时e值是什么为什么e值越小越好)
   * [GC偏好](#gc偏好)
   * [重复序列(Dup)](#重复序列dup)
   * [CNV和SV](#cnv和sv)
   * [标准化](#标准化)
   * [对离散的RNA-seq数据建模，负二项分布(negative binomial distribution)优于泊松分布(poisson distribution)](#对离散的rna-seq数据建模负二项分布negative-binomial-distribution优于泊松分布poisson-distribution)
   * [CNV-seq与CMA之争](#cnv-seq与cma之争)
   * [芯片数据为什么经常取log2](#芯片数据为什么经常取log2)
   * [芯片(microArray)和panel区别](#芯片microarray和panel区别)
   * [怎么获取unique mapping read？](#怎么获取unique-mapping-read)
   * [双端测序中read1和read2的关系](#双端测序中read1和read2的关系)
   * [mappability](#mappability)
   * [BWA输出的sam文件中可选字段(tag)的含义](#bwa输出的sam文件中可选字段tag的含义)
   * [下载sra数据](#下载sra数据)
   * [fastq/fasta downsample](#fastqfasta-downsample)
   * [截短reads](#截短reads)
   * [BAM文件排序异常](#bam文件排序异常)
* [概念](#概念)
   * [专业名词](#专业名词)
   * [综合征](#综合征)
   * [隐性基因、显性基因以及共显性基因](#隐性基因显性基因以及共显性基因)
   * [等位基因频率(AF)](#等位基因频率af)
   * [外显率](#外显率)
   * [易位](#易位)
   * [显(隐)性遗传病](#显隐性遗传病)
   * [染色体带型](#染色体带型)
   * [UPD](#upd)
   * [印记基因](#印记基因)
   * [LOH, AOH, ROH, LCSH](#loh-aoh-roh-lcsh)
   * [XO核型](#xo核型)
   * [染色体](#染色体)
   * [剂量敏感基因(Dosage Sensitivity Gene)](#剂量敏感基因dosage-sensitivity-gene)
   * [正义链(sense strand)和反义链(antisense strand)](#正义链sense-strand和反义链antisense-strand)
   * [冈崎片段(Okazaki fragment)](#冈崎片段okazaki-fragment)
   * [基因组变异检测](#基因组变异检测)
      * [基本概念](#基本概念)
      * [检测流程](#检测流程)
         * [变异检测](#变异检测)
         * [变异注释](#变异注释)
   * [homozygous/hemizygous/heterozygous deletions区别](#homozygoushemizygousheterozygous-deletions区别)
* [技术原理](#技术原理)
   * [PGS/PGD](#pgspgd)
      * [FISH](#fish)
      * [Array-CGH](#array-cgh)
   * [CNV-seq](#cnv-seq)
* [数据库](#数据库)
   * [肿瘤数据库](#肿瘤数据库)
   * [遗传疾病公共数据库](#遗传疾病公共数据库)
   * [其它](#其它)
   * [在线资源](#在线资源)
* [软件](#软件)
   * [生物信息软件参数解析](#生物信息软件参数解析)
      * [samtools](#samtools)
      * [bcftools](#bcftools)
   * [python模块](#python模块)
      * [pysam](#pysam)
      * [pyfaidx - 对fasta进行快速随机访问](#pyfaidx---对fasta进行快速随机访问)
   * [BWA & Bowtie2](#bwa--bowtie2)
   * [IGV](#igv)
   * [Kraken2](#kraken2)
   * [CNVkit](#cnvkit)
   * [samtools](#samtools)
* [文件格式](#文件格式)
   * [.fai (索引文件)](#fai-索引文件)
   * [bam/sam](#bamsam)
* [期刊杂志](#期刊杂志)
* [下载](#下载)
   * [BioStars](#biostars)
   * [StackExchange-Bioinformatics](#stackexchange-bioinformatics)
* [其他](#其他)
* [比较酷的事情](#比较酷的事情)
   * [不同k值下基因组间的k-mer相似度近似于物种分类间的相似度](#不同k值下基因组间的k-mer相似度近似于物种分类间的相似度)
   * [DUP/DEL的发生机制](#dupdel的发生机制)
<!--te-->

----

# 常见问题


## PhD;MD;MSc;MPhil;BSc

* MD: 医学博士 (Medicinae Doctor)
* PhD: 学术研究型博士学位 (Philosophic Doctor)
* MSc: 理学硕士 (Master of Science)
* MPhil: 理学硕士 master
* BSc: 理学学士

Mphil的毕业论文要求要比 MA/MSC的要求高



## gtf和gff中，exon, UTR, 和CDS区别？

* [彻底搞清楚promoter, exon, intron, and UTR](http://www.xybiotech.com/resources/support/667.html)
* [关于exon,CDS,start_codon,stop_codon,UTR那点事情](http://blog.sciencenet.cn/blog-1113671-1079417.html)



## 序列比对时，E值是什么？为什么E值越小越好？

* [p值、E值、FDR、q值…你晕菜了吗？](https://mp.weixin.qq.com/s?__biz=MzI3MTM3OTExNQ==&mid=2247483871&idx=1&sn=2acadddcc14a01d8bf074e9b6fcadab8&scene=21#wechat_redirect)
* [人气推文p值、E值、FDR、q值…你晕菜了吗？续集来啦！](https://mp.weixin.qq.com/s?__biz=MzI3MTM3OTExNQ==&mid=2247483940&idx=1&sn=be08093540e43b2cbc386fc5a6e2d934&chksm=eac3fde0ddb474f65cdf50e0c14ec408eb796b7d3422f2c215b7fe5b32aa6790e2c281eeb835&scene=21#wechat_redirect)


举个比较极端的例子：我们知道两天序列比对时都有一个打分，打分超过某个阈值，则认为匹配，否则不匹配
。假设出现假阳(不匹配但被识别为匹配)的概率为0.01(p-value=0.01)，我们使用一条查询序列去匹配某数据库，
获得了500条候选序列(上帝说：它们与该查询序列其实都不匹配)，则这500个比对中至少出现一次pvalue小于0.01
的概率为 1-(1-0.01)^500≈0.99。

500个随机比对中打分最好的p值小于等于0.01的概率接近于1！也就是说，p值小于等于0.01的筛选完全无法避免
错误匹配的混入啊！难道，这么严格的取值都不足以作为这个序列匹配是正确的证据了？！

很遗憾地告诉你，当候选序列很多的时候，这个证据确实还不够强！那么，这种情况下，我们应该继续减小
p-value的阈值吗？非也！因为这个问题不是出在p-value阈值定高定低了，而是出在p-value指标体现不出
该查询序列对应的候选序列的数目。所以我们应该做的是，引入另一个既考虑了p-value又考虑了候选序列
数目的统计指标，它就是传说中的E-value！它的别名就是：期望值(在一个离散性随机变量试验中每次可
能结果的概率乘以其结果的总和, E-value = p-value * n)。事实上，目前比较知名的一些搜索引擎都使用
了E值。

是不是大家现在一脸懵圈？这就对了。如果现在碰到和你一样懵或更懵的人的概率是万分之一，对面有1万个人，
那么，懵圈的E-value就是1（别问我怎么算的）。也就是说，对面大概有1个人和你一样懵或更懵。

对一查询序列来说，比对软件报告一个候选序列A与其匹配的E-value是1，就意味着其他候选序列中还有一个序列B
（虽然不知道B一定是谁）也可以与这个查询序列匹配得不错，至少和候选序列A与该查询序列的匹配程度相当或更好。
那么，软件报告这个候选序列A就极有可能是假阳性结果。我们肯定是希望，E-value越小越好，E-value为0.001，
就是只有千分之一个候选序列可以威胁当前的匹配（突然想到电影院里半个人都没有的梗）。Mascot中常用的阈值
30分就是这么来的：30分 = -10*log10(E-value=0.001)



## GC偏好

GC rich的区域不易测序的原因，主要发生于以下两个阶段:

1. PCR 阶段

由于GC rich的区域，其氢键数较多，稳定性较强，因此在PCR时，GC rich的区域较不易分开，因此不容易被扩增。

此外，即便GC rich的区域在PCR时被分开了，单股的GC rich区域亦容易因为氢键，而自行黏合形成二级结构，亦不易被扩增。

若采用PCR free的样本备制方式，则可能改善此PCR所造成的问题。

2. Fragmentation 阶段

在测序前需将DNA 打断成适当大小的片段才能上机测序，由于GC rich的区域不易被打断，使得存在GC rich区域的片段过大，
不适合上机测序，而在长度筛选(size selection)时被舍弃。

目前，若要解决此问题，透过增加测序量，才能提高获取这些序列的机会。


> Uneven coverage of reads resulted from GC bias can be introduced at several processes of Illumina sequencing, e.g., 
PCR amplification of library, cluster amplification, and the sequencing step. 
Among these factors, library amplification by PCR plays a major role in generating GC bias. 
[Aird D, Ross MG, Chen WS, Danielsson M, Fennell T, et al. (2011) Analyzing and minimizing PCR amplification bias in 
Illumina sequencing libraries.]


GC偏好也存在其他地方，比如基因编码区内密码子的最后一位，C碱基往往占优势；基因的长度和GC含量成相关性；
Aquifex aeolicus 的基因组整体GC含量是43%，而核糖体RNA操纵子的GC含量是65%。


**为什么reads数会随着GC含量从低到高而呈现先升高后下降的趋势呢？**

对于DNA模板而言，有的二级结构复杂，有的热稳定性差异大，这些因素都会影响PCR扩增效率。
因此，并非所有基因组片段都能在PCR扩增文科中得到同等体现，而是存在明显的扩增偏好。


## 重复序列(Dup)

* [《NGS攻略》之Dup传](https://mp.weixin.qq.com/s?__biz=MzIxOTQzNTg5NQ==&mid=2247485740&idx=2&sn=0d15036377f25d2949cfc3ead09654d2&chksm=97da0f34a0ad862281a5529909fcbbd632ceb44949f1abe8dabf862eb1752049c1bc9cec2899&scene=21)
* [《NGS攻略》之PCR-Free传](https://mp.weixin.qq.com/s?__biz=MzIxOTQzNTg5NQ==&mid=2247485740&idx=2&sn=0d15036377f25d2949cfc3ead09654d2&chksm=97da0f34a0ad862281a5529909fcbbd632ceb44949f1abe8dabf862eb1752049c1bc9cec2899&scene=21)

所谓Dup，即重复序列Duplicate reads，指通过测序得到的两对或两对以上的Pair-End Reads
同时比对到参考基因组上相同的起始和结束位置的序列（如图1所示）。这些重复序列在总测序序列
中占比简称为Dup rate。由于这些重复序列并不能带来额外信息，相反会影响变异检测结果准确性，
因此下游生信分析中这些重复序列是需要去除的去掉，这也就意味着Dup rate越高，数据利用率越低，
测序成本浪费的也就越多。

造成Dup rate偏高的真实原因是什么？
PCR放大成百上千倍，为什么NGS的Dup rate只有十位数甚至是个位数？
有没有办法降低测序过程中的Dup？

对于Dup的来源，在NGS的“江湖”中有各种各样的“传说”，很多大侠认为主要是从样本建库端引入的
（或者说认为建库PCR是造成Dup rate偏高的罪魁祸首），但其实测序产生的Dup reads来源很广泛，
客观来讲主要有以下几个方面：

1. 样本本身的Dup；
2. 文库构建中扩增引入的Dup（即PCR Dup）；
3. 测序前信号放大（荧光信号采集单元生成过程）引入的Dup；
4. 芯片测序过程中引入的光学Dup。

大多数人认为NGS数据的Dup主要来自于上述第二种。但据真实案例显示，第三种荧光信号采集单元
生成的过程中引入的Dup和第四种芯片测序过程中引入的光学Dup居多。而第一种样本本身的Dup反倒
是我们生物学中应真正关注，并与测序数据的Dup加以区分的一种“有用的”Dup。



**去重(或标记)的方法**

[去重工具到底哪家强](http://www.360doc.com/content/18/0806/10/19913717_776047876.shtml)

1. picard的MarkDuplicates
2. **sambamba的markdup** (注意：加上-r参数才会去重，否则仅标记(FLAG存在1024))【速度最快，常用】
3. samtools的markdup(标记)、rmdup(去重)
4. samblaster的markdup（-r: 去重）



## CNV和SV

* [基因组变异检测概述（SNP、InDel、SV）](https://blog.csdn.net/Alex6plus7/article/details/50236375)

人类基因组上的变异主要分为三大类：
    1. 单核苷酸变异，（通常称为单核苷酸多态性，通俗的说法就是单个DNA碱基的不同，简称SNP）；
    2. 小的Indel（Insertion 和 Deletion的简），指的是在基因组的某个位置上所发生的小片段序列的插入或者删除，
其长度通常在50bp以下（这个长度范围的变异可以利用Smith-Waterman 的比对算法来获得1,2）；
    3. 大的结构性变异，这种类型比较多，包括长度在50bp以上的长片段序列的插入或者删除、染色体倒位，染色体内
部或染色体之间的序列易位，拷贝数变异，以及一些形式更为复杂的变异。

为了和SNP变异作区分，第2和第3类变异通常也被称为基因组结构性变异（Structural variation，简称SV）。

这里值得一提的是，研究人员对基因组的结构性变异发生兴趣，主要是由于这几年的研究发现：（1）虽然还未被广泛公认，
但研究人员发现SV对基因组的影响比起SNP来说还要大3；（2）基因组上的SV比起SNP而言，似乎更能用于解释人类群体多样
性的特征；（3）稀有且相同的一些结构性变异往往和疾病（包括一些癌症）的发生相关联甚至还是其致病的诱因4–6。不过
应该注意的地方是，大多数的结构性变异并不真正与疾病的发生相关联，但是却确实与周围环境的响应或者其他的一些表型
多态性相联系。

目前主要有4种检测基因组上结构性变异的策略，分别为：（1）Read pair（也称为Pair-end Mapping，简称PEM）；
（2）Split read（简称SR）；（3）Read Depth（简称RD）和（4）基于de novo组装的方法（图1）。


## 标准化

* [Loess Normalization and Quantile Normalization](http://eln.iis.sinica.edu.tw/lims/files/users/admin/sheng_wu_jing_pian_de_ji_ben_fen_xi_liu_cheng_.pdf)
* [3种Normalization的R实例](https://genomicsclass.github.io/book/pages/normalization.html)
* [基因芯片数据分析中的标准化算法和聚类算法](https://www.plob.org/article/829.html)
* [quantile normalization on pandas dataframe](https://stackoverflow.com/questions/37935920/quantile-normalization-on-pandas-dataframe)

芯片间的数据标准化(Cross slide normalization): 平均数, 中位数标准化(mean or median normalization)

平行实验数据的标准化: Quantile Normalization

芯片内的数据标准化(within slide normalization): Lowess Normalization


## 对离散的RNA-seq数据建模，负二项分布(negative binomial distribution)优于泊松分布(poisson distribution)

参考文献：

1. [Differential expression analysis for sequence count data](https://genomebiology.biomedcentral.com/articles/10.1186/gb-2010-11-10-r106)
【2010年，影响因子12+，引用次数8000+】
2. [ReadDepth: A Parallel R Package for Detecting Copy Number Alterations from Short Sequencing Reads](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0016327)
【2011年，plos one， 引用100+】

其它

1. [二项分布 | 泊松分布 | 指数分布 | 负二项分布 | 伽玛分布 | Βeta分布 | 卡方分布 | 正态分布 | 多维高斯分布 | 狄利克雷分布 | 帕累托分布 | 柯西分布 | 持续收集~...](https://blog.csdn.net/weixin_34166847/article/details/86395350)
2. [Question: What Makes One Probability Distribution Better For Rna-Seq Than Another?](https://www.biostars.org/p/6028/)
3. [Why do we use the negative binomial distribution for analysing RNAseq data?](http://bridgeslab.sph.umich.edu/posts/why-do-we-use-the-negative-binomial-distribution-for-rnaseq)
4. **[WHY SEQUENCING DATA IS MODELED AS NEGATIVE BINOMIAL](https://bioramble.wordpress.com/2016/01/30/why-sequencing-data-is-modeled-as-negative-binomial/)**



## CNV-seq与CMA之争

* [现阶段产前临床应用时选择哪种方法较好: CNV-seq和CMA (伊宁)](https://zhuanlan.zhihu.com/p/70315264)
* [CMA和CNV-seq技术哪个更好？—— 选择CMA (蒋宇林)](https://mp.weixin.qq.com/s?__biz=MzA4NTI5ODgwOQ==&mid=570030518&idx=1&sn=dfc3c0c3ba2b1b94fecf3073f8f83d2f&chksm=3bd742a00ca0cbb6ca8e9d387e3e5c86e49ee705fadd9225a012fe3b0722cb237a33619c29dd&mpshare=1&scene=1&srcid=06306jqvZl28fWX4J3lzA5zY&key=6ff676ea8e4091fd7d49bafc28ed57f39d123c2dd78120642e4d6a44fdab0f390c504a76cbb365a31a8162c8609fe6de6e3cff9fb20b6370968367f8ca0f866caabf2a588df6a70c237fdf89fe14f1eb&ascene=1&uin=MjQ4MTQ1NDg4Mw%3D%3D&devicetype=Windows+10&version=62060728&lang=zh_CN&pass_ticket=1%2FBYjCaDwDx5g%2FUK4Qpp5Da%2Bs1GM2hvU1qolE43hGId9rJr6llFP6Fbwf4vV1Jzp)
* [好东西应该再次分享——CNV数据分析 (徐雄)](https://mp.weixin.qq.com/s?__biz=MzI0NjQ3OTIwMA==&mid=100000647&idx=1&sn=ee3698b8255f5a180eb277f167d60c15&chksm=69bfe3885ec86a9e5f6b2eca652622306943ad9430e0aa61478c5c6a88b73137d7fdd188c3f1&scene=18&xtrack=1&key=0d395d45dee340535117e67eadabde94a49c87d85a9b41aa71a655ec35c5f20a0bd6c313958c40ff2c1f0720746098dc3b09f1a4ebff14d84cf9ded05779a05dda55188bac051edd99c1db71270d1576&ascene=1&uin=MjQ4MTQ1NDg4Mw%3D%3D&devicetype=Windows+10&version=62060728&lang=zh_CN&pass_ticket=1%2FBYjCaDwDx5g%2FUK4Qpp5Da%2Bs1GM2hvU1qolE43hGId9rJr6llFP6Fbwf4vV1Jzp)


## 芯片数据为什么经常取log2

* [Question: Log2 Ratio or Log2 Fold Change - terminology confusion and which one should I use?](https://www.biostars.org/p/221766/)
* [Why do we usually use Log2 when normalizing the expression of genes?](https://www.researchgate.net/post/Why_do_we_usually_use_Log2_when_normalizing_the_expression_of_genes)
* [MA plot](https://www.jianshu.com/p/cdfac0bfb733)
* [文献：The limits of log-ratios](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC400743/)
* [Nature: Microarray data normalization and transformation](https://www.nature.com/articles/ng1032z)

与对照组相比，实验组fold change变大的取值范围是1-正无穷；但FC变小的取值范围是0-1，不对称。
将其转化成log2，则不对称数据变成了以0为中心的对称数据。

**为什么不将fold change转换成拷贝数(CN,copy number)，而是要取log2呢？**
主要是因为芯片数据常用来分析实验组/对照组的基因表达差异，而每个基因的正常拷贝数是多少可能事先不清楚。


## 芯片(microArray)和panel区别

* [microarray 和二代测序(NGS)的区别](http://blog.sina.com.cn/s/blog_6babbcb8010165qr.html)
* **[SNP芯片的原理](https://www.cnblogs.com/think-and-do/p/6611334.html)** 分别介绍了Illumina、Affymetrix(昂飞)和Agilen(安捷伦)的多款芯片设计原理，非常棒！

本质区别：芯片属于一代测序(本质是核酸杂交), panel属于二代测序(本质是PCR)



## 怎么获取unique mapping read？

[怎么获取unique mapping read？](http://www.biotrainee.com/thread-1115-1-1.html)

**tophat/hisat2**

grep 'NH:i:1' out.sam > unique.sam

**BWA**

有`XT:A:U`就代表这一条是unique read。 ("XT"代表mapping类型，数据类型为"A"，即可打印字符，其值可以是Unique/Repeat/N/Mate-sw).

由于BWA还提供了"AS"(alignment score)和"XS"(suboptimalalignment score)这两项，所以即使有些reads没有被Uniquely mapped，
只要AS的值和XS的值相差足够大，也有一定价值。

**Bowtie2**

由于bowtie2产生的sam文件并没有NH标签，所以提取uniqueread可能比较麻烦。首先提取“AS”标签表示能比对上的read（>=1 time），
然后利用grep反正则表达式过滤掉XS标签得到我们需要的unique read。

`单端`: grep "AS:" aligned.sam | grep –v "XS:" > unique_alignments.sam

`双端`：grep "AS:" aligned.sam | grep –v "XS:" > unique_alignments.sam | grep "YT:Z:CP" unique.sam > pair-end_unique.sam
  ("Filter out the reads that aligned concordantly using grep YT:Z:CP")



## 双端测序中read1和read2的关系

[双端测序中read1和read2的关系](https://www.jianshu.com/p/b18ee79a0285)

原始reads如下：

XXX.R1.fastq

```
@NS500832:569:HNN3VAFXY:3:21405:22082:10749 1:N:0:AATAAGC
GGTAAATTTAAAATAAAACAAGCGGGAGTCACAGATACACTGTCTGGGAAAGTGAAACTTAAGAGCTTTGTGAGTCCTGTTGTAATGCTTTTAGATGCATTTATATACCAACAGGCCAAAGTCACATTTTTTAC
+
EEEEEEEEEEEEEEEEAEEEEEAAEEEEEEEEEEEAE/AEEEA/AE<<E<AEEEEAEEEE/<AEEAEE<<EE<AEE/EAEEEEEEEEEAEEA<EEE<EE/<EEE<E<//</AEAE6//AEEEAE/<EAAEAAA<
```

XXX.R2.fastq

```
@NS500832:569:HNN3VAFXY:3:21405:22082:10749 2:N:0:AATAAGC
AACCTTGGTAACCCCTGAATGATCAGGAATCTAATCGGTAAAAAATGTGACTTTGGCCTGTTGGTATATAAATGCATCTAAAAGCATTACAACAGGACTCACAAAGCTCTTAAGTTTCACTTTCCCAGACAGTGTA
+
EEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEE/EEEE/EEAEEEEEEEEEE<EAEEEEA6/EAAEAA<EEE<<EEEE<EEEEEEEEEEEAEEE/EEEEEEEEEE<AEEE/EEEAEAEEEA</</AEEEEEE/AE
```

经过bowtie2比对后的sam文件中的记录如下：

```
NS500832:569:HNN3VAFXY:3:21405:22082:10749   99    chr6  29794821 27 134M  =  29794856 171   GGTAAATTTAAAATAAAACAAGCGGGAGTCACAGATACACTGTCTGGGAAAGTGAAACTTAAGAGCTTTGTGAGTCCTGTTGTAATGCTTTTAGATGCATTTATATACCAACAGGCCAAAGTCACATTTTTTAC    EEEEEEEEEEEEEEEEAEEEEEAAEEEEEEEEEEEAE/AEEEA/AE<<E<AEEEEAEEEE/<AEEAEE<<EE<AEE/EAEEEEEEEEEAEEA<EEE<EE/<EEE<E<//</AEAE6//AEEEAE/<EAAEAAA<    AS:i:-3  XS:i:-65 XN:i:0   XM:i:1   XO:i:0   XG:i:0   NM:i:1   MD:Z:76G57  YS:i:-5  YT:Z:CP
NS500832:569:HNN3VAFXY:3:21405:22082:10749   147   chr6  29794856 27 136M  =  29794821 -171  TACACTGTCTGGGAAAGTGAAACTTAAGAGCTTTGTGAGTCCTGTTGTAATGCTTTTAGATGCATTTATATACCAACAGGCCAAAGTCACATTTTTTACCGATTAGATTCCTGATCATTCAGGGGTTACCAAGGTT  EA/EEEEEEA/</<AEEEAEAEEE/EEEA<EEEEEEEEEE/EEEAEEEEEEEEEEE<EEEE<<EEE<AAEAAE/6AEEEEAE<EEEEEEEEEEAEE/EEEE/EEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEE  AS:i:-5  XS:i:-75 XN:i:0   XM:i:1   XO:i:0   XG:i:0   NM:i:1   MD:Z:41G94  YS:i:-3  YT:Z:CP
```

可见，双端测序下机数据中得到的read1和read2是两条互补链insertsize中方向相对的两条序列，再比对到单链的参考基因组之前会先将其中一条read转义，
然后进行比对，所以比对得到的SAM和BAM文件中read1和read2有一条是被转了的。



## mappability

[ENCODE mappability and repeats](https://davetang.org/muse/2013/07/08/encode-mappability/)

这里有两个概念：

   * alignability: 可比对性，允许2个错配
   * uniqueness： 唯一性，0个错配



## BWA输出的sam文件中可选字段(tag)的含义

[sam-tags](https://samtools.github.io/hts-specs/SAMtags.pdf)

* `XT:A:?`: 代表mapping类型，数值类型为A(可打印字符), 其值可以是Unique/Repeat/N/Mate-sw，`XT:A:U`就代表这一条是unique read
* `X0:i:?`: Number of best hits(最优匹配的数目)
* `X1:i:?`: Number of suboptimal hits found by BWA(次优匹配的数目)
* `XN:i:?`: Number of ambiguous bases in the referenece(参考基因组中模糊碱基(N)的数目)
* `XM:i:?`: Number of mismatches in the alignment(错配的碱基数) 
* `XO:i:?`: Number of gap opens(gap的数目)
* `XG:i:?`: Number of gap extentions(gap延申的碱基数目)
* `XA:Z:?`: Alternative hits; format: (chr,pos,CIGAR,NM;)*, 其他最优匹配，如`XA:Z:chr7,+48079409,36M,0;`
* `SA:Z:?`: Other canonical alignments in a chimeric alignment(嵌合比对中的嵌合部分)
* `AS:i:?`: Alignment score(该匹配的得分)
* `XS:i:?`: Suboptimal alignment score(次优匹配的得分)
* `YS:i:?`: mate序列匹配的得分
* `XF:?:?`: Support from forward/reverse alignment
* `XE:i:?`: Number of supporting seeds
* `NM:i:?`: Edit distance(编辑距离)
* `MD:Z:?`: Mismatching positions/bases(不匹配的位置和碱基);代表序列和参考序列错配的字符串（字符指的是参考序列的碱基，不是read的碱基，如`MD:Z:29G6`代表参考基因组该位点的碱基为G）
* `YT:Z:?`: UU表示不是pair中一部分、CP是pair且可以完美匹配、DP是pair但不能很好的匹配、UP是pair但是无法比对到参考序列上
* `BC:?:?`: Barcode sequence
* `RG:Z:?`: Read group
* `MC:Z:?`:  CIGAR string for mate/next segment

下面通过一些例子说明：

**`XT:A:U  NM:i:1  X0:i:1  X1:i:78 XM:i:1  XO:i:0  XG:i:0  MD:Z:12G23`**:
只有1个最优匹配，有78个次优匹配，最优匹配中没有gap，有1个错配(基因组上第13个碱基是G)，编辑距离为1. 是unique read。
`CIAGR`字段为"36M"(注意：CIAGR中M可是mismatch)

**`XT:A:U  NM:i:2  X0:i:1  X1:i:0  XM:i:1  XO:i:1  XG:i:1  MD:Z:1G33`**:
只有1个最优匹配，有1个错配，1个gap(gap的碱基数为1)，编辑距离为2。
`CIAGR`字段为"10M1I25M"

获得完全匹配(perfect match)的reads: `NM:i:0 XM:i:0 X0:i:1`





## 下载sra数据

[NCBI-SRA数据下载的3种方法](https://www.jianshu.com/p/e72c72c1f181)

下载常用sra数据，通常有三种方法：

* aspera
* prefetch
* wget

现在NCBI更改了sra数据的存储协议，所以aspera方法已经失效。


prefetch下载sra步骤：

1. NCBI搜索SRA号
2. 点击"Send to:",选中"File",格式选择"Accesion List",下载文件(SraAccList.txt)
3. 执行下载命令: `prefetch --option-file SraAccList.txt`

wget下载sra步骤：

1. NCBI搜索SRA号
2. 点击"Send to:",选中"File",格式选择"RunInfo",下载文件(SraRunInfo.csv)
3. 从SraRunInfo.csv中提取'download_path'字段信息
4. 使用wget下载



## fastq/fasta downsample

如果fastq/fasta不是很大，比如只有几个G，可以使用`seqtk`：

```shell
# 从fastq中随机挑选1000条reads
seqtk sample -s 10 test.fastq.gz 1000 > test_1000.fastq
# 输入文件可以是压缩文件也可以是文本文件
# 也可以
seqtk sample -s 10 test.fastq.gz 1000 | gzip - > test_1000.fastq.gz
```

`seqtk`有以下两个问题：

1. 当输入文件过大时(如几十个G)，速度很慢；
2. 很耗内存 (可以使用-2参数解决，但速度更慢)

如果碰到以上问题，有个折中的方法：因为fastq/fasta文件里面存放的reads就是按照随机顺序
存放的，所以我们可以直接取前1000行。

```shell
# 1. 使用head
gunzip -c test.fastq.gz | head -4000 | gzip - > test_1000.fastq.gz

# 2. 使用fastp (速度更快)
fastp -i test.fastq.gz -o test_1000.fastq.gz -A -G -Q -L -j test_1000.fastq.json --reads_to_process 1000
# 注意：--reads_to_process参数在低版本中不存在
```



## 截短reads

1. 使用fastx_trimmer

```shell
# 截取第15个碱基到第50个碱基之间的36个碱基
gunzip -c test.fastq.gz | fastx_trimmer -f 15 -l 50 -z -o test_1.fastq.gz
```

2. 使用fastp

```shell
# 截取前1000条reads的前50bp
fastp -i test.fastq.gz -o test_1000.fastq.gz -j test_1000.fastq.json -A -G -Q -L -b 50 --reads_to_process 1000
```



## BAM文件排序异常

最近遇到了一个非常奇怪的现象：4个样本进行bwa比对，各自获得排序后的bam文件，其中，有3个文件中reads是从chr1，chr2开始排序，而剩余的1个文件却是从chr10，chr11开始排序。

先来说说这个异常bam文件的一些异常点：

1. 原始sam文件中，SQ字段就是从chr10开始的，而不是chr1。(samtools默认排序的方法是根据sam文件header的SQ字段进行排序的）
2. 没有一条read是比对到chrM上的，所以SQ字段中就没有chrM。

这个问题纠结了两天，测试了不同BWA版本，重新构建了基因组的index，调整了BWA/samtools的参数,更换了不同样本，均没有发现问题所在。在快要放弃时，发现原来是**计算节点**的问题—— 在这个节点上，BWA比对全都异常(从chr10开始，没有read比对到chrM)，而其他节点均正常。深层次原因未知，目前只能避开异常节点。








----

# 概念


## 专业名词

* `VUS (Variant Uncertain Significance)`：未知的变异，意义不确定的变异
* `AF (Allele Frequency)`: 等位基因频率
* `MAF (Minor Allele Frequency)`: 多个群体中总的AF?
* `X-inactivation` ([X染色体去激活](https://en.wikipedia.org/wiki/X-inactivation)): 
又称X染色体失活或里昂化，是指雌性哺乳类细胞中两条X染色体的其中之一失去活性的现象。
X染色体会被包装成异染色质，进而因功能受抑制而沉默化。
* `canonical transcript`： 经典转录本
* `AD (Autosomal Dominant Inheritance)`: 常染色体显性遗传
* `AR (Autosomal Recessive Inheritance)`: 常染色体隐性遗传

## 综合征

[WiKi收录的1430个综合征](https://en.wikipedia.org/wiki/List_of_syndromes)


## 隐性基因、显性基因以及共显性基因

显性基因常能形成一种有功能的物质（如酶），而它的隐性等位基因则由于相应的核苷酸发生了突变而
不能产生这种物质，所以在杂合体中只有显性基因能表现出正常的功能（显性），而隐性基因则不能表现。

一对等位基因之间，彼此没有显性和隐性的区别，在杂合子状态时，两种基因的作用都能表达，分别独立
地产生基因产物。形成相应的表型，这种遗传方式称为共显性（codominance)遗传。ABO血型的遗传可作为
共显性遗传的实例。

ABO血型的基因已定位于第9号染色体上的9q4.2位点，在这一基因座位上，由A.B和O三种基因组成复等位基因。
基因A对基因0为显性。基因B对基因O也是显性，基限A和基因B为共显性。基因型AA和AO都决定红胞膜上机抗
原A的产生，这种个体为A型血，基因型BB和BO都决定红细胞膜上抗原B的产生，这种个体为B型血，基因型OO
则只有H物质的产生面而不产生抗原A和抗原B，这种个体为O型血，基因型AB决定红细胞膜上有抗原A和抗原B，
故为AB型血，为共显性遗传。


**DiGeorge综合征(22q11.2缺失)**

DiGeorge综合征(DiGeorge syndrome, DGS)是一组与咽囊系统发育缺陷有关的体征和症状。DGS的典型三联征表
现为心脏圆锥动脉干畸形、胸腺发育不全和低钙血症(由甲状旁腺发育不全造成)。大多数DGS患者以及诸如腭心
面综合征(velocardiofacial syndrome，VCFS，也称为Shprintzen综合征)的其他类似综合征患者都存在染色体
22q11.2的缺失。这些疾病都属于染色体22q11.2缺失综合征(22q11.2 deletion syndrome, 22qDS)的范畴。

对于疑似DGS或22qDS的新生儿的紧急治疗主要着重于评估和治疗可能的低钙血症和严重先天性心脏缺陷，以及识
别和治疗患有完全DGS[一种严重的联合免疫缺陷病(severe combined immunodeficiency, SCID)]的新生儿

**猫叫综合征**

患者第5号染色体短臂缺失，故又名5p—综合征，为最常见的缺失综合征，因婴儿时有猫叫样啼哭而
得名，其原因在于患儿的喉部发育不良或未分化所致，发病率约为1/50000，女患者多于男患者。

头小，圆月脸不对称，呈惊恐状；眼距增宽，内眦赘皮，眼角下斜，斜视，白内障，视神经萎缩；
鼻梁宽，小下颌，偶见唇腭裂，错咬合，耳位低，发育不良，颈短。新生儿期肌力低下，明显的智力低下、
智力发育迟缓，如2岁后才能坐稳，4岁后才能独立走路，成人期后多动及破坏性行为。生长发育落后，
先天性心脏病（50%）；掌骨短，并指，通贯掌纹，髋关节脱位，半椎体，脊柱侧凸；肾脾缺如，尿道下裂，
隐睾，腹股沟疝等。

死亡率较低，很多患者存活至成年，但他们的身高及体重低于正常人。



**猫眼综合征**

猫眼症候群（英语：Cat eye syndrome）是一种遗传病，其会导致眼睛虹膜的缺损，使眼睛看起来像猫眼一样。
其在瑞士的发生率约为1/50000至1/150000。

遗传方面，其遗传方式为无家族史的偶发案例。最常原因为最常是因为第22对染色体长臂11位置发生了重复及
180度反转所致，而带有2个染色体的著丝点及双卫星区域。

眼睑裂下斜(down-slanting palpebral fissures)和眼间距过宽(ocular hypertelorism)等若干眼部缺陷、
耳前窝/耳前赘(preauricular pits/tags)、肾脏问题(缺肾、多肾、肾发育不良)、个子矮小、疝气、智力
缺陷(只有一小部分猫眼综合征患者智力正常)、骨骼缺陷、大量其它器官问题





## 等位基因频率(AF)

等位基因频率是群体遗传学的术语，用来显示一个种群中特定基因座上各个等位基因所占的频率，
或者说是等位基因在基因库中的丰富程度。

等位基因频率的定义如下：

如果
1. 一个染色体中存在某特定基因座，
2. 一个种群有N个个体，每一个个体的染色体套数为n（例如二倍体生物的体细胞中有两个该特定基因座），
3. 该等位基因在种群中有i份；
那么等位基因频率为i/(Nn)。

例子：

如果在一个种群中有10个个体，一个特定基因座有两个可能的等位基因A和a，个体的基因型分别为：

AA, Aa, AA, aa, Aa, AA, AA, Aa, Aa, 和 AA

那么等位基因A和a的等位基因频率分别为：

pA = (2+1+2+0+1+2+2+1+1+2)/20 = 0.7

pa = (0+1+0+2+1+0+0+1+1+0)/20 = 0.3

当然，也可以分开单独计算AA、Aa、aa个体的频率再加起来除。因为此基因座仅有A和a二种等位基因，
因此 pA + pa = 1（100%），所以 pa 也可以这样计算：

pa = 1-0.7 = 0.3


## 外显率

外显率是指一定环境条件下，群体中某一基因型（通常在杂合子状态下）个体表现出相应表型的百分率。

外显率(penetrance)等于100%时称为完全外显(complete penetrance)，低于100%时则为不完全外显
（incomplete penetrance)或外显不全。譬如说，玉米形成叶绿素的基因型AA或Aa，在有光的条件下，
应该 100%形成叶绿体，基因A的外显率是100%；而在无光的条件下，则不能形成叶绿体，我们就可以
说在无光的条件下，基因A的外显率为0。另外如在黑腹果 蝇中，隐性的间断翅脉基因i的外显率只有90%，
那也就是说90%的ii基因型个体有间断翅脉，而其余10%的个体是野生型，但它们的遗传组成仍然都是 ii。

基因的作用可受环境和其他基因的影响而改变其表型的表达（表现度）。因此，即使在同一家庭中，
有相同基因改变（等位基因）者可表现出非常不同的表型。例如Waardenburg综合征Ⅰ型中，PAX3基
因突变产生的典型表现是额部白发，眼距增宽，虹膜异色，但有20%不到的病例有严重的听力丧失。
有些带有异常等位基因的家庭成员除了额部白发外无其他表现。然而他们的子女可因同一突变而有
严重的先天性耳聋。较罕见者，表现度很低而无临床异常可见，但他可把异常等位基因传给后代，
使其产生所有临床症状。这种情况下，系谱上可有一代跳空。此现象称为外显率缺失。然而，某些
外显率缺失的情况是由于检查者未能识别或是不熟悉遗传病的轻微表现所致。表现度很小的病例有
时可视作疾病的逍遥型。


## 易位

[平衡易位型胚胎检测技术](http://www.sohu.com/a/221089944_781409)

易位(translocation)：指从某一条染色体上断裂下的节段连接到另一染色体上。两条染色体各发生一处断裂，并交换其无着丝粒节段，
分别形成新的衍生染色体和相互易位。在相互易位中，如有染色体片段的丢失，称为"不平衡易位"，若无染色体片段的丢失，表型正常，
故称染色体"平衡易位"

两条不同源的染色体各发生断裂后，互相变位重接而形成两条结构上重排的染色体称相互易位。这种易位大多数都保留了原有基因总数，
对基因作用和个体发育一般无严重影响，故称平衡易位。在减数分裂时，如果两个易位的染色体在一起，两个正常的染色体在一起进入
生殖细胞中，将产生平衡配子，因为这样的分离能保证每一个细胞有一套完整的基因。如果一个易位的染色体和一个正常的染色体在一
起分离而进入生殖细胞中，将产生不平衡的配子。平衡易位是人类中最多的一类染色体结构畸变，在新生婴儿中的发生率约为1/500～1/1000。

![](https://gss0.baidu.com/-Po3dSag_xI4khGko9WTAnF6hhy/zhidao/pic/item/0df431adcbef7609601dee4a29dda3cc7dd99ed4.jpg)


## 显(隐)性遗传病

**隐性遗传病**， 其传递方式是隐性的，当一对染色体中都有致病基因时才能发病（称为病人）。

**显性遗传病**，只要有一条染色体中带有致病基因就会发病

**伴X显性遗传病**

* 不管男女，只要存在致病基因就会发病，但因女子有两条X染色体，故女子的发病率高于男子。因为没有一条正常染色体的掩盖作用，男子
发病时，往往重于女子。
* 病人的双亲中必有一人患同样的病（基因突变除外）。
* 可以连续几代遗传，但患者的正常子女不会有致病基因再传给后代。
* 男病人将此病传给女儿，不传给儿子，女病人（杂合体）将此病传给半数的儿子和女儿。


**常染色体显性遗传病（AD）**

是指致病基因位于常染色体上，且由单个等位基因突变即可起病的遗传性疾病。具有如下特点：

1. 只要体内有一个致病基因存在，就会发病。双亲之一是患者，就会遗传给他们的子女，子女中半数可能发病。若双亲都是患者，
其子女有3/4的可能发病（双亲均为杂合体，子代中纯合体患病占1/4，杂合体患病占1/2，纯合体正常占1/4，设致病基因为A，
则Aa*Aa=1/4AA（纯合患病）+2/4Aa（杂合患病）+1/4aa（正常）），若患者为致病基因的纯合体，子女全部发病。
2. 此病与性别无关，男女发病的机会均等。
3. 在一个患者的家族中，可以连续几代出现此病患者。但有时因内外环境的改变，
致病基因的作用不一定表现（外显不全），一些本应发病的患者可以成为表型正常的致病基因携带者，而他们的子女仍有1/2的可能发病，
出现隔代遗传。
4. 无病的子女与正常人结婚，其后代一般不再有此病。


**常染色体隐性遗传病（AR）**

致病基因在常染色体上，基因性状是隐性的，即只有纯合子时才显示病状。此种遗传病父母双方均为致病基因携带者，故多见于近亲婚配者的子女。其特点是：

1. 患者是致病基因的纯合体，其父母不一定发病，但都是致病基因的携带者（杂合体）。
2. 患者的兄弟姐妹中，约有1/4的人患病，男女发病的机会均等。③家族中不出现连续几代遗传，患者的双亲、远祖及旁系亲属中一般无同样的病人。
3. 近亲结婚时，子代的发病率明显升高。


**性遗传（sex－linked inheritance）**

是指在遗传过程中子代的部分性状由性染色体上的基因控制，这种由性染色体上的基因所控制性状的遗传方式就称为伴性遗传，
又称性连锁（遗传）或性环连。许多生物都有伴性遗传现象。在人类，了解最清楚的是红绿色盲和血友病的伴性遗传。
红绿色盲在某个家系中的遗传情况。伴性遗传分为**X染色体显性遗传（XD）**（如：抗维生素D佝偻病，钟摆型眼球震颤等），
女性发病率高于男性；**X染色体隐性遗传（XR）**（如：红绿色盲，血友病等），
男性发病率高于女性；Y染色体遗传（如：鸭蹼病，人类印第安毛耳外耳廓多毛症等），只有男性发病。




## 染色体带型

**10q23.3**：p和q在染色体分别代表短臂和长臂；10q23.3 表示第10号染色体长臂的第2区3号带中的第3号亚带。如果亚带又再细分,则在原
亚带编号后再加数字,不需再加标点,例如10q23.31。请注意这些数字并非十进位的字,只是带型符号。

**t(1;3)(q25;q12)**：t 表示易位，translocation的缩写；t(1;3)(q25;q12)表示 1号染色体 长臂 2区5带 与 3号染色体 长臂 1区2带 发生了易位


## UPD

uniparental disomy, UPD: 单亲二体 [Wiki](https://en.wikipedia.org/wiki/Uniparental_disomy)

当一个人两个拷贝来源于一个亲本或染色体的一部分仅来源于一个亲本时，发生单亲二倍体（UPD）。 
UPD是卵子或精子形成期间发生的随机事件，或者是在早期胎儿发育中发生。

![](http://image107.360doc.com/DownloadImg/2017/06/2310/102552590_4)

在许多情况下，UPD可能对健康或发育没有影响。因为大多数基因没有印记，如果一个人从父亲遗传两个拷贝，
而不是从父母各遗传一个拷贝，这并不重要。然而，在一些特殊情况下，基因是否全部遗传自一个人的母亲或
父亲是有影响的。具有UPD的人(必需基因经历印记)可能缺乏活性拷贝。这种基因功能的丧失可导致发育延迟，
智力残疾或其他健康问题。

一些遗传疾病的发生是由UPD或正常基因组的印记印记导致的。最着名的病症包括Prader-Willi综合征，
其特征在于进食和肥胖不受控制; Angelman综合征，该疾病导致智力残疾和语言障碍。这些疾病都可以
由UPD或染色体15的长臂上的基因的印记中的其他错误引起。其它病症, 例如Beckwith-Wiedemann综合征
（以加速生长和癌性肿瘤的风险增加为特征的病症）与染色体11短臂上印迹基因的异常相关。

单亲二体可分为单亲同二体(isodisomy, 来自同一亲体的同一染色体)和单亲异二体(heterodisomy, 
分别来自同一亲体的两条同源染色体)


## 印记基因

[印记基因数据库](http://www.geneimprint.com)

 人体继承的基因，其两个拷贝一个来自母亲，一个来自父亲。通常两个拷贝的基因都是有活性的(表达出来)，
 或在细胞中被“开启”。然而，在一些情况下，两个拷贝中只有一个正常开启，基因的表达与否取决于它们是
 在父亲的染色体上还是在母亲的染色体上：通常一些基因只有当它们由父亲遗传时才是有活性的; 其他一些
 只有当从从母亲遗传时才是有活性的，该现象被称为基因组印记。

 经历基因组印记的基因在卵和精细胞形成期间，亲本的来源通常被标记或“印记”。该印记过程称为甲基化, 
 是将甲基团连接到DNA的某些片段的化学反应。这些分子可识别基因拷贝是遗传自母亲或者是父亲。甲基基
 团的的添加和去除可用于控制基因的活性。

 所有人类基因中只有小部分经历基因组印记。目前,研究人员还不确定为什么部分基因被印记，而其他基因
 却没有。但是，经研究他们知道印迹基因具有一定的倾向性，即在染色体的相同区域聚集。在人体中已经鉴
 定了两个主要的印迹基因簇，一个在染色体11的短（p）臂（在位置11p15），另一个在染色体15的长（q）
 臂（在区域15q11至15q13）



## LOH, AOH, ROH, LCSH

loss of heterozygosity, LOH: 杂合性丢失

杂合性丢失，是指（由于某些原因），染色体（整体或局部）杂合性丢失（曾经存在）。 
[ This term describes an event where heterozygosity (once present) is now absent]
是位于一对同源染色体上的相同基因座位的两个等位基因中的一个（或其中部分核苷酸片段）发生丢失，
与之配对的染色体上仍然存在。 [拷贝数异常]


absence of heterozygosity, AOH: 杂合性缺失

是指染色体（整体或局部）杂合性是不存在的。  [拷贝数正常]
[This term describes an observation where no heterozygosity is present]


runs of homozygosity, ROH: 

也有文献写作：regions of homozygosity. 拷贝数正常的纯和区域。 
[This term is specific to copy number neutral homozygosity]
[Does not apply to hemizygous deletions]

long contiguous stretch of homozygosity, LCSH:

等同于ROH，可以互换。[This term is interchangeable with ROH]


LOH、AOH、ROH和LCSH都在说纯合性现象。

后3个都是在说现象，而没有道出造成这种现象的原因，只有LOH透露出一点信息，是杂合性消失（丢失），
至于消失的原因是simi还是UPD，需要做定量分析。

LOH最先用在STR检测肿瘤组织DNA与癌旁组织DNA的扩增结果时发现并加以描述的，即原先是杂合性的位点变成
了纯合性的了。

在肿瘤样本中只检测到一个等位基因而呈纯合状态了。是一个等位基因丢失了（缺失），还是其中一个STR长度
发生了变动而使两个等位基因都是一样的长度了（没有缺失发生）？后来RDB检测肿瘤样本，也发现了同样的现象。
这是肿瘤中染色体不稳定的一个生物标记。如果没有个体配对样本的对照分析，出现这种纯合状态，只能说是
AOH（不存在杂合性）。

	* 用aCGH进行定量分析，不如SNP芯片提供的信息多。SNP芯片既显示拷贝数剂量（单倍体、二倍体或多倍体），
还显示基因型、揭示嵌合体等数方面的信息。会明确显示这种AOH是否有拷贝数的改变（缺失），loss了一个拷贝，
但不一定LOH，因为并不知道原先有无杂合性，需要用外周血以外的检材（例如口腔黏膜脱落上皮细胞）平行检测
才能证实。

	* 在NGS，也只能见到这种纯合现象，在正常人中出现杂合的多态性区域，检材出现纯合状态，若是个别的点，
	只能说是此位点“纯合”，若是多个（一溜儿，run）多态性位点出现纯合现象，就是ROH。
	
	长筒袜上出现跳丝，也叫run：先是一个小眼，如果用手一抻，脱扣更多，就像跑步一样，向两头延长了。

这种ROH提示缺失也可能是UPD，因为点突变不会有这么多点同时发生（N个点的突变率的积，可能性太低！）；
而UPD有可能是染色体损伤的抢救性复制，也可能是由于近亲婚配所致。若是近亲婚配所致，会在该染色体和其
他染色体多处出现ROH区域，而且亲源越近，片段越长、越多。若是单独出现，则多为缺失。如果这个run很长，
就属于LCSH了。


AOH 判定原则，需关注是否为微缺失微重复综合征，参考ACMG指南（2013 CNV guideline）

ROH 是否导致疾病?主要考虑2个因素：1. 区域内是否包含印记基因，如果ROH是由单亲二倍体UPD造成的，
那么有可能造成相关基因印记缺陷，从而导致疾病。2. 区域内是否包含于临床表型相关的基因？ 如果包
含相关基因，提示需对相关基因进行测序，以排除hot spot 或 founder mutation造成的纯合突变。

目前AOH最推荐的检测方案为SNP-ARRAY. 低深度全基因组测序受测序深度限制，尚不能进行genotype分析，
所以无法检测AOH. 全外显子组测序，进行参数优化后，可以在一定范围内分析AOH。但外显子区域仅占基
因组1%,其分析范围相对有限，通常不作为临床分子诊断应用。




## XO核型

女胎缺少一条X性染色体


## 染色体


![男性染色体](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1549947933615&di=6b04a917b190c3a28116ecad893e5fd5&imgtype=0&src=http%3A%2F%2Fbig5.cri.cn%2Fgate%2Fbig5%2Fnews.cri.cn%2Fmmsource%2Fimages%2F2005%2F09%2F06%2Fwc050906039.jpg)

在染色体狭窄处是着丝粒(centromere,cen), cen将染色体分为短臂(p)和长臂(q)。

染色体形态：

* 中央着丝粒染色体，cen位于染色体的1/2处
* 亚中着丝粒染色体，cen位于染色体的5/8处
* 近端着丝粒染色体，cen位于染色体的7/8处

根据人类细胞遗传学国际命名体制(ISCN),根据染色体的形态、大小和着丝粒位置将染色体分为7组：

* A组(大)：1-3
* B组(大)：4,5
* C组(中)：6-12,X
* D组(中)：13-15
* E组(小)：16-18
* F组(小)：19,20
* D组(最小)：21,22,Y

染色体的两端为端粒，是一种蛋白-DNA结构，含有TTAGGG六核苷酸重复延伸序列，保护染色体不被
降解，防止染色体末端融合，端粒缩短与细胞的寿命有关。

近端着丝粒染色体(13-15,21,22,Y)，除Y以外都具有随体，位于短臂末端介细丝连接的球状小体，
细丝部位是rDNAgene所在部位，转录rRNA进而形成核仁。


**1. 常用的正常和异常染色体的命名、缩写和符号**

`A～G` 染色体组；

`1～22` 常染色体序号；

`X,Y` 性染色体；

`/` 用于分开嵌合体不同的细胞系；

`+,` 放在常染色体号或组的符号之前时，表示整个染色体的增加或丢失；放在染色体壁、结构或其它符号之后时，表示染色体长度的增加或减少； 　　

`?` 染色体结构不明或有疑问，？应放在染色体组或号之前

`:` 表示断裂；

`::` 断裂和连接；

`;` 从几个染色体结构重排中，分开染色体和染色体区；

`→` 从……到……

`ace` 无着丝粒断片；

`cen` 着丝粒

`chi` 异源嵌合体；

`ct` 染色单体；

`del` 缺失

`der` 衍生染色体； 

`dic` 双着丝粒； 

`dup` 重复； 

`end` 内复制； 

`g` 裂隙； 

`h` 次缢痕；

`i` 等臂染色体； 

`ins` 插入； 

`inv` 倒位； 

`inv ins` 倒位插入；

`inv(p-q+)/inv(p+q-)` 臂间倒位； 

`mar` 标记染色体； 

`mat` 来自母亲； 

`mos` 嵌合体（同源）； 

`P` 染色体短臂； 

`pat` 来自父亲； 

`Ph` 费城染色体； 

`q` 染色体长臂； 

`r` 环状染色体； 

`rcp` 相互易位； 

`rea` 重排； 

`rec` 重组染色体；

`rob` 罗伯逊易位；

`s` 随体；

`sce` 姐妹染色体互换；

`t` 易位；

`tan` 连续（串联）易位；

`ter` 末端；

`pter` 短臂末端；

`qter` 长臂末端；

`tri` 三着丝粒。

**2.染色体临床意义：**

[各种综合征](http://www.biodiscover.com/news/industry/115442.html)

***1、性染色体数目和形态异常 ***

(1) **[X染色体缺失] 特纳（Turner）综合征**：45，X染色体为45个，只有1个X染色体。表型为女性，但性腺发育不全，第二性征发育延迟或发育不全。
个短小，耳畸形低位、高腭、小颌、后发际低、短颈、有颈蹼、盾状胸、乳距宽、肘外翻及智力可能有轻度缺陷等。 　　
尚有核型为45，X/46，XX嵌合体；X染色体长臂缺失；X染色体短臂缺失；X染色体长、短臂均缺失；环状X染色体；
X染色体长臂等臂染色体及X染色体与常染色体易位等亦可能有轻重不同的Turner氏综合征表现。 　　

(2) **[X染色体过多] 47,XXX 48,XXXX 49,XXXXX及它们与正常染色体组成的嵌合体**。表型多为女性，有的有性腺发育不全，也有无明显异常且有生育能力。 　　

(3) **[Y染色体过多和异常] 克林费尔特（Klinefelter）综合征**；47，XXY 患者为男性，多半身材高大，具小而硬的睾丸，
精子缺乏，多有乳房发育，呈女性体型，体毛稀小，臂和腿较长和智力可能迟钝。 　　
47，XYY核型较上为少见，患者为男性，多半身材高大，受寻衅，智力较差，可能有精神病和违法行为，
亦有相当一部分人没有临床上的异常表现。 　　

(4) **两性畸形** 真两性畸形患者既有睾丸又有卵巢组织。其体态，第二性征及外生殖器等似女又似男。
其染色体核型大多是46，XX，少数偶可为46，XY或为46，XX/46，XY、45、X/46，XY等的嵌合体。 　　
睾丸女性化综合征患者的外貌为正常的女性，但有XY染色体和睾丸组织。在XY性腺发育不全患者中，
其性腺和第二性征往往与特纳氏综合征一样发育不全。 　　

***2、常染色体数目及形态异常***

**DOWwn综合征（先天愚型）**：典型的21三体综合征，有47个染色体，多1个21号染色体，为常染色体异常中最多见的一种核型。
高龄产妇所生的婴儿中发生率较高。患者有明显的痴呆和外观、手掌、皮纹等多种特殊貌，患儿易感染且易患白血病，多数难活至成年。 　　
21与21，21与22，21与14等罗伯逊易位以及21三体与正常核嵌合型均可有轻重不等的先天愚型表现。 　　
优生学之任务是改善人口素质。开展产前诊断，进行遗传咨询，及早发现21三体综合征等遗传性疾病有重要的意义。 　　

**Edwad综合征系18三体综合征**，患儿有47个染色体，多1个18号染色体，于新生儿中的发生率约为1/4,500，多在分娩时或产后即死亡。
有多种畸形。 　　

**Patar综合征系13三体综合征**，有47个染色体，多1个D组的13号染色体，发生率大约为4/10万，有多种畸形，
多见于流产、早产儿或生后不久死亡的新生儿。 　　
此外在新生儿或流产中偶见8号三体、9号三体、22号三体综合征及双三体（即在同1个个体中有两种三体，例如：既有21三体又有X三体）。
其余各对之三体十分罕见，往往只在自然流产中见到。 
常染色体的缺失多为致死性，极少能存活。偶见21单体、13单体和22单体的报道。 　　

***3、常染色体结构异常***

主要类型有：部位臂缺失；部分臂重复及各种各样的易位……等。 　　

(1) **5P-综合症**：因患儿哭声似猫叫故亦称“猫叫综合征”，在其5号染色体上短臂部分缺失。有头小、眼距宽、
眼裂外侧下倾、耳位低，通贯手等多种畸形，约一半患者有先天性心脏病，智力低下，生活能力差，常早亡。 　　

(2) **4P-综合征**：类似5P-综合症，但常更为加重，还可呈尿道下裂，腭裂、严重的精神及运动障碍，癫痫发作等，属少见病例。 　　

(3) **18P-综合征**: 偶有成活者。 

(4) **染色体断裂综合征**：可见大量染色体断裂，多由于范可尼（Fanconi）综合征与Bloom综合征。 　　

(5) **脆性X染色体综合征**：在病理情况下，某些染色体断裂发生的频率很高，称之为脆性染色体。本病即是其中之一种，
在无（低）叶酸的培养基中培养后，在Xq27-28部位容易出现断裂或裂隙。病人以男性多见，呈智力低下，孤僻、长脸、大耳、
大睾丸、大生殖器、颌部突出等状；在女性症状较轻，约1/3表现为轻度智力障碍。 　　

(6) **费城染色体（Ph’）**：因首见于美国费城（Philadelphia）而命名。系其22号染色体部分长臂接到9号染色体长臂的一种易位。
为慢性粒细胞白血病可见到的特殊的染色体异常，但在其他少数急性白血病中偶可见到。这也是恶性细胞染色体变异中唯一已被公认
确实具有恒定变化的染色体变异。 　　


## 剂量敏感基因(Dosage Sensitivity Gene)

**单倍剂量不足**

最近在解读过程中，接触到一个新的名词-单倍剂量不足，它的英文名字叫做Haploinsufficiency。
单倍剂量不足指一个等位基因突变或者缺失后后，另一个等位基因能正常表达，这种基因表达翻译后
的蛋白水平只有正常的50%，但不足以维持正常的生理功能，导致特定表型出现。

导致单倍剂量不足的愿意可能有多种，比如一个基因的拷贝发生缺失，或者突变导致不能产生正常
的mRNA，或者特殊情况下mRNA或蛋白质不稳定导致降解等。

与解读相关的是，单倍剂量不足现象是导致遗传病发生的一个原因，如果一个基因存在单倍剂量不
足的机制，loss of fucntion或者gene deletion可能会导致疾病发生。具体到日常解读中，遇到
LoF或者gene deletion，我们可以通过查询NCBI的ClinGen和ExAC的pLI（loss-intolerance）来查
看基因是否存在单倍剂量不足，进而寻找可能致病的线索。

**ClinGen的Haploinsufficiency score**

ClinGen有一个分级系统，根据Haploinsufficiency score的分级结果，预测基因功能缺失突变（LOF）
或拷贝缺失与临床表型的相关性。ClinGen成立了EBR工作组，建立一个分级系统，用来系统评估CNVs的
可能临床相关性，该分级系统参考以下内容：已报道的致病突变数，遗传方式，表型一致性，大规模
case-control研究，致病机制，公共人群数据库，专家共识。并且会定期整合新的证据和重新评估。
ClinGen评估了Loss of fucntion和triplosensitivity（基因发生duplicate），分数从0-3，分值越高
则有更多的证据表明这个基因的剂量敏感导致相应临床表型。1表示少量证据表明与表型相关，3表示大
量证据表明与表型相关，此外，针对剂量不敏感的基因，给40的score，引起AR疾病的基因，评分为30的
score。

**[ExAC的pLI score](https://decipher.sanger.ac.uk/info/loss-intolerance)**

我们还得聊一聊另一个预测值pLI，它指的是基因对于LOF突变的不可忍受的可能性。
The Exome Aggregation Consortium (ExAC) 通过分析60,706 不同族群的个体外显子数据，
计算了pLI分值，来表示基因 不耐受Loss of Function (LoF) 突变。ExAC通过模型比较每个基因内观察到
的罕见突变和期望的罕见突变数据，通过Z score量化这种偏离。编码区的长度来减少混杂因素，对于蛋白
截断突变（Protein Truncating Variants (PTV) ），通过比较PTV在观察和期望中的数据，将基因分成3类。

* `Null`, 观察约等于期望，对LoF突变耐受 where observed ≈ expected (LoF variation is tolerated) 
【即使纯合缺失，也不会引起表型变化】
* `Recessive`, 观察得到的小于期望的50%，杂合LoF耐受 where observed ≤ 50% of expected (heterozygous LoFs are tolerated)
【杂合缺失，不会引起表型变化，但纯合缺失会引起变化】
* `Haploinsufficient`, 观察得到的小于期望的10%，杂合LoF不耐受where observed < 10% of expected (heterozygous LoFs are not tolerated) 
【杂合缺失，会引起表型变化】

pLI分值是一个给定基因归类到Haploinsufficient 类别中的概率，也就是对LoF不耐受的分值。分值越高，
越不耐受（intolerant），分值越低，越耐受（tolerant）。当然，具体运用中，不能仅根据pLI值就判定
一个LOF突变的致病性，我们还要同时考虑如疾病发病年龄，外显率，Haploinsufficiency score等。
【高pLI(>=0.9), 基因对LoF极度不耐受，也就是杂合缺失会引起表型变化；低pLI(<=0.1),基因对LoF极度耐受，
也就是纯合缺失也不会引起表型变化】


## 正义链(sense strand)和反义链(antisense strand)

与mRNA核苷酸序列相同的那条链(U代替T),称编码链或正义链

DNA双链分子中只有一条链通过碱基互补原则转录为一条mRNA链,指导合成RNA的那条链称模板链或反义链或转录链.



## 冈崎片段(Okazaki fragment)

冈崎片段（英语：Okazaki fragment）是DNA复制过程中，一段属于不连续合成的延迟股，
即相对来说长度较短的DNA片段。

冈崎片段之所以存在是因为DNA聚合酶无法在模板DNA的5'端往3'端的方向上合成DNA，
因此只能反向合成在模板DNA上产生了许多以3'到5'方向合成的冈崎片段（复制的片
段与模板DNA方向相反，故依旧是5'往3'），再由DNA黏合酶将其黏合。在前导链
（领先股）上DNA的合成是连续的，在后滞链（延迟股）上则是不连续的。




## 基因组变异检测

* [biostar handbook(十)|如何进行变异检测](https://www.jianshu.com/p/2a0ee4a010cb)
* [Freebayes Call SNP](http://www.bioinfo-scrounger.com/archives/254)
* [Samtools+bcftools Call SNP](http://www.bioinfo-scrounger.com/archives/248)

### 基本概念

常见的基因组变异一般可以归为如下几类：

* SNP， 单核苷酸多态性, 一个碱基的变化
* INDEL，插入或缺失, 一个碱基的增加或移除
* SNV， 单核苷酸变异，一个碱基的改变，可以是SNP，也可以是INDEL
* MNP， 多核苷酸多态性，一个区块中有多个保守的SNP
* MNV，多核苷酸变异，一个区块中有多个SNP或INDEL
* short variations, 小于50bp的变异
* large-scale variation, 大于50bp的大规模变异
* SV, 结构变异，通常是上千个碱基，甚至是染色体级别上的变异

研究这些变异需要用到不同的手段，其中普通的DNA二代测序在寻找20bp以下的变异比较靠谱，对于大于1kb的结构变异而言，
采用光学图谱(Bionanogenomics)可能更加靠谱一点。因此，对于目前最常用的二代测序而言，还是尽量就找SNP和INDEL吧，
几个碱基的变化找起来还是相对容易些和靠谱些。

对于SNP的定义这里也要注意下，最初的SNP的定义指的是单个碱基导致的多态性，在群体中广泛存在(1%)，
可用来作为分子标记来区分不同个体。目前的定义比较粗暴一点，就是那个和“参考基因组”不同的单个位点。
值得注意的是，这个概念可能不同人还有不同的定义，当你和别人就某个问题争执的时候，最好问问他是如何定义这个基本概念。
由于SNP的广泛存在，并且变异可能会导致疾病，也就是存在某些SNP会导致疾病。
Online Mendelian Inheritance in Man,就是一个人类遗传疾病数据库，建议去看下。

最后说下genotype和haplotype。

* genotype，基因型指的是一个个体的遗传组成。但是对于基因组变异而言，基因型通常指的是个体在某个位点上的等位基因情况。
* haplotype, 单倍型最初指的是从单个亲本中遗传的一组基因，而在基因组变异背景下，则是指一组变异。


### 检测流程

变异检测(variant calling)即通过比较参考序列和比对结果来找到两者的不同并记录，基本上可以分为如下几步：

* **序列比对**
* **比对后处理(可选)**
* **从联配中确定变异**
* **根据某些标准进行过滤**
* **对过滤的变异注释**

这里面的每一个可选的工具都有很多，不同工具组合后的分析流程得到的结果可能会有很大差异。

#### 变异检测

这一部分目前就有很多软件，但是常用并且相对比较可靠的工具有如下几个：

* **bcftools**: http://www.htslib.org/doc/bcftools.html
* **FreeBayes**: https://github.com/ekg/freebayes
* **GATK**: https://software.broadinstitute.org/gatk/
* **VarScan2**: http://varscan.sourceforge.net/

当然这些工具最初都是用于人类基因组。

例子

```
# 以埃博拉基因组为例完成一次简单的Variant Calling，所需工具为efetch, fastq-dump, 
# emboss/seqret，bwa, samtools和FreeBayes和snpEff。这些都可以通过conda快速安装。

# 第一步： 获取参考基因组序列，并建立索引

# 建立文件夹
mkdir -p refs
# 根据Accession下载
ACC=AF086833
REF=refs/$ACC.fa
efetch -db=nuccore -format=fasta -id=$ACC | seqret -filter -sid $ACC > $REF
bwa index $REF

# 第二步： 获取需要比对的测序数据， 以前10w条为例

# 仅要前10w条read
SRR=SRR1553500
fastq-dump -X 100000 --split-files $SRR

# 第三步：序列比对

BAM=$SRR.bam
R1=${SRR}_1.fastq
R2=${SRR}_2.fastq
TAG="@RG\tID:$SRR\tSM:$SRR\tLB:$SRR"
bwa mem -R $TAG $REF $R1 $R2 | samtools sort > $BAM
samtools index $BAM

# 第四步：使用freebayes或HaplotypeCaller(GATK4)检测变异

freebayes -f $REF $BAM > ${SRR}_freebayes.vcf
gatk HaplotypeCaller -R $REF-I $BAM -stand-call-conf 30 \
    -bamout bamout.bam
    --genotyping-mode DISCOVERY
    -O ${SRR}_haplotypecaller.vcf

# 用IGV可视化
# 这是最简单的变异检测流程，对于找到的变异还可以进一步过滤

# 第五步：变异标准化（可选）
# 大部分软件，如GATK， freebayes已经是标准化的结果。
bcftools norm -f $REF SRR1553500_freebayes.vcf  > SRR1553500_freebayes_norm.vcf
```

注释：

1. 变异标准化

由于VCF文件的灵活性，同一种变异可以通过不同的形式表示, 如下图

![](https://upload-images.jianshu.io/upload_images/2013053-2c0545f3d78aa314.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/546/format/webp)

变异标准化按照如下规则对变异位点表示进行简化

* 尽可能以少的字符表示变异
* 无等位基因可以标识为长度为0
* 变异位点必须左对齐

2. samtools + bcftools 来call变异
```
samtools mpileup -guf hg19.fasta test.bam > test.bcf
bcftools call -vmO z -o test.vcf.gz test.bcf
```


#### 变异注释

* [突变注释工具SnpEff,Annovar,VEP,oncotator比较分析](https://www.jianshu.com/p/6284f57664b9)

变异注释意味着猜测遗传变异(SNP, INDEL, CNY, SV)对基因功能，转录本和蛋白序列以及调控序列的影响。为了对变异进行预测，
预测软件需要你提供基因组注释信息，并且注释信息的完善程度决定了预测的准确性。变异预测一般会提供如下结果

* 变异位点所在基因组注释的位置，是转录本上游，还是编码区，还是非编码RNA
* 列举出收到影响的转录本和基因
* 确定变异在蛋白序列上的影响， 如stop_gained(终止密码子提前), missense(错义), stop_lost(终止密码子缺失), frameshift(移码)等
* 对于人类，还可以和已知的位点进行匹配

这些效应的定义可以在序列本体论查询.

变异注释常用软件有：VEP, snpEFF, AnnoVar, VAAST2. 其中VEP是网页工具http://asia.ensembl.org/Tools/VEP, 使用很方便，
可惜支持的物种有限。snpEFF可以说是支持物种最多的工具，这里使用它。


例子：

```
snpEff databases > listing.txt
# 确认物种名
grep -i ebola databases
# 下载
snpEff download ebola_zaire
# 下载之后还需要检查一下snpEFF提供的注释是否和我们所使用参考基因组一致.
snpEff dump ebola_zaire | less

snpEff ebola_zaire ${SRR}_freebayes.vcf > ${SRR}_annotated.vcf
# 最终会生成注释后的VCF文件以及变异位点的描述性报告。
```


## homozygous/hemizygous/heterozygous deletions区别

[What is the Difference Between a Hemizygous and Heterozygous Deletion?](https://tinyheero.github.io/2016/06/04/hemi-vs-het-del.html)

I have been using the term hemizygous and heterozygous deletion interchangeably 
for the last few years to describe a single allele/copy deletion in cancer 
genomes. But it was recently brought to my attention that the term heterozygous 
dletion is not always correct when describing single copy deletions. The term 
heterozygous implies that the original two alleles of a genomic locus were 
different. But we may observe a single allele deletion where the original two 
alleles were identical. In this case, this would not be a heterozygous deletion, 
but rather it would be a hemizygous deletion which implies there is only copy 
remaining but makes no claim that the two original alleles were different.

So basically if you are describing a single allele/copy deletion, then it is 
always safe to call it a hemizygous deletion. You can only call it a heterozygous 
deletion if you are sure that the original two alleles were actually different 
from each other.



上边的解释可能有问题，要想正确回答这个问题，需要搞清楚homozygous(纯合子)/hemizygous(半合子)/heterozygous(杂合子)的概念。


* `homozygous(纯合子)`：当等位基因的某一SNP位点碱基相同，我们称该位点为纯合位点。
* `heterozygous(杂合子)`：当等位基因的某一SNP位点碱基不同，我们称该位点为杂合位点。
* `hemizygous(半合子)`：某个没有等位基因的基因的某一SNP位点，我们称为半合位点。(如男性X染色体上的大部分基因都是半合子)

以上是我自己总结的概念，可能不准确，如有疑问请看[Wiki](https://en.wikipedia.org/wiki/Zygosity#Heterozygous)



----



# 技术原理

## PGS/PGD

胚胎植入前遗传学筛查(Preimplantation Genetic Screening)/胚胎植入前遗传学诊断(Preimplantatin Genetic Diagnosis)

### FISH

荧光原位杂交技术(Fluorescence In Situ Hybridization)

**1.FISH的前世今生**

在FISH技术问世之前，基于20世纪60年代，放射性核素探针的原位杂交方法，检测间期染色体和分裂期染色体上
特定DNA和RNA序列的方法，该方法存在操做比较麻烦、分辨率有限、探针不稳定、放射性同位素的危害较高等问题，
故目前弃之不用。20世纪80年代用非放射性半抗原如生物素进行核酸标记的技术逐渐开展后，探针也开始使用这种
非放射性标记方法。随后FISH技术逐渐开展起来，1986年以后该技术被应用于分析细胞分裂期染色体铺片的DNA序列。
相对于放射性来说，FISH具有稳定性好、操作安全、结果迅速、空间定位准确、干扰信号少、一张玻片可以标记多
种颜色探针等优点。这些优点逐渐使FISH成为一种研究分子细胞遗传学很好的方法。

FISH即染色体荧光原位杂交(Flourescence in situ hybridization,FISH)是通过荧光素标记的DNA探针与样本细胞核
内的DNA靶序列杂交，从而获得细胞核内染色体或基因状态的信息。FISH是将传统的细胞遗传学同DNA技术相结合，开
创了一门新的学科——分子细胞遗传学。（如下图所示)

![](https://mmbiz.qpic.cn/mmbiz_png/kMeQ2TpoXzo1fMadhxq6WHR205wPw1JkSwjdow97lQB2aD0IWR0dy6YFrUU2ng1AzvBRHoibSR2V37HiaP9EeKug/0?wx_fmt=png)

**2.FISH信号解读-红红绿绿是什么**

目前临床上用于FISH检测的探针的荧光素大都是绿色的和橙红色标记，可大致分为：染色体计数(着丝粒)探针
(centromere-enumeration probes，CEP)，位点特异性识别探针(locus-specific identifier probes，LSI)，染色体
涂染(paint，WCP)探针。其中CEP和LSI探针中的计数探针、融合探针及分离重排探针，在血液病诊断与预后分型中最
为常用。比如骨髓增生异常综合征(MDS)中8号染色体数目会增加;又或者多发性骨髓瘤(MM)中IGH基因的结构重排和
AML-M3中的PML/RARA融合基因。检测的结果可以是扩增、缺失、融合、断裂等。

![](https://mmbiz.qpic.cn/mmbiz_png/kMeQ2TpoXzo1fMadhxq6WHR205wPw1JkyDy5Jn7X9527EUicRJBiaziarH7uVBd4hm0WoQvxtXQKjiaaT3L9a8fHgA/0?wx_fmt=png)

**3.计数探针的原理**

通过标记某条染色体或者是某个基因特有的特异性DNA片段，与目的基因相结合，从而产生荧光杂交信号。由于正常人
的染色体是二倍体，那么正常人的检测信号就是两个，当信号多于两个或者少于两个(排除切片影响)，该染色体或者基
因就异常(扩增或缺失);如下图8号染色体三体。

![](https://mmbiz.qpic.cn/mmbiz_png/kMeQ2TpoXzo1fMadhxq6WHR205wPw1JkmtuHhicRutxnmVZMMicXSVXqoGyqLbbQB7icIjsJO3spxXhunEibW0tQ9Q/0?wx_fmt=png)

**4.双色双融合探针的原理**

含有用两种不同颜色荧光素标记的探针(一般用绿色和橙红色两种)，分别对应两个独立的靶基因位点，当两个独立的靶
基因位点相互融合就会形成典型的两个融合信号(黄色)和一个正常的绿色信号及一个正常的红色信号;如下图慢性粒细胞
白血病BCR/ABL融合基因形成模式图。

![](https://mmbiz.qpic.cn/mmbiz_png/kMeQ2TpoXzo1fMadhxq6WHR205wPw1JkCkqVS1fmWChyzTB8gzpCM5INMlEOASPV357vFBp9jhwATeWziawlib7Q/0?wx_fmt=png)

**5.重排探针的原理**

某基因发生重排时会在相对恒定位置断开，通过不同颜色荧光素标记断裂点两端特异性的DNA片段，该基因没有发生重排，
红色和绿色靠近会发生混合色形成黄色;如果发生断裂，则形成单独的颜色(如单独的红或绿)，当然，重排探针同样能够
提示数目异常(如多倍体)。如下图IGH基因的重排。

![](https://mmbiz.qpic.cn/mmbiz_png/kMeQ2TpoXzo1fMadhxq6WHR205wPw1JkY8PG8JaxSsq4jL0yNLdsKZgceibCs1lQYc7VoibOlv0xPZD9KyYoFqNg/0?wx_fmt=png)

**6.FISH检测的优势是什么**

FISH技术一般用于了解基因或染色体发生扩增、缺失、融合或断裂，只需分析间期细胞，每次可分析间期细胞500-1000个，
不受细胞是否分裂的影响，能更好地全面判断患者某种染色体异常比例。由于使用的是特异的探针，使人为的判断误差大
大减小。根据荧光信号判断结果，比染色体分析获得结果更加快速，重复性好。


### Array-CGH

* [瑞因生物_256的博客](http://blog.sina.com.cn/s/blog_c32c9b250101ddx7.html)
* [医学遗传中心](http://www.e3861.com/cn/keshizhuanjia/yixueyichuanzhongxin/5521.html)

DNA拷贝数变化（CNV）在许多人类疾病（如癌症、遗传性疾病、心血管疾病及糖尿病）的发生发展中起重要作用，但因为
CNV在健康个体间也普遍存在，因此理解特定疾病的分子机制的关键在于鉴定出正常和畸变染色体间的差异。

比较基因组杂交（CGH）是检测基因组DNA的片段扩增或缺失的有效方法，而基于微阵列技术的比较基因组杂交（aCGH）通
过在一张芯片上用标记不同荧光素的样品（肿瘤样品和对照样品）同时进行杂交可检测样本基因组和对照基因组间DNA拷
贝数变化（CNV），常用于肿瘤及遗传性疾病全基因组CNV检测，直观地表现出肿瘤及遗传性疾病基因组DNA在整个染色体
组的缺失或扩增，对肿瘤而言缺失部位可能包含抑癌基因，而扩增片段则可能存在致癌基因。

微阵列比较基因组杂交(array comparative genomic hybridization ,aCGH) 技术是在CGH技术基础上发展起来的新的染
色体病诊断技术,仅需少量的DNA 即可系统地检测整个基因组DNA 的扩增或缺失。与传统的核型分析相比，ArrayCGH不需
要细胞培养、分辨率高、操作简单、自动化程度高，且软件分析结果减少了人为主观因素产生的误差，ArrayCGH分辨率能
够达到0.05 Mb,可以检测到一些核型分析检测不到的染色体的微小缺失或重复，是研究整个基因组缺失或重复的非常有应
用前途的分子细胞遗传学技术。ArrayCGH被美国人类遗传学杂志推荐为不明原因发育迟缓、智力低下、自闭症、多发畸形
的首选遗传学诊断方法。

1、技术原理（用图说明）

![](http://www.e3861.com/userfiles/images/3_%E5%89%AF%E6%9C%AC.jpg)

2、应用举例：检测普拉德•威利/ 天使(PWS/AS)综合症

![](http://www.e3861.com/userfiles/images/TM%E6%88%AA%E5%9B%BE%E6%9C%AA%E5%91%BD%E5%90%8D_%E5%89%AF%E6%9C%AC.jpg)


**1.什么是拷贝数的变异(CNV)？**

人类的基因组是由包括60亿个化学碱基（或者称为核苷酸）的DNA组成的，并被包装到23对染色体中，每对染色体都是一条
来自父代，一条来自母代。这些DNA编码大约30,000个基因。过去通常认为基因在基因组中是以2个拷贝的形式存在，然而
目前的发现已经表明：有大量的DNA片段在拷贝数上有很大的变异，这些DNA片段的大小从数千到数百万碱基不等。这些拷
贝数的变异（简称CNVs）包含拷贝数改变的基因，比方说，那些过去认为每对染色体上存在2个拷贝的基因，现在发现有时
是1个拷贝，有时是3个甚至3个以上，在少数罕见的情况下这些基因还会一起缺失。

**2.为什么说CNVs很重要？**

染色体上DNA序列的不同决定了我们个体的独特性，包括对疾病的易感性等等。过去认为DNA的单核苷酸的改变（称为SNPs
单核苷酸多态性）是基因变异的主要形式，最近的研究发现CNVs的发生率至少是SNPs的3倍。因为CNVs中经常包含一些在人
类疾病发生和对药物的反应中起着重要的作用的基因，所以理解CNV形成机制能够帮助我们更好地理解人类基因组的进化。

**3.新的CNV图谱有什么帮助？**

新的CNV图谱能够在三个领域对医学研究有帮助：首先也是最重要的，就是能够帮助寻找与常见疾病相关的基因，到目前为
止，还没有真正认识到这些基因的CNVs在人类健康中所起的作用，我们正试图证明这一点；第二，CNV图谱正被用来研究家
族遗传病；第三，数千种严重的发育缺陷正是由于染色体的重排引起的，CNV图谱被用来排除在未受影响个体上变异的发生，
帮助研究人员确定可能涉及到的目标区域，整个数据的生成要归功于一个更加精确及完整的人类基因组参考序列。

**4.最近文章中有什么令人惊奇的发现？**

最令人吃惊的发现是，在270份被测的DNA样品中，人类基因组中有12%发生了拷贝变异，大约2900个基因，或者说已知基因
的10%都包括在这些CNVs中。在普通人群中一些CNVs有数百万个碱基的大小，影响到大量的基因，但却没有明显可见的结果。

**5.在人类基因组中有多少CNVs？他们有多大？**

到目前为止，大约发现有2000CNVs，其中1447个是最近的研究刚发现的，在人群中可能有数千个CNVs，大约有100个CNVs发生
在每个基因组中，平均大小为250,000碱基（基因的平均大小为60,000碱基）。更多的CNVs会随着检测技术的进步和对来自世
界范围人群更多的DNA样品的检测而被发现。

**6. CNVs会导致疾病吗？**

大部分的CNVs不会直接导致疾病。然而也有一些例子表明若发生CNVs的部位影响了关键的发育基因，就会导致疾病。比如说，
最近的综述分别列出了17种神经系统疾病——包括帕金森症和阿尔兹海默症——他们都源于拷贝数变异。为了增加数据的可信度，
Sick  Chidren医院针对在人群中发现的家族CNVs建立了“基因变异数据库”。Well Trust Sanger学院也开发了与临床疾病相
关的CNVs的数据库（称为DECIPHER）。

**7.哪种类型的基因会发生拷贝数变异(CNV)？**

那些涉及到免疫系统和大脑的发育及功能活动的基因——这两个功能在人类中得以快速进化——往往有很多CNVs。另一方面，在
早期发育中起重要作用的基因和一些参与细胞分裂的基因——也都对基础生物学有关键作用——却不发生CNVs。

**8.人群中有特异的CNVs吗？**

随着所有类型基因变异的发生，CNVs也在人群间发生着频率及发生上的改变，这告诉了我们一些事情――我们共同的起源是在
非洲，大量的拷贝数变异（大约89%）共同出现在不同的人种中。不过我们每个人所继承的CNV的特征却精确的反映了我们的
血统，并且能够用于推断我们目前来自三大洲中的哪个。在不同大洲人群间研究CNVs能够帮助研究基因变异（这些变异是由
于不同人群为了适应不同的环境而产生的，例如在非洲人群中，与HIV相关的CCL3L1基因的拷贝数显著增加），而理解基因
变异在人群中分布情况的不仅能告诉我们人类的史前史，而且能帮助我们发现致病基因。

**9.aCGH芯片技术的发展趋势如何？**

下一代的aCGH芯片技术将保证无论大的和小的CNVs都能被检测到，新的DNA测序技术的实现和“个体”基因组测序计划相结合，
相信最终能够捕获基因组上的每一个变异。


## CNV-seq

前言

CNV，即拷贝数变异（copy number variation），一般指长度为1kb到几个Mb基因组大片段的拷贝数复制、缺失。CNV在基因组
中的存在形式主要有以下几种：两条同源染色体拷贝数同时出现缺失；1条同源染色体发生缺失，1条正常；一条同源染色体出
现拷贝数重复，另一条正常；1条同源染色体出现缺失，另一条出现拷贝数重复；两条同源染色体同时出现拷贝数重复。

CNV在人类基因组中分布广泛，是人类疾病的重要致病因素之一。致病性CNV可引起智力障碍、生长发育迟缓、自闭症、各种各
样的出生缺陷、白血病和肿瘤等多种疾病。目前对CNV进行检测的方法主要有aCGH, SNP-array, CNV-seq、MLPA等，这些方法
各有哪些优缺点，我们又该如何选择？

检测方法一：aCGH

aCGH也称为基于芯片的比较基因组杂交（array-based comparative genomic hybridization）。

原理：将等量的待测DNA和正常对照DNA分别用红色和绿色荧光染料标记，混合，然后与全基因组DNA芯片进行竞争性杂交。杂交
后的芯片经激光扫描，比较每个点红光和绿光的发光强度。若红光过强，表明待测样本拷贝数复制；若红光较弱，表明待测样
本拷贝数缺失；若红绿光均等，则表明待测样品拷贝数正常。

应用：可以检测全基因组水平上的CNV。

点评：aCGH的分辨率，取决于芯片中探针在全基因组中的密度和探针长度。安捷伦SurePrint G3 Human CGH Microarray 1×1M芯
片中，探针间距约为2kb。因为来自一个点的荧光的光强变化，可能会带有一定的偶然性，所以，一般是看染色体空间位置上相
邻的3个点（或者更多的点），如果这3个点的荧光比值，都发生同一个方向的偏离，就可以判断这一段有拷贝数变异的证据。
基于这点考虑，按照3个点计算，aCGH的分辨率约为6kb。

检测方法二：SNP-array

SNP（Single Nucleotide Polymorphisms，单核苷酸多态）是指在基因组水平上由单个核苷酸的变异所引起的DNA序列多态性而
形成的遗传标记。SNP在人类基因组中广泛存在，平均约每500-1000个碱基对中就有1个SNP，人类30亿碱基中大约有300万个。

原理： 与aCGH采用的双杂交策略不同的是，SNP-array利用待测样本与芯片探针进行单杂交，通过比较不同样本信号的强度来
确定每个位点的拷贝数。

应用：SNP-array芯片的探针为SNP位点序列，可以提供SNP信息。除可检测CNV外，还可检测单亲二倍体(UPD)、杂合性缺失(LOH)
和嵌合体。

点评：SNP 芯片探针在全基因组上的的密度非常大，分辨率很高。但是这些探针在基因组中并非均衡分布，在一些重复序列和复
杂的CNV 区域， SNP 密度是较小的，不能得到较为清晰的CNV 图谱。Affymetrix 公司和Illumina 公司在新一代芯片中增加一
个非多态性的探针，将探针更好地定位在特定区域，提高图谱的清晰度。目前Affymetrix 公司的CytoScan HD芯片为探针密度最
高的芯片，含有270万个探针，基因间探针间距平均为1kb。按照3个点计算，SNP-array的分辨率约为3kb。


检测方法三：CNV-seq

CNV-seq，即通过低倍全基因组测序检测CNV的技术，2009年由Xie[1]等开发提出。

原理：CNV-seq检测原理与aCGH相似。将等量的待测样本DNA和正常对照DNA建库测序后，分别与reference sequence进行对比。
通过比较两个样本每个滑窗内比对reads数目的多少来确定每个位点的拷贝数。

应用：可以检测全基因组水平上的大片段CNV。

点评：贝瑞和康采用双盲实验设计，对染色体结构异常的样本进行检测，滑窗大小为20kb的情况下，CNV-seq和高密度SNP-array
对于已知致病CNVs都能达到100%的检出[2]。与中等密度SNP-array相比，CNV-seq表现更优。鉴于CNV-seq价格较低，CNV-seq可
以替代微阵列芯片用于大片段CNV检测。关于CNV-seq的分辨率取决于滑窗的大小。一般来讲，如果是低倍基因组测序，要使滑窗
内的reads数目可信的话，所取的滑窗不可能太小。根据文章2描述，以20kb滑窗大小计算，按照3个点计算，CNV-seq的分辨率约
为60kb。


检测方法四：MLPA

MLPA(multiplex ligation-dependent probe amplication，多重连接依赖式探针扩增)于2002年由荷兰学者Dr.SchoutenJP等首
先提出，是针对待检DNA靶序列进行定性和半定量分析的技术。

原理：在DNA靶序列的特定变异位点（如点突变）两侧设计一对MLPA探针。每条探针包含一段通用引物序列和一段特异性杂交序
列。杂交序列与靶序列杂交后，使用连接酶将两部分探针连接成一条核苷酸单链，再使用通用引物进行PCR扩增。通过比较待测
DNA与正常对照DNA的PCR产物量，来确定待测样本DNA靶序列的拷贝数。值得注意的是，连接酶很挑剔，只有在检测位点处探针与
靶序列完美互补配对的情况下，连接酶才能将两部分探针顺利连接成单链进行后续扩增。如果检测位点存在甲基化、点突变、
CNV，则探针连接失败，不能进行后续PCR扩增。

应用：验证高度怀疑的特定基因中的点突变、甲基化、CNV。

点评：该技术具有快速及特异性高的特点，但是不能对染色体组进行全局分析。单一反应管内可以同时检测40个不同的核苷酸序
列的拷贝数变化。


----

# 数据库

* [12个医学公共数据库](http://www.dxy.cn/bbs/topic/39055159?from=recommend)


## 肿瘤数据库

**NCDB**

美国国家癌症数据库(National Cancer Database, NCDB)是经国家认证的，由美国外科医师学会和美国癌症学会联合组建的，
它是一个基于医院登记数据的临床肿瘤学数据库，来源于超过1500多个癌症委员会认证的机构。NCDB数据库可用于分析和跟
踪恶性肿瘤患者的治疗过程和结局。数据库代表了全美超过70%的新诊断癌症病例和超过三千四百万个历史记录。

**SEER**

SEER(Surveillance, Epidemiology, and EndResults Program)是美国癌症统计的权威来源。SEER数据库可提供癌症统计信息，
以减轻美国人口中的癌症负担。SEER数据库由美国国家癌症研究所(National Cancer Institute,NCI)癌症控制和人口科学
部(Division of Cancer Control andPopulation Sciences, DCCPS)的监视研究项目(SurveillanceResearch Program, SRP)
提供支持。

**TCGA**

美国癌症基因组图谱(The Cancer Genome Atlas, TCGA)是由美国国家癌症研究所(National Cancer Institute, NCI)和
国家人类基因组研究所(NationalHuman Genome Research Institute, NHGRI)合作开发的，目前它包含了33种癌症的数据，
每种癌症都涉及关键基因组变化的全面、多维的图谱。TCGA数据库储存有2.5PB的数据，对超过1.1万多名患者的肿瘤组织
及配对正常组织进行描述，目前已被广泛应用于研究领域。这些数据已为独立研究人员进行的癌症研究或者TCGA研究网络
出版物做出了超过1千多项的贡献。

在TCGA中直接下载数据的方法较为繁琐，但是有多个网站提供TCGA数据(包括表达和临床等)完善的整理，以下是其中整理
最为完整和可靠的：

GDAC: http://gdac.broadinstitute.org/

Cancer Browser: https://genome-cancer.ucsc.edu/

cBioportal: http://www.cbioportal.org/index.do


**METABRIC**

国际乳腺癌协会的分子分类数据库(Molecular Taxonomy of Breast Cancer International Consortium, METABRIC) 
是一个加拿大-英国联合项目，旨在根据有助于确定最佳治疗过程的分子特征将乳腺肿瘤进一步分类。我们迄今为止已经
根据肿瘤的基因指纹将乳腺癌重新分类为10个全新的类别。这些基因可以对乳腺癌生物学提供迫切需要的洞察力，使医生
能够预测肿瘤是否会对某种特定的治疗产生反应。肿瘤是否有可能扩散到身体的其他部位，或者治疗后是否有可能复发。

**Kaplan Meier Plotter**

Kaplan MeierPlotter是一个包含5种癌症(乳腺癌、卵巢癌、肺癌、胃癌、肝癌)的mRNA表达谱芯片公共数据库，
从中能够获得基因表达与疾病预后的信息。


**COSMIC**

* [【数据库-2】COSMIC遗传资源数据库](https://www.jianshu.com/p/557f91d2d88e)

COSMIC是一个在人类癌症中发现的体细胞获得性突变的在线数据库。体细胞突变是在非生殖细胞中发生的，
不是由儿童遗传的。 COSMIC是癌症中体细胞突变目录(Catalogue Of Somatic Mutations In Cancer)的首
字母缩写，它从科学文献中的论文和桑格研究所癌症基因组计划的大规模实验筛选中提取数据。该数据库
可供学术研究人员免费使用，并可向其他人商业许可。



## 遗传疾病公共数据库

* `DECIPHER`: 国际公共致病性CNVs数据库
* `CliGen(原ISCA)`: 国际细胞基因芯片标准化联合会
* `OMIM`: 在线人类孟德尔遗传数据库
* `DGV`: 国际公共良性CNVs数据库

**DECIPHER**

[DECIPHER](https://decipher.sanger.ac.uk/disorders#syndromes/overview) 为“Database of Chromosomal Imbalance and Phenotype 
in Humans using Ensembl Resources”的简称，也是目前分子遗传学中最重要的生物信息学数据库之一。用户可以通过检索数据库，
发现一系列相关的遗传疾病信息，包括变异位点、临床表型等，提高临床诊断效能。DECIPHER数据库包含了超过200家研究中心上传的超过
10,000例的案例信息。

**OMIM**

* [OMIM简明使用说明](http://www.biotrainee.com/thread-1107-1-1.html)
* [【数据库-6】OMIM数据库](https://www.jianshu.com/p/dfcc37211bde)

[OMIM](http://www.omim.org/) 为“0nline Mendelian Inheritance in Man”的简称，意即“在线人类孟德尔遗传数据库”，是目前分子遗传
学中最重要的生物信息学数据库之一。数据库持续更新，主要着眼于可遗传的或遗传性的基因疾病，包括文本信息和相关参考信息、序列纪
录、图谱和相关其他数据库。

**DGV**

[DGV](http://dgv.tcag.ca/dgv/app/home) 为“Database of Genomic Variants”的简称，目的是提供人类染色体结构变异的概况信息，数据
库记录了一系列基因变异与表型相关的信息，数据库信息持续更新中。

**Orphanet**

[Orphanet](http://www.orpha.net/consor/cgi-bin/index.php?lng=EN) 数据库是为所有用户提供罕见病和罕见病药物信息的开放门户，
目的在于提高罕见病的诊断、护理和治疗效果。

**CNVD**

[CNVD](http://202.97.205.78/CNVD/) 为“Copy Number Variation in Disease”的简称，是哈尔滨医科大建立的数据库。

**ISCA**

[ISCA](http://dbsearch.clinicalgenome.org/search/)


**HGMD**

人类基因突变数据库（HGMD），从1996年开始，由英国Cardiff的医学遗传研究所维护，有17万4千种发表在文献上的由遗传
所引起的疾病的种系变异。


**ClinVar/ClinGen**

* [【数据库-4】clinvar](https://www.jianshu.com/p/0ff9d1c091f4)
* [ClinGen对BA1的修订：人群频率过滤要防的坑](https://bbs.genelinks.com/thread-1156-1-1.html)


在2012年，美国NIH开展了ClinVar，一个免费的数据库，旨在对生殖细胞和体细胞的变异进行临床解释。
它最初是从OMIM上及位点特异性数据得到数据提交，但很多从临床测试实验室和研究者直接获得数据提交。
ClinVar要求每个变异的分类为临床的类别（良性的，有可能是良性的，可能的致病性、致病性或不确定性的意义）。

为了促进ClinVar的数据提交和提高对变异的注解的准确性，NIH从2013年开始启动对ClinGen的经费支持。

ClinGen对提交给ClinVar的数据建立了一个排名体系。提交者提交的变异必须分成至少三个临床意义层，
提供区分方法和支持证据之后才能获得一星进入体系。用户可以在讨论他们的注解上与提交者接触。
二星级描述的是在大多数提交者没有冲突的变异。三星、四星来自于专家小组和大型团队。根据2016年1月4日的数据，
在ClinVar 172,870个变异中56,742至少达到一星级，对待没有星级的105,000收录条目应该谨慎一些。

通过不同的浏览器，ClinVar用户很容易获得不同提交者之间所有的变异注解的差别。这对有些实验室过度或低估致病变异
是有用的提醒，可能会促使他们改变自己的方法。

ClinGen已经为ClinVar中不同疾病的注解的差异提供专家意见。但为了达到这个需求，知识必须共享，临床实验室以及
那些做基因测试和从事基础研究的机构应使他们的变异数据可自由利用。


**gnomAD**

* [遗传资源数据库专题-gnomAD](https://www.jianshu.com/p/5696d6204446?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)

Genome Aggregation Database(简称gnomAD)是由各国研究者联合发展起来的基因组突变频率数据库。
其目的是汇集和协调来自众多大规模测序计划的全外显子组和全基因组测序数据，为广泛的科学研究团体汇总数据。

该数据库提供的数据集包括123,136个个体的全外显子组测序数据和15,496个个体的全基因组测序数据，
这些数据来源于各种疾病研究项目及大型人群测序项目。


**ExAC**

* [【数据库-7】ExAC数据库](https://www.jianshu.com/p/da8ddd7e4903)

ExAC数据库的全称是（the Exome Aggregation Consortium，外显子组整合数据库）,
该数据库旨在汇总和协调各种大规模测序项目的外显子组测序数据，并为更广泛的科学界提供摘要数据。
所有数据均基于GRCh37 / hg19。2016年8月，Nature刊登了一篇ARTICLE，主要重点就是哈佛-麻省理工Broad
研究所的科学家公布了60706名不同种族个体的外显子序列。整合了多个研究项目的外显子集合协作组（ExAC）
分析了来自不同祖先的共60706位个人的高质量外显子测序数据,通过深度分析制作的人类遗传变异数据库ExAC
并制定了每个序列变异的致病性的精确度量标准。研究鉴定了根据选择压力区别的突变类型；鉴定了3230个基因
截短突变，其中72%的基因没有与已知的人类疾病表型建立关系。ExAC数据库可以用来过滤潜在的致病性突变，
避免遗传误诊以及发现更多遗传性疾病的致病因素及根源提供了有力的工具。


**MalaCards**

* [【数据库-8】MalaCards人类疾病数据库](https://www.jianshu.com/p/e93934bccfd6)

MalaCards是人类疾病及其注释的综合可搜索数据库，综合各大数据库网站。


**dbSNP**

* [【数据库-3】dbSNP数据库](https://www.jianshu.com/p/3d8600af2928)

单核苷酸多态性数据库dbSNP(dbSNP, The Single Nucleotide Polymorphism Database）是由NCBI与人类基因组研究所
（National Human Genome Research Institute）合作建立的，收录了SNP、短插入缺失多态性、微卫星标记和短重复
序列等数据，以及其来源、检测和验证方法、基因型信息、上下游序、人群频率等信息。

dbSNP接受明显中性的多态性，对应于已知表型的多态性和无变异的区域。它于1998年9月创建，用于补充NCBI收集的
公众可获得的核酸和蛋白质序列GenBank。从构建131（2010年2月开始）开始，dbSNP已经收集了超过1.84亿份提交文
件，代表了55种生物的超过6400万种不同变种，包括智人，小家鼠，水稻和许多其他物种。 NCBI将在2017年逐步停止
对dbSNP和dbVar中的所有非人类生物的支持。


**1000 Genomes Project**

* [【数据库-1】1000 Genome Project 数据库](https://www.jianshu.com/p/2b7a8e52d201)

1000 Genomes Project（缩写为1KGP）于2008年1月启动，是一项国际研究工作，旨在建立迄今为止最详细的人类遗
传变异目录。科学家计划在接下来的三年内使用新开发的技术对来自不同种族群体的至少一千名匿名参与者的基因组
进行测序，这些技术更快，更便宜。 2010年，该项目完成了试验阶段，在“自然”杂志的一篇出版物中对此进行了详
细描述。2012年，1092个基因组的测序在Nature出版物中公布。 2015年，“自然”杂志上的两篇论文报告了结果，项
目的完成以及未来研究的机会。确定了许多罕见的变异，仅限于密切相关的群体，并分析了8个结构变异类别。

该项目将来自世界各地研究所的多学科研究团队联合起来，包括中国，意大利，日本，肯尼亚，尼日利亚，秘鲁，
英国和美国。每一个都将为庞大的序列数据集和精细的人类基因组图谱做出贡献，这些图谱将通过公共数据库免费
提供给科学界和公众。

1000 Genome Project 的目标是发现在人群中频率大于1%的变异位点，对来自不同人群的大量样本进行测序，识别
到了许多的变异位点，为人类遗传变异的研究提供了一个综合的资源。


* [印记基因数据库](http://www.geneimprint.com)


* [肿瘤学和血液学的遗传学和细胞遗传学图谱](http://atlasgeneticsoncology.org/Educ/PolyMecaEng.html)

小芳推荐的，挺好



## 其它

**Comparative Toxicogenomics Database**

比较基因组数据库(Comparative ToxicogenomicsDatabase, CTD)是一个强大的、公开可用的数据库，旨在提高人们对环境暴
露如何影响人类健康的了解。它提供了关于化学基因/蛋白质相互作用、化学疾病和基因疾病关系的相关信息。这些数据与功
能和路径数据相结合，以帮助验证关于环境影响疾病的机制假设。

**GEO**

基因表达库(Gene Expression Omnibus,GEO) 是一个支持微阵列实验的最小信息(MinimumInformation About a Microarray 
Experiment, MIAME)兼容数据提交的公共功能基因组数据存储库。可接受基于数组或序列的数据。提供相关工具帮助用户查
询和下载实验和管理基因表达谱

**WHO Mortality Database**

世界卫生组织死亡数据库(WHO Mortality Database)是对各个成员国的居民登记系统按照年龄、性别和死因汇编的每年死亡
数据。



## 在线资源

**UCSC**

hg19相关资源：http://hgdownload.cse.ucsc.edu/goldenpath/hg19/database/。
可以下到 `cytoBand`, `Affy相关芯片` 等等很多很多信息。

UCSC使用介绍：https://wenku.baidu.com/view/55edd1be3868011ca300a6c30c2259010302f338.html






----

# 软件

## 生物信息软件参数解析

### samtools

mpileup

* -g Compute genotype likelihoods and output them in the binary call format (BCF)(计算genotype likelihoods并以bcf格式输出)
* -f The faidx-indexed reference file in the FASTA format(用samtools faidx对参考序列建索引.fai文件，用其他软件建索引也可以的)
* -u Generate uncompressed VCF/BCF output(输出不压缩的bcf文件)
*-t Comma-separated list of FORMAT and INFO tags to output (case-insensitive)（按照自己的需求，输出vcf格式中常见的各种tags，比如-t DP输出vcf中的DP值；-t SP输出类似GATK call snp 出的VCF的GQ值？）

### bcftools

call

* -O Output compressed BCF (b), uncompressed BCF (u), compressed VCF (z), uncompressed VCF (v)(一般可以选择z,压缩的vcf格式)
* –threads Number of output compression threads to use in addition to main thread（主要用于压缩时的多线程，在-O b/z时使用）
* -m alternative modelfor multiallelic and rare-variant calling designed to overcome known limitations in -c calling model(一种更优的新算法，克服了旧算法的缺陷)
* -v output variant sites only(只输出突变位点信息)
* -f –format-fields 可以在输出的VCF文件中增加新的tag，例如增加GQ
* -V, –skip-variants 可以跳过输出snps|indels（比如我想只输出snps，则跳过indels）

filter

* -e –exclude 主要用表达式方式去除过匹配上的位点，这个参数很关键，很多过滤都依靠这个表达式
* -g, –SnpGap 过滤INDEL附近的snp位点，比如-SnpGap 5则过滤INDEL附近5个碱基距离内的SNP
* -G, –IndelGap 过滤INDEL附近的INDEL位点。。。应该是这个意思
* -o, –output 输出文件的名称
* -O, –output-type 输出的格式，一般z和v都行
* -s, –soft-filter 将过滤掉的位点用字符串注释
* -S, –set-GTs set genotypes of failed samples to missing value (.) or reference allele (0)（将不符合要求的个体基因型改为./.）


## python模块

### pysam

* [pysam: htslib interface for python](https://pysam.readthedocs.io/en/latest/index.html)
* [pysam - 多种格式基因组数据（sam/bam/vcf/bcf/cram/…）读写与处理模块（python)](https://www.cnblogs.com/nkwy2012/p/6558069.html)
* [如何使用Python处理BAM](https://zhuanlan.zhihu.com/p/31625187)
* [用python做生物信息数据分析（2-pysam）](https://www.jianshu.com/p/0a6eaed4d5e5)

在开发基因组相关流程或工具时，经常需要读取、处理和创建bam、vcf、bcf文件。
目前已经有一些主流的处理此类格式文件的工具，如samtools、picard、vcftools、bcftools，
但此类工具集成的大多是标准功能，在编程时如果直接调用的话往往显得不够灵活。

本文介绍的是一个处理基因组数据的python模块，它打包了htslib-1.3、samtools-1.3 和 
bcftools-1.3的核心功能，能在编程时非常灵活的处理bam和bcf文件。


*** 基础操作**

1.安装

如果Linux上安装了pip，可以一键安装
```
pip3 install pysam
```


2.读取bam文件(pysam.AlignmentFile)

bam是sam的二进制文件，因其占用空间少，所以都会使用bam进行存储和操作。

要读取bam文件,必须先创建一个`AlignmentFile`对象.

```
path_in = './test.bam'
samfile = pysam.AlignmentFile(path_in, "rb")
```

之后就可以逐行读取和处理bam文件了(顺序读取),以下打印出了bam的一行.

```
for line in samfile:
    print(line)
    break
```

其中，每个line都是`AlignedSegment`对象。

```
line = next(samfile)
print(type(line))
```


3.读取vcf/bcf文件(pysam.VariantFile)

读取方法同上,只是使用的是VariantFile方法:

```
gvcf = "./MHC.unified.g.vcf.gz"
vcf_in = pysam.VariantFile(gvcf)
```


4.创建并写入到新的bam或vcf文件

pysam的核心功能是可以随心所欲的读取数据,处理之后,写入到一个新建的bam或bcf文件里.

我们可以完全自定义一些内容,然后写入到一个新的bam文件里,如下:

```
header = { ‘HD‘: {‘VN‘: ‘1.0‘},
            ‘SQ‘: [{‘LN‘: 1575, ‘SN‘: ‘chr1‘},
                   {‘LN‘: 1584, ‘SN‘: ‘chr2‘}] }

with pysam.AlignmentFile(tmpfilename, "wb", header=header) as outf:
    a = pysam.AlignedSegment()
    a.query_name = "read_28833_29006_6945"
    a.query_sequence="AGCTTAGCTAGCTACCTATATCTTGGTCTTGGCCG"
    a.flag = 99
    a.reference_id = 0
    a.reference_start = 32
    a.mapping_quality = 20
    a.cigar = ((0,10), (2,1), (0,25))
    a.next_reference_id = 0
    a.next_reference_start=199
    a.template_length=167
    a.query_qualities = pysam.qualitystring_to_array("<<<<<<<<<<<<<<<<<<<<<:<9/,&,22;;<<<")
    a.tags = (("NM", 1),
              ("RG", "L1"))
    outf.write(a)
```
同理,我们也可以读取一个已有的bam文件,逐个修改以上的属性,然后存储到一个新的bam文件里.
这里不再举例.

上面设置header可能有点麻烦,容易出错,但我们可以复制一个已有bam文件的header到一个新的bam文件里.

```
outf = pysam.AlignmentFile(path_out, "wb", template=samfile)
```
以上template参数指定了模板bam文件.


5.关闭文件

```
outf.close()
```

总结:

pysam模块非常实用,有了pysam模块,我们就可以非常灵活的操纵bam/bcf文件,
而不必依赖于samtools或bcftools. pysam可以随机读取bam/bcf文件,
也可以将处理后的内容自定义输出到bam/bcf文件.


**API**

SAM/BAM/CRAM files

>pysam.AlignmentFile

>pysam.AlignedSegment(AlignmentHeader header=None)

* **aend**: 参考序列结束位置(抛弃，用reference_end代替)
* **alen**: 参考序列长度(抛弃，用reference_length代替)
* **aligned_pairs**: 查询序列和参考序列一一对应的比对位点(抛弃，用get_aligned_pairs()代替)
* **bin**: 
* **blocks**: 参考序列的起始和终止位点(抛弃，用get_blocks()代替)
* **cigar**: cigar属性，简要比对信息表达式(抛弃，用cigar代替)
* **cigarstring**: 简要比对信息表达式，比如：'3S6M1P1I4M'
* **cigartuples**: 简要比对信息表达式, 返回列表，如： (operation, length)

operation的类型：
| 简写 | 类型 | 数字 |
| ----- | ----:|:---- |
|M|BAM_CMATCH|0|
|I|BAM_CINS|1|
|D|BAM_CDEL|2|
|N|BAM_CREF_SKIP3|
|S|BAM_CSOFT_CLIP4|
|H|BAM_CHARD_CLIP5|
|P|BAM_CPAD	6|
|=|BAM_CEQUAL|7|
|X|BAM_CDIFF|8|
|B|BAM_CBACK|9|

* **compare(self, AlignedSegment other)**: return -1,0,1, if contents in this are binary <,=,> to other
* **flag**: flag属性
* **from_dict(type cls, sam_dict, AlignmentHeader header)**: 解析代表aligned segment的字典
* **fromstring(type cls, sam, AlignmentHeader header)**: 
* **get_aligned_pairs(self, matches_only=False, with_seq=False)**: 查询序列和参考序列一一对应的比对位点
* **get_blocks(self)**: a list of start and end positions of aligned gapless blocks
* **get_cigar_stats(self)**: 
* **get_forward_qualities(self)**: 原始reads的碱基质量(map到负链上的reads将是反的)
* **get_forward_sequence(self)**: 原始reads的碱基序列(map到负链上的reads将是反的)
* **get_overlap(self, uint32_t start, uint32_t end)**: 
* **get_reference_positions(self, full_length=False)**: reads比对到参考基因组的位置列表
* **get_reference_sequence(self)**: 参考序列
* **get_tag(self, tag, with_value_type=False)**: 
* **get_tags(self, with_value_type=False)**: 可选字段 [('XT', 'U'), ('NM', 1), ('X0', 1), ('MD', '24G11')]
* **has_tag(self, tag)**: 
* **infer_query_length(self, always=False)**: 从CIGAR字段推断查询序列长度
* **infer_read_length(self)**: 从CIGAR字段推断read长度
* **inferred_length**: 抛弃，用 infer_query_length()代替
* **is_duplicate**: 是否是 optical 或者PCR重复
* **is_paired**: 是否是paired序列
* **is_proper_pair**: 是否是适当、正确的pair？
* **is_qcfail**: 是否质控失败
* **is_read1**: 
* **is_read2**: 
* **is_reverse**: 是否map到负链
* **is_secondary**: 是否不是主要的比对(有更好的比对位置)
* **is_supplementary**: 是否是补充对齐
* **is_unmapped**: 是否没有比对上
* **isize**: 抛弃，使用template_length代替
* **mapping_quality**: mapping的质量
* **mapq**: 抛弃，用mapping_quality代替
* **mate_is_reverse**: 是否mate比对到了负链
* **mate_is_unmapped**: mate是否没有比对上
* **mpos**: 抛弃，用next_reference_start代替
* **mrnm**: 抛弃， 用next_reference_id代替
* **next_reference_id**:  mate/next read的reference id
* **next_reference_name**: 
* **next_reference_start**: 
* **opt(self, tag)**: 抛弃，用get_tag()代替
* **overlap(self)**: 抛弃，用get_overlap() 代替
* **pnext**: 抛弃，用next_reference_start 代替
* **pos**: 抛弃，用reference_start代替
* **positions**: 抛弃，用 get_reference_positions()代替
* **qend**: 抛弃，用query_alignment_end代替
* **qlen**: 抛弃，用query_alignment_length代替
* **qname**: 抛弃，用query_name代替
* **qqual**: 抛弃，用query_alignment_qualities代替
* **qstart**: 抛弃，用query_alignment_start代替
* **qual**: 抛弃，用query_qualities 代替
* **query**: 抛弃，用query_alignment_sequence 代替
* **query_alignment_end**: 



>class pysam.PileupColumn

>class pysam.PileupRead

>class pysam.IndexedReads(AlignmentFile samfile, int multiple_iterators=True)


**实例**

1.统计指定SNP位点各碱基的数目

```
import pysam

def get_snp_count(samf, chrom, snp):
    data = {"ref": "", "A": 0, "T": 0, "C": 0, "G": 0}
    reads = samf.fetch(chrom, snp-1, snp)
    firstline = True
    for read in reads:
        snp_pos, _, ref_base = [i for i in read.get_aligned_pairs(with_seq=True) if i[1] == snp-1][0]
        query_base = read.query[snp_pos].upper()
        data[query_base] += 1
        if firstline:
            data["ref"] = ref_base.upper()
            firstline = False
    return data
```

2.提取比对到某SNP位点的非uniq reads

```
import pysam

# 获得比对到指定位点的非uniq reads的ID
def get_reads_id(bamfile, chrom, pos):
    samf = pysam.AlignmentFile(bamfile)
    ids = []
    reads = samf.fetch(chrom, pos-1, pos)
    for read in reads:
        try:
            read.get_tag("XS")
        except:
            continue
        name = read.to_dict()["name"]
        if name not in ids:
            ids.append(name)
    samf.close()
    return ids

# 根据reads ID提取比对结果
def get_reads(bamfile, outsamfile, ids):
    samf = pysam.AlignmentFile(bamfile)
    outfile = pysam.AlignmentFile(outsamfile, mode="w", template=samf)
    for read in samf:
        if read.query_name in ids:
            outfile.write(read)
    samf.close()
    outfile.close()
```


### pyfaidx - 对fasta进行快速随机访问

Samtools provides a function “faidx” (FAsta InDeX), which creates a small flat index file “.fai” 
allowing for fast random access to any subsequence in the indexed FASTA file, while loading a minimal 
amount of the file in to memory. This python module implements pure Python classes for indexing, 
retrieval, and in-place modification of FASTA files using a samtools compatible index. The pyfaidx 
module is API compatible with the pygr seqdb module. A command-line script “faidx” is installed 
alongside the pyfaidx module, and facilitates complex manipulation of FASTA files without any 
programming knowledge.

[例子](https://pypi.org/project/pyfaidx/)



## BWA & Bowtie2

* [BWA中文手册](https://cncbi.github.io/BWA-Manual-CN/)
* [关于map当中的unique mapped reads问题](http://blog.sina.com.cn/s/blog_5d5f892a0102wbwc.html)
* [BWA，Bowtie，Bowtie2的比对算法推导](https://zhuanlan.zhihu.com/p/30485711)
* [Manual Reference Pages  - bwa (1)](http://bio-bwa.sourceforge.net/bwa.shtml)

之后先后出现了两个重要的比对软件， MAQ/BWA以及Bowtie。MAQ/BWA是Heng Li发表的。
Li是从华大基因走出来的人，后来去了Wellcome Trust Sanger Institute, 现在在哈佛Broad Institute。
MAQ的引用率非常高，并成为了Li的成名作。之后写作的BWA以准确率高而闻名，是SNP分析的首选比对软件。

而Bowtie借着其算法上的优势，在运算速度上一举成名。如果对速度的要求高于准确率的时候，
bowtie就成了不二选择。bowtie被广泛地应用于ChIP-seq, RNA-seq的分析当中。

就我个人经验而言（其实是对研究机构前人脚本学习和接受），对于ChIP-seq, RNA-seq，多使用bowtie2，
因为它快速，下游结合cufflinks等结果验证率很高。

对于SNP， Indels, methylation分析，使用BWA，下游结合GATK可能会好一点。



**[bowtie2比对后产生的Alignment summary解读](https://www.cnblogs.com/leezx/p/8540862.html)**

Hisat2和bowtie2比对后产生的Alignment summary的格式是一样的，如下：

单端数据比对的结果如下：

```
20000 reads; of these:
  20000 (100.00%) were unpaired; of these:
    1247 (6.24%) aligned 0 times
    18739 (93.69%) aligned exactly 1 time
    14 (0.07%) aligned >1 times
93.77% overall alignment rate
```

双端数据比对的结果如下：

```
10000 reads; of these:
  10000 (100.00%) were paired; of these:
    650 (6.50%) aligned concordantly 0 times
    8823 (88.23%) aligned concordantly exactly 1 time
    527 (5.27%) aligned concordantly >1 times
    ----
    650 pairs aligned concordantly 0 times; of these:
      34 (5.23%) aligned discordantly 1 time
    ----
    616 pairs aligned 0 times concordantly or discordantly; of these:
      1232 mates make up the pairs; of these:
        660 (53.57%) aligned 0 times
        571 (46.35%) aligned exactly 1 time
        1 (0.08%) aligned >1 times
96.70% overall alignment rate
```

解读双端模式：

第一部分：

`aligned concordantly`就是read1和read2同时合理的比对到了基因组/转录组上。 `exactly 1 time` 就是只有一种比对结果。
`>1 times` 就是read1和read2可以同时比对到多个地方。

第二部分：

`concordantly 0 times`就是read1和read2不能同时合理的同时比对到基因组/转录组上

`aligned discordantly`就是read1和read2都能比对上，但是不合理，1. 比对方向不对，pair-end测序的方向是固定的；
2.read1和read2的插入片段长度是有限的

第三部分：

对剩余reads（既不能concordantly，也不能discordantly 1 time）的单端模式的比对


**[bwa aln常见参数](https://blog.csdn.net/Doris_xixi/article/details/80842353?utm_source=blogxgwz9)**

* `-n`: 允许最大错配数(mismatch + gap)
* `-o`: 允许的gap数



## IGV

* [学IGV必看的初级教程](https://tiramisutes.github.io/2018/02/05/IGV.html)


## Kraken2

1. 安装：

```
# https://github.com/bioconda/bioconda-recipes/issues/15202
conda create -c bioconda -c conda-forge -n kraken2 kraken2=2.0.8_beta bracken=2.2
```

2. 下载比对数据库

```
wget https://www.ccb.jhu.edu/software/kraken2/dl/minikraken2_v2_8GB.tgz
# 或：
# wget -c -b ftp://ftp.ccb.jhu.edu/pub/data/kraken2_dbs/minikraken_8GB_202003.tgz
tar zxvf minikraken2_v2_8GB.tgz -C $HOME/dbs/minikraken2
```

3. 使用

[Pathogen NGS 数据分析入门](https://indexofire.github.io/pathongs/C12_Metagenomics-Analysis/01_kraken/)

使用kraken2需要用--db指向其数据库，比如微生物鉴定常用minikraken2数据库。
用--report参数生成结果报告。

```
$ conda activate kraken2
(kraken)$ kraken2 --use-names --threads 4 --db $HOME/dbs/minikraken2 --report report.txt assembly.fna > result.kraken
(kraken)$ kraken2 --use-names --threads 4 --db $HOME/dbs/minikraken2 --report report2.txt --fastq-input --paired S1_R1.fq.gz S1_R2.fq.gz > result2.kraken
(kraken)$ wget https://ccb.jhu.edu/software/bracken/dl/minikraken2_v2/database200mers.kmer_distrib
(kraken)$ mv database200mers.kmer_distrib $HOME/dbs/minikraken2
(kraken)$ bracken -d $HOME/dbs/minikraken2 -i kraken2.report -o bracken.species.txt -l S
```


## CNVkit

* [使用CNVkit进行CNV分析](http://www.360doc.com/content/19/1224/13/68068867_881784738.shtml)
* [CNV分析工具之一：CNVkit](https://www.dxy.cn/bbs/newweb/pc/post/38832790?from=recommend)

cnvkit.py调用samtools失败：
* [samtools的库的问题](https://www.jianshu.com/p/9ae2219e237b)
* [如何用conda安装软件|处理conda安装工具的动态库问题](https://www.jianshu.com/p/f8a0692df264)

cnvkit.py调用R包DNAcopy失败：

>错误: package or namespace load failed for ‘DNAcopy’:
 package ‘DNAcopy’ was installed before R 4.0.0: please re-install it

[重新安装DNAcopy包](https://bioconductor.org/packages/release/bioc/html/DNAcopy.html)：

```R
# To install this package, start R (version "4.0") and enter:

if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("DNAcopy")
```



## samtools

[samtools-manual](http://www.htslib.org/doc/samtools.html)

1. 将sam转成bam: `samtools view -b -S a.sam > a.bam`  或者 `cat a.sam | samtools view -b -S - > a.bam`
2. 

----

# 文件格式

## .fai (索引文件)

[利用`.fai`索引对基因组序列快速提取](http://born2run.cn/2018/06/05/samtools-index-fai/)

`samtools`中的`index`方法就能够直接提取出参考基因组特定位置的序列。

```
samtools faidx hg19.fa -r 'chr1:100000-200000'
```

这个速度是非常的快的，因为主要是基于了事先建立好的索引文件`hg19.fa.fai`。

**.fai格式到底是什么**

`faidx`其实已经解释的很清楚了，我们利用

```
samtools faidx genome.fasta
```

所生成的genome.fasta.fai格式其实就是5列信息：
1. contig:也就是我们在fasta格式中看到的以>xxx标记的信息，
一般情况下就是我们基因组中的染色体。例如>chr2
2. length:也就是contig的长度，假设我们的contig是某个物种的一号染色体，
长度为10000，那么就代表有10000个碱基。
3. offset:这个就是开始的位置，而这个开始的位置并不是是指染色体开始的坐标
（开始的坐标都是1），而是在genome.fasta这个文件中，序列是从文件的什么位置开始。
举个例子，假设genome.fasta中的文件如下：
```
chr1	17	19
```
chr1，17都很好理解，20表示的是第一个A在文件中开始的坐标，我们从第一个字符开始数>:0,
c:1,h:2,r:3,1:4,(空格):5,<:6,n:7,o:8,(空格):9,d:10,e:11,s:12,r:13,i:14,b:15,
e:16,>:17,\n(最后有一个看不见的换行符):18。所以A开始的位置是19。（希望我这么解释能够说明白）
4. 一行有多少个碱基：因为一般情况下，基因组的序列不可能写到一行中，会分行开始写，
但是每一行的碱基数是固定的（除了最后一行），假设每一行写60个碱基，那么第四列的数字就是60.
5. 一行所占字符数：一般情况下，这个数字是第四列+1，因为会多一个看不见的转行符占一个字符，
如果一行是60个碱基，那么这一列的数字就为61。

**知道index能做什么**

这个就需要一点点有关于读写的小知识，特别是各种编程语言中对于文件柄操作的seek。

seek就是将文件柄的坐标移到特定位置的方法，以python为例，
```
with open('genome.fasta','r') as f:
	f.seek(19,0)
	base=f.read(1)
	print(base)
```
上述语句就相当于，我将之前的genome.fasta文件打开，正常情况下，
我直接读取的话应该是读取第一行>chr1 <xxxx>这一行信息，但是我将坐标移动了，
移动到第19个位置（第二个0，表示按照绝对坐标移动，还可以按照相对坐标移动，
只需要将0换成1），然后读取一个字符，自然得出的就是第一个碱基A。

我想这么一说应该就挺好想，如何快速的从基因组中取得一段特定序列了。
只需要seek到需要提取序列的位置，在read序列的长度就可以了。

答案就是这么简单。唯一需要考虑的就是，怎么不被换行符所影响。

```
def get_seq(self, fbuffer, start, end, offset, line, size):
    '''

    :param fbuffer:打开的基因组文件柄
    :param start:查询的基因组起始位置（contig已经做过判断了）
    :param end:查询的基因组的终止位置
    :param offset:.fai文件中，contig所对应的碱基起始位置
    :param line:.fai文件中，第四列：每一行多少个碱基
    :param size:.fai文件中，第五列：每一行多少个字符
    :return:
    '''
    location = offset + int(start / line) + start - 1
    length = (int(end / line) - int(start / line)) * (size - line) + end - start + 1
    fbuffer.seek(location, 0)
    sequence = fbuffer.read(length).replace('\n','')
    return sequence
```
这样直接返回的就是序列了。为了确认查询的是否正确，
我一般会用同样的坐标在用samtools查一遍。确认没问题。


## bam/sam

[sam/bam及相关规范](http://samtools.github.io/hts-specs/)



**FLAG数值含义**

| 数值 | 二进制         | 解释                                                        |
| ---- | -------------- | ----------------------------------------------------------- |
| 1    | 0000 0000 0001 | 该read是成对的paired reads中的一个                          |
| 2    | 0000 0000 0010 | paired reads中每个都正确比对到参考序列上                    |
| 4    | 0000 0000 0100 | 该read没比对到参考序列上                                    |
| 8    | 0000 0000 1000 | 与该read成对的matepair read没有比对到参考序列上             |
| 16   | 0000 0001 0000 | 该read其反向互补序列能够比对到参考序列                      |
| 32   | 0000 0010 0000 | 与该read成对的matepair read其反向互补序列能够比对到参考序列 |
| 64   | 0000 0100 0000 | 在paired reads中，该read是与参考序列比对的第一条            |
| 128  | 0000 1000 0000 | 在paired reads中，该read是与参考序列比对的第二条            |
| 256  | 0001 0000 0000 | 该read是次优的比对结果 (luyl注: CIGAR字段中包含"H")         |
| 512  | 0010 0000 0000 | 该read没有通过质量控制                                      |
| 1024 | 0100 0000 0000 | 由于PCR或测序错误产生的重复reads                            |
| 2048 | 1000 0000 0000 | 补充匹配的read                                              |



**各标签含义**

***tophat/hisat2***

* `NH:i:<N>`: N=1时 为unique。常用于tophat/hisat2产生的sam文件unique read筛选。
* `CC:Z`: 当为‘=’为map到同一条基因上，一般在map基因组时由于内含子存在而容易出现，他只代表两种不同的方式，计数时应记为1。此处一般为其他基因的名字。CP:i 和HI：i标签为map到第i条基因及起始位置。
* `YT:Z:<S>`:代表的含义与bowtie产生的sam也不同。具体还未知！其他标签AS，XN,XM,XO,XG,NM,MD等如下图可以看出都相同。

***bowtie2***

* `AS:i:<N>` Alignment score.可以为负的，在local下可以为正的。 只有当Align≥1 time才出现
* `XS:i:<N>` Alignment score for second-best alignment. 当Align>1 time出现
* `YS:i:<N>` Alignment score for opposite mate in the paired-end alignment. 当该read是双末端测序中的另一条时出现
* `XN:i:<N>` Thenumber of ambiguous bases in the reference covering this alignment.（推测是指不知道错配发生在哪个位置，推测是针对于插入和缺失，待查证）
* `XM:i:<N>` 错配碱基的数目
* `XO:i:<N>` The number of gap opens(针对于比对中的插入和缺失)
* `XG:i:<N>` The number of gap extensions(针对于比对中的插入和缺失延伸数目)
* `NM:i:<N>` The edit distance。（edits:插入/缺失/替换数目)
* `YF:Z:<S>` 该reads被过滤掉的原因。可能为LN(错配数太多，待查证)、NS(read中包含N或者．)、SC(match bonus低于设定的阈值)、QC(failing quality control，待证)
* `YT:Z:<S>` 值为UU表示不是pair中一部分、CP是pair且可以完美匹配、DP是pair但不能很好的匹配、UP是pair但是无法比对到参考序列上。
* `MD:Z:<S>` 比对上的错配碱基的字符串表示。


**1. Edit Distance编辑距离（NM tag）**

[参考](https://www.cnblogs.com/leezx/p/5978014.html)

今天要介绍的是如何通过bam文件统计比对的indel和mismatch信息

首先要介绍一个非常重要的概念--编辑距离

定义：从字符串a变到字符串b，所需要的最少的操作步骤（插入，删除，更改）为两个字符串之间的编辑距离。

（2016年11月17日：增加，有点误导，如果一个插入有两个字符，那编辑距离变了几呢？1还是2？我又验证了一遍：确实是2）

这也是sam文档中对NM这个tag的定义。



编辑距离是对两个字符串相似度的度量（参见文章：Edit Distance）

举个栗子：两个字符串“eeba”和“abca”的编辑距离是多少？

根据定义，通过三个步骤：1.将e变为a 2.删除e 3.添加c，我们可以将“eeba”变为“abca”

```
e e b   a
a   b c a
```
所以，“eeba”和“abca”之间的编辑距离为3



回到序列比对的问题上

下面是常见的二代比对到ref的结果（bwa）：

```
D00360:96:H2YLYBCXX:1:2110:18364:84053    353    seq1_len154_cov5    1    1    92S59M8I17M1D6M1D67M    seq30532_len2134_cov76    1    0    AAAAAAAAAAAAAAAAAAAAAAAACCCTGTCTCTAATAAAATACAAACAATTAGCCGGGCATGGTGGCACGCGCCTTTAGTCCCAGCTACTAGGGAGGCTGAGGCAGGGGAATTGTTTGAACCCGGGAGGTGGAGGTTGCAGTGAGCGGAGTTTTTTTCACTGCACTCCAGCCTGGTGACAAATCAAAAATCCATTTCAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAAACAACAAA  DDDDDHIIIIIIII<EHHII?EHH0001111111<11<DEH1D1<FH1D<<<C<@GEHD</<11<101<1D<<C<E0D11<<1<D?1F1CC1DE110C0D1011100////0DD<1=@1=FGHCDHH<FG<D0<<<EF?CE<00<<0<D//0;<:D/////;///////;8F.;/.8.8......88.9........-8BBGADHIIHD?>D?HH<,>=HHDD,5CHDCDHD><,,,--8----8-8--    NM:i:25    MD:Z:16A21C16C0A3T15^A6^G1G0T0G3C2T0G1C41A4A2A3    AS:i:49    XS:i:42    SA:Z:seq13646_len513_cov63,125,-,103S125M21S,1,11;    RG:Z:chr22
```

cigar字段包含了序列比对的简化信息，** M（匹配比对，包含match和mismatch），=（纯match），
X（纯mismatch），I（插入），D（删除），还有N、P和S、H。（注：目前只在blasr比对结果中见过=和X）**

根据cigar字段可以统计indel信息，但是无法统计mismatch。

这个时候就可以用到`NM tag`了，mismatch = NM – I - D = 25 – 8 – 1 – 1 = 15


**2. CIGAR字段中H和S区别**

[Difference between Hard Clip（H） and Soft Clip（S） in Samtools CIGAR string](https://www.cnblogs.com/leezx/p/6105646.html)






----

# 期刊杂志

* Science, Nature, PANS, CELL (顶级综合类期刊)
* genetics in medicine (医学遗传学, IF=10)
* AMERICAN JOURNAL OF HUMAN GENETICS (美国人类遗传学杂志, IF=10)
* nature genetics (自然遗传学, IF=27)
* science translational medicine (科学转化医学, IF=16)
* clinical cancer research (临床癌症研究, IF=10)
* journal of clinical oncology (临床肿瘤学杂志, IF=26)
* genome research (基因组研究, IF=10)
* clinical chemistry (临床化学, IF=8)


----

# 下载

* affyCytoScan探针:   http://hgdownload.soe.ucsc.edu/goldenPath/hg19/database/affyCytoScan.txt.gz
* 染色体条带坐标文件：http://hgdownload.cse.ucsc.edu/goldenpath/hg19/database/cytoBand.txt.gz
* 转录本注释文件：    http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/refGene.txt.gz
* 经典转录本：        http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/knownCanonical.txt.gz
<<<<<<< HEAD
                     http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/kgXref.txt.gz(对应ID)
* mappability-Kmer: http://hgdownload.cse.ucsc.edu/goldenPath/hg19/encodeDCC/wgEncodeMapability
* RepeatMasker: http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/rmsk.txt.gz

=======
                      http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/kgXref.txt.gz(对应ID)
* repeats-RepeatMasker:  http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/rmsk.txt.gz  [【深入UCSC Genome Browser】repeats-RepeatMasker](https://blog.csdn.net/tanzuozhev/article/details/80958785)


----

## BioStars

* [How To Get Bed File Containing Exons Of Canonical Transcripts And Their Corresponding Gene Symbols](https://www.biostars.org/p/93011/)
* [Why the list of genes in UCSC "knownGene" table is strikingly different than the list of genes in UCSC "known canonical" table?](https://www.biostars.org/p/367011/)
* [How to tell which transcript is the canonical transcript?](https://www.biostars.org/p/209633/)


## StackExchange-Bioinformatics
* [How to obtain .bed file with coordinates of all genes](https://bioinformatics.stackexchange.com/questions/895/how-to-obtain-bed-file-with-coordinates-of-all-genes)


----

# 其他

[2020年生物信息学领域前75名的博客和网站](https://blog.feedspot.com/bioinformatics_blogs/)
* [How to obtain .bed file with coordinates of all genes](https://bioinformatics.stackexchange.com/questions/895/how-to-obtain-bed-file-with-coordinates-of-all-genes)

----

# 比较酷的事情

## 不同k值下基因组间的k-mer相似度近似于物种分类间的相似度

 the authors show that k-mer similarity between genomes at different k approximates 
 various degrees of taxonomic similarity. Roughly, high similarity at k=21 defines 
 genus-level similarity, k=31 defines species-level, and k=51 defines strain-level. 
 (This is an ad-lib from what is much more precisely and carefully stated within the paper.) 
 This relationship is something that we already sorta knew from Kraken and similar k-mer-based 
 taxonomic efforts, but the MetaPalette paper was the first paper I remember reading 
 where the specifics really stuck to me.

 [A post about k-mers - this time for taxonomy!](http://ivory.idyll.org/blog/2017-something-about-kmers.html)


## DUP/DEL的发生机制

* [基因组拷贝数变异及其突变机理与人类疾病](http://m-learning.zju.edu.cn/G2S/eWebEditor/uploadfile/20140917085256342.pdf)

人类基因组上大量的 CNV 是如何产生的？其中一类已知的机制是 DNA 重组, 包括**非等位同源重
组(Nonallelic homologous recombination, NAHR)**和**非同源末端连接(Nonhomologous end-joining, 
NHEJ)**等。最近, 一种新的基于 DNA 错误复制的机制被发现, 即“复制叉停滞与模板交换”(Fork 
stalling and template switching, FoSTeS)模型。此种机制可以解释那些不符合 NAHR、NHEJ 
等突变机制的具有复杂结构的 CNV.

前人类基因组序列其实只包括了绝大部分常染色质区域, 而且有很多空隙(Gap)。常染色质区域的空隙
中大约有 54%在其附近有片段重复序列(Segmental duplication, SD; 长度大于 1 kb), 它们更倾向于
产生 CNV。而反过来, CNV 也可能是造成难以填补序列空隙的因素之一。即使是在有参考序列的基因组
区域, 我们将来也可能发现更多的新 CNV。基因组结构比较复杂的区域含有较多的 SD 序列, 这为 CNV 
的产生提供了结构基础。

NAHR 是由两条同源的、但在基因组不同位置重复出现的、高度相似性的 DNA 序列配对并发生序列交换
造成的。相同染色体上的同向重复序列间的 NAHR 会导致重复或缺失, 反向重复序列间的NAHR 会导致
倒位。不同染色体上的重复序列间的 NAHR 可能会造成染色体易位.

其中涉及到的专业数据：

* [非等位同源重组](https://en.wikipedia.org/wiki/Non-allelic_homologous_recombination)
* [非同源末端连接](https://en.wikipedia.org/wiki/Non-homologous_end_joining)
* [片段重复序列](https://en.wikipedia.org/wiki/Low_copy_repeats)