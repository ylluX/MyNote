# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
* [目录](#目录)
* [常见问题](#常见问题)
   * [.bashrc和.bash_profile的关系和区别](#bashrc和bash_profile的关系和区别)
   * [设置PS1](#设置ps1)
   * [特殊的内置参数($#/$?/$n/$@/$$/$!)](#特殊的内置参数n)
   * [生成连续的数](#生成连续的数)
   * [vim,less中文乱码](#vimless中文乱码)
   * [Shell脚本并发及并发数的控制](#shell脚本并发及并发数的控制)
   * [比较两个文件是否相同](#比较两个文件是否相同)
   * [${a##.*}, ${a%%.*}用法](#a-a用法)
* [基础命令](#基础命令)
   * [查看图片信息`identify`](#查看图片信息identify)
   * [转换图片格式`convert`](#转换图片格式convert)
   * [软连接的删除](#软连接的删除)
* [VIM](#vim)
   * [基础操作](#基础操作)
* [awk](#awk)
* [zsh](#zsh)
* [QSUB](#qsub)
<!--te-->

----

# 常见问题

## .bashrc和.bash_profile的关系和区别

.bash_profile是最重要的一个配置文件，它在用户每次登录系统时被读取，里面的所有命令都会被bash执行。
所以如果你有对/etc/profile有修改的话必须得重启你的修改才会生效，此修改对每个用户都生效。

.bashrc文件会在bash shell调用另一个bash shell时读取，也就是在shell中再键入bash命令启动一个新shell时就
会去读该文件。所以如果你有对/etc/profile有修改的话必须得重启你的修改才会生效，此修改对每个用户都生效。
这样可有效分离登录和子shell所需的环境。但一般 来说都会在.bash_profile里调用.bashrc脚本以便统一配置用
户环境。


.bash_logout在退出shell时被读取。所以我们可把一些清理工作的命令放到这文件中



## 设置PS1

"""
export PS1="\[\e[32;1m\][\[\e[34m\]\u\[\e[32m\]@\[\e[31m\]\h \[\e[33m\]\`pwd\`\[\e[32m\]](\[\e[35m\]\t\[\e[32m\])\n$\[\e[0m\]"
"""


## 特殊的内置参数($#/$?/$n/$@/$$/$!)

* `$#` 是传给脚本的参数个数
* `$0` 是脚本本身的名字
* `$1` 是传递给该shell脚本的第一个参数
* `$2` 是传递给该shell脚本的第二个参数
* `$@` 是传给脚本的所有参数的列表
* `$*` 是以一个单字符串显示所有向脚本传递的参数，与位置变量不同，参数可超过9个
* `$$` 是脚本运行的当前进程PID号
* `$!` 是上一个命令的进程PID号
* `$?` 是显示最后命令的退出状态，0表示没有错误，其他表示有错误


## 生成连续的数

1. for i in `seq 1 7`; do echo $i; done
2. for i in $(seq 1 7); do echo $i; done
3. for i in {seq 1..7}; do echo $i; done
4. for i in {1..7}; do echo $i; done
5. for ((i=0;i<=7;++i));do echo $i; done
6. i=0;while ((i<=7));do echo $i; done
7. i=0;until((i>7));do echo $i; done


## vim,less中文乱码

在.bashrc中添加：`export LC_ALL="zh_CN.UTF-8"`


## Shell脚本并发及并发数的控制

[Shell脚本并发及并发数的控制](https://www.jianshu.com/p/701952ffb755)

shell 并发时，可以在每条命令后边添加 `&` 符号；如果需要等待上边并发命令执行完后，
再执行后续命令，可以使用 `wait` 命令。

但是如果并发命令很多时，可能会占用过多系统资源，此时，可以使用管道和令牌原理实现并发控制。

```
#!/bin/bash

# Step1 创建有名管道
[ -e ./fd1 ] || mkfifo ./fd1

# 创建文件描述符，以可读（<）可写（>）的方式关联管道文件，这时候文件描述符3就有了有名管道文件的所有特性
exec 3<> ./fd1   

# 关联后的文件描述符拥有管道文件的所有特性,所以这时候管道文件可以删除，我们留下文件描述符来用就可以了
rm -rf ./fd1                    

# Step2 创建令牌 
for i in `seq 1 2`;
do
    # echo 每次输出一个换行符,也就是一个令牌
    echo >&3                   
done

# Step3 拿出令牌，进行并发操作
for line in `seq 1 10`;
do
    read -u3      # read 命令每次读取一行，也就是拿到一个令牌   
    {
        echo $line
        sleep 1
        echo >&3  # 执行完一条命令会将令牌放回管道
    }&
done

wait

exec 3<&-                       # 关闭文件描述符的读
exec 3>&-                       # 关闭文件描述符的写
```


## 比较两个文件是否相同

* 使用diff : `diff -q file1 file2 > /dev/null && echo "same" || echo "diff"`
* 使用cmp : `cmp --silent file1 file2 && echo "same" || echo "diff"`

或者和`$?`一起使用

```
diff file1 file2 > /dev/null
if [ $? != 0 ]; then
  echo "diff"
else
  echo "same"
fi
```


## ${a##.*}, ${a%%.*}用法

* `${varible##*string}` 从左向右截取最后一个string后的字符串
* `${varible#*string}` 从左向右截取第一个string后的字符串
* `${varible%%string*}` 从右向左截取最后一个string后的字符串
* `${varible%string*}` 从右向左截取第一个string后的字符串

```ssh
a="abcXXdefXXghiXXlmnXXopq"
echo "${a##*XX}"   # opq
echo "${a#*XX}"    # defXXghiXXlmnXXopq
echo "${a%%XX*}"   # abc
echo "${a%XX*}"    # abcXXdefXXghiXXlmn
```


----

# 基础命令

## 查看图片信息`identify`

## 转换图片格式`convert`

## 软连接的删除

**软连接文件夹的删除**

如果dir是软连接文件夹，`rm -r dir` 和 `rm -r dir/` 都不会删除
该文件夹下的所有软连接的源文件或文件夹

如果dir不是软连接文件夹，`rm -r dir` 不会删除该文件夹的源文
件夹; 但是**`rm -r dir/` 则会删除该文件夹的源文件夹下的所有
内容【请特别注意】**


----

# VIM

## 基础操作

* [vim中使用正则表达式](https://blog.csdn.net/whaoXYSH/article/details/24652361)
* [Vim 中读写特殊字符](https://blog.csdn.net/chenster/article/details/53307707)


* 删除空行：`:g/^$/d`
* 输入`^M`：`Ctrl+V Ctrl+M`
* 删除`^M`：`:%s/\r//g` 或 `:%s/^M//g`
* 搜索`^@`：`/<Ctrl-V>000`
* 替换`^@`：`:%s/\%x00/ /g`    # sed替换：`sed -i 's/\x0//g' filename`
* 删除`^@`：`Ctrl+V Ctrl+2`


----
# awk

[Linux三剑客之awk命令](https://www.cnblogs.com/ginvip/p/6352157.html)

1. 对test.txt文件中的第三行求和
```sh
awk 'BEGIN{SUM=0}{SUM+=$3}END{print SUM}'
```



----

# zsh

* [小试shell中的神器zsh](http://www.zxzyl.com/archives/1001)
* [http://www.zxzyl.com/archives/1001](https://www.zhihu.com/question/21418449)


----

# QSUB

常用投递命令：

> qsub -cwd -l vf=1G -l p=10 -l h=node1 –q all.q –P project test.sh

    * -l vf=1G ：任务的预估内存，内存估计的值应稍微大于真实的内存，内存预估偏小可能会导致节点跑挂。
    * -l p=10 ：指定核心数
    * -l h=node1 ： 指定计算节点
    * -P ：指明任务所属的项目

* 暂停任务：`qmod –sj jobid`
* 开始暂停任务：`qmod –usj jobid`
* 重新运行正在运行的任务：`qmod -f –rj jobid`

* 查看节点任务状态：`qhost –j –q –h compute-0-1`
* 查看任务状态：`qstat –j jobid`
* 查看任务的内存，cpu使用情况：`qstat –j jobid |grep usage`
* 删除任务：`qdel –f jobid / qdel –f –u user`
* 查询队列权限：`qselect –U user`
* 查询队列节点：`qstat -f | grep -v "\-\-"`
* 查看所有用户的任务: `qstat -u *,`
* 查看所有节点正在运行的任务: `qhost -j`
* 查看某队列中正在运行的任务: `qhost –j | grep "xxx.q"`
* 查看提交过的历史任务：`qacct -o luyl -b YYYYMMDDHHmm -j`