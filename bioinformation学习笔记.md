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
   * [软件](#软件)
      * [生物信息软件参数解析](#生物信息软件参数解析)
         * [samtools](#samtools)
         * [bcftools](#bcftools)
   * [文件格式](#文件格式)
      * [.fai (索引文件)](#fai-索引文件)

<!-- Added by: luyl, at: 2018-09-10T13:18+08:00 -->

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
chr1，17都很好理解，20表示的是第一个A在文件中开始的坐标，我们从第一个字符开始数
>:0,c:1,h:2,r:3,1:4,(空格):5,<:6,n:7,o:8,(空格):9,d:10,e:11,s:12,r:13,i:14,b:15,
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