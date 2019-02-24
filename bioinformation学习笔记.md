# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [常见问题](#常见问题)
      * [GC偏好](#gc偏好)
   * [概念](#概念)
      * [易位](#易位)
      * [显(隐)性遗传病](#显隐性遗传病)
      * [染色体带型](#染色体带型)
      * [UPD](#upd)
      * [LOH](#loh)
      * [XO核型](#xo核型)
      * [染色体](#染色体)
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
      * [肿瘤数据库](#肿瘤数据库)
      * [遗传疾病公共数据库](#遗传疾病公共数据库)
      * [其它](#其它)
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

<!-- Added by: luyl, at: 2019-01-31T11:05+08:00 -->

<!--te-->

----

# 常见问题

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


----


# 概念

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

uniparental disomy, UPD: 单亲二体

## LOH

loss of heterozygosity, LOH: 杂合性缺失

杂合性缺失，位于一对同源染色体上的相同基因座位的两个等位基因中的一个（或其中部分核苷酸片段）发生缺失，与之配对的染色体上仍然存在。


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

**ExAC的pLI**

我们还得聊一聊另一个预测值pLI，它指的是基因对于LOF突变的不可忍受的可能性。
The Exome Aggregation Consortium (ExAC) 通过分析60,706 不同族群的个体外显子数据，
计算了pLI分值，来表示基因 不耐受Loss of Function (LoF) 突变。ExAC通过模型比较每个基因内观察到
的罕见突变和期望的罕见突变数据，通过Z score量化这种偏离。编码区的长度来减少混杂因素，对于蛋白
截断突变（Protein Truncating Variants (PTV) ），通过比较PTV在观察和期望中的数据，将基因分成3类。

* `Null`, 观察约等于期望，对LoF突变耐受 where observed ≈ expected (LoF variation is tolerated)
* `Recessive`, 观察得到的小于期望的50%，杂合LoF耐受 where observed ≤ 50% of expected (heterozygous LoFs are tolerated)
* `Haploinsufficient`, 观察得到的小于期望的10%，杂合LoF不耐受where observed < 10% of expected (heterozygous LoFs are not tolerated) 

pLI分值是一个给定基因归类到Haploinsufficient 类别中的概率，也就是对LoF不耐受的分值。分值越高，
越不耐受（intolerant），分值越低，越耐受（tolerant）。当然，具体运用中，不能仅根据pLI值就判定
一个LOF突变的致病性，我们还要同时考虑如疾病发病年龄，外显率，Haploinsufficiency score等。


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


## 遗传疾病公共数据库

**DECIPHER**

[DECIPHER](https://decipher.sanger.ac.uk/disorders#syndromes/overview) 为“Database of Chromosomal Imbalance and Phenotype 
in Humans using Ensembl Resources”的简称，也是目前分子遗传学中最重要的生物信息学数据库之一。用户可以通过检索数据库，
发现一系列相关的遗传疾病信息，包括变异位点、临床表型等，提高临床诊断效能。DECIPHER数据库包含了超过200家研究中心上传的超过
10,000例的案例信息。

**OMIM**

* [OMIM简明使用说明](http://www.biotrainee.com/thread-1107-1-1.html)

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