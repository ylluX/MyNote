# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
* [目录](#目录)
* [随笔](#随笔)
   * [常用命令](#常用命令)
   * [数组](#数组)
   * [创建空data.frame](#创建空dataframe)
   * [paste和cat区别](#paste和cat区别)
   * [插入1行或1列](#插入1行或1列)
   * [生成随机数](#生成随机数)
   * [R之向量的创建和数据框的转换](#r之向量的创建和数据框的转换)
   * [多维数组](#多维数组)
* [包](#包)
   * [stringr](#stringr)
   * [DNAcopy](#dnacopy)
<!--te-->

----

# 随笔

## 常用命令

* 查看R版本：`version`

* 安装包: `install.packages(package)`

* 获得(设置)当前工作目录：`getwd()`, `setwd()`

  

## 数组

* 生成连续序列：`seq(from=1,to=5,by=2)`, 增量为1可写成：c(1:5)
* 生成重复序列：`rep(1, times=5)`


## 创建空data.frame

```R
mydata <- data.frame(age=numeric(0), gender=character(0), weight=numeric(0), stringsAsFactors=FALSE))
mydata[1,] <- c(20,'a',70)
mydata
  age gender weight
1  20      a     70
```

## paste和cat区别

```R
a<-c(1,2,3,4)
b<-c(4,5,6,7)
c<-c('hi','hello')
paste(a,b,c)
cat(a,b,c)
#输出结果：
> paste(a,b,c)
[1] "1 4 hi"    "2 5 hello" "3 6 hi"    "4 7 hello"
> cat(a,b,c)
1 2 3 4 4 5 6 7 hi hello
```

## 插入1行或1列

如何向R中的`dataframe`的某一位置添加一行（`rbind`函数）或一列向量（`cbind`函数）

插入一列

```R
y<-1:4
data1 <- data.frame(x1=c(1,3,5,7), x2=c(2,4,6,8),x3=c(11,12,13,14),x4=c(15,16,17,18))
data2 <- cbind(data1[,1:2],y,data1[,3:ncol(data1)])
```

插入一行

```R
data1<- data.frame(x1=runif(10),x2= runif(10),x3= runif(10))
row<- c(1, 1, 1)
data2 <- rbind(data1[1:5,], row, data1[6:nrow(data1), ])
```




## 生成随机数

[用R生成随机数](https://blog.csdn.net/wangd6/article/details/59119307)

## R之向量的创建和数据框的转换

```R
a <- rnomal(12, mean=40, sd=20)
is.verctor(a) # TRUE
is.array(a)   # FALSE
is.numeric(a) # TRUE
# 改变维度
dim(a) <- c(3,4)
is.verctor(a) # FALSE
is.array(a)   # TRUE
is.numeric(a) # FALSE
# 将array转换成data.frame
a <- as.data.frame(a)
is.data.frame(a) # TRUE
```



## 多维数组



**生成多维数组**

1. 一组值只有定义了维数向量（dim属性）后才能被看作是数组。

```R
a <- 1:24
dim(a) <- c(3,4,2)
```

2. 用array()函数构造多维数组

```R
a <- array(0, dim=c(3,4,2))
```

**将两个二维数组合并成三维数组**

1. 使用abind包

```
library(abind)
abind(x,y,along=3)
```

2. 使用原生函数

```R
a1 <- array(1:12,dim=(3,4))
a2 <- array(13:24, dim=(3,4))
a <- array(c(a1,a2),dim=c(3,4,2))
```

**保存数组**

```R
# 保存
save(a1,a2,a, file="test.RData")
# 读取
load("test.RData")
```





## 安全导入数据

[Safe Loading of RData Files](https://www.r-bloggers.com/2016/04/safe-loading-of-rdata-files-2/)

如果直接用`load()`函数导入`RData`数据，可能会存在覆盖原有同名函数的风险，为了避免该问题，可以通过以下方式解决：

```R
# 将变量导入的新的环境中
load_to_env <- fcuntion(RData, env = new.env()){
    load(RData, env)
    return(env) 
}

# 测试
a <- array(1:20, dim=c(5,4))
b <- c(1:5)
save(a,b, "test.1.RData")
a <- a * 2
b <- b + 5
save(a,b, "test.2.RData")
data1 <- load_to_env("test.1.RData")
data2 <- load_to_env("test.2.RData")
print(data1$a)
```






----

# 包

## stringr

```R
ks = c("46,XY[30%]","46,XX[70%]")
str_extract(ks,'\\d+%')
[1] "30%" "70%"
str_split(ks, "\\[", simplify=T)
     [,1]    [,2]  
[1,] "46,XY" "30%]"
[2,] "46,XX" "70%]"
```


## DNAcopy

安装

[4.0以上版本R安装方法：](http://www.bioconductor.org/packages/release/bioc/html/DNAcopy.html)

```r
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("DNAcopy")
```

[4.0以下版本R安装方法：](https://bioconductor.riken.jp/packages/3.1/bioc/html/DNAcopy.html)

```r
## try http if https is not available
source("https://bioconductor.org/biocLite.R")
biocLite("DNAcopy")
```