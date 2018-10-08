# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [概念](#概念)
      * [基因组变异检测](#基因组变异检测)
         * [基本概念](#基本概念)
         * [检测流程](#检测流程)
            * [变异检测](#变异检测)
            * [变异注释](#变异注释)
   * [技术原理](#技术原理)
      * [PGS/PGD](#pgspgd)
         * [FISH](#fish)
         * [Array-CGH](#array-cgh)
   * [数据库](#数据库)
      * [CNV](#cnv)
         * [CNV Syndromes](#cnv-syndromes)
   * [软件](#软件)
      * [生物信息软件参数解析](#生物信息软件参数解析)
         * [samtools](#samtools)
         * [bcftools](#bcftools)
      * [python模块](#python模块)
         * [pysam](#pysam)
            * [基础操作](#基础操作)
            * [API](#api)
               * [SAM/BAM/CRAM files](#sambamcram-files)
   * [文件格式](#文件格式)
      * [.fai (索引文件)](#fai-索引文件)

<!-- Added by: luyl, at: 2018-10-08T11:43+08:00 -->

<!--te-->

----
# 概念

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


----

# 数据库

## CNV

### CNV Syndromes

* [DECIPHER](https://decipher.sanger.ac.uk/disorders#syndromes/overview)


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


在开发基因组相关流程或工具时，经常需要读取、处理和创建bam、vcf、bcf文件。
目前已经有一些主流的处理此类格式文件的工具，如samtools、picard、vcftools、bcftools，
但此类工具集成的大多是标准功能，在编程时如果直接调用的话往往显得不够灵活。

本文介绍的是一个处理基因组数据的python模块，它打包了htslib-1.3、samtools-1.3 和 
bcftools-1.3的核心功能，能在编程时非常灵活的处理bam和bcf文件。


#### 基础操作

**1.安装**

如果Linux上安装了pip，可以一键安装
```
pip3 install pysam
```


**2.读取bam文件(pysam.AlignmentFile)**

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


**3.读取vcf/bcf文件(pysam.VariantFile)**

读取方法同上,只是使用的是VariantFile方法:

```
gvcf = "./MHC.unified.g.vcf.gz"
vcf_in = pysam.VariantFile(gvcf)
```


**4.创建并写入到新的bam或vcf文件**

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


**5.关闭文件**

```
outf.close()
```

**总结:**

pysam模块非常实用,有了pysam模块,我们就可以非常灵活的操纵bam/bcf文件,
而不必依赖于samtools或bcftools. pysam可以随机读取bam/bcf文件,
也可以将处理后的内容自定义输出到bam/bcf文件.


#### API

##### SAM/BAM/CRAM files

>pysam.AlignmentFile

>pysam.AlignedSegment(AlignmentHeader header=None)

**aend**: 参考序列结束位置(抛弃，用reference_end代替)
**alen**: 参考序列长度(抛弃，用reference_length代替)
**aligned_pairs**: 查询序列和参考序列一一对应的比对位点(抛弃，用get_aligned_pairs()代替)
**bin**: 
**blocks**: 参考序列的起始和终止位点(抛弃，用get_blocks()代替)
**cigar**: cigar属性，简要比对信息表达式(抛弃，用cigar代替)
**cigarstring**: 简要比对信息表达式，比如：'3S6M1P1I4M'
**cigartuples**: 简要比对信息表达式, 返回列表，如： (operation, length)
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
**compare(self, AlignedSegment other)**: return -1,0,1, if contents in this are binary <,=,> to other
**flag**: flag属性
**from_dict(type cls, sam_dict, AlignmentHeader header)**: 解析代表aligned segment的字典
**fromstring(type cls, sam, AlignmentHeader header)**: 
**get_aligned_pairs(self, matches_only=False, with_seq=False)**: 查询序列和参考序列一一对应的比对位点
**get_blocks(self)**: a list of start and end positions of aligned gapless blocks
**get_cigar_stats(self)**: 
**get_forward_qualities(self)**: 原始reads的碱基质量(map到负链上的reads将是反的)
**get_forward_sequence(self)**: 原始reads的碱基序列(map到负链上的reads将是反的)
**get_overlap(self, uint32_t start, uint32_t end)**: 
**get_reference_positions(self, full_length=False)**: reads比对到参考基因组的位置列表
**get_reference_sequence(self)**: 参考序列
**get_tag(self, tag, with_value_type=False)**: 
**get_tags(self, with_value_type=False)**: 可选字段 [('XT', 'U'), ('NM', 1), ('X0', 1), ('MD', '24G11')]
**has_tag(self, tag)**: 
**infer_query_length(self, always=False)**: 从CIGAR字段推断查询序列长度
**infer_read_length(self)**: 从CIGAR字段推断read长度
**inferred_length**: 抛弃，用 infer_query_length()代替
**is_duplicate**: 是否是 optical 或者PCR重复
**is_paired**: 是否是paired序列
**is_proper_pair**: 是否是适当、正确的pair？
**is_qcfail**: 是否质控失败
**is_read1**: 
**is_read2**: 
**is_reverse**: 是否map到负链
**is_secondary**: 是否不是主要的比对(有更好的比对位置)
**is_supplementary**: 是否是补充对齐
**is_unmapped**: 是否没有比对上
**isize**: 抛弃，使用template_length代替
**mapping_quality**: mapping的质量
**mapq**: 抛弃，用mapping_quality代替
**mate_is_reverse**: 是否mate比对到了负链
**mate_is_unmapped**: mate是否没有比对上
**mpos**: 抛弃，用next_reference_start代替
**mrnm**: 抛弃， 用next_reference_id代替
**next_reference_id**:  mate/next read的reference id
**next_reference_name**: 
**next_reference_start**: 
**opt(self, tag)**: 抛弃，用get_tag()代替
**overlap(self)**: 抛弃，用get_overlap() 代替
**pnext**: 抛弃，用next_reference_start 代替
**pos**: 抛弃，用reference_start代替
**positions**: 抛弃，用 get_reference_positions()代替
**qend**: 抛弃，用query_alignment_end代替
**qlen**: 抛弃，用query_alignment_length代替
**qname**: 抛弃，用query_name代替
**qqual**: 抛弃，用query_alignment_qualities代替
**qstart**: 抛弃，用query_alignment_start代替
**qual**: 抛弃，用query_qualities 代替
**query**: 抛弃，用query_alignment_sequence 代替
**query_alignment_end**: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****: 
****:


>class pysam.PileupColumn

>class pysam.PileupRead

>class pysam.IndexedReads(AlignmentFile samfile, int multiple_iterators=True)




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