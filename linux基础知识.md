# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [基础命令](#基础命令)
      * [查看图片信息identify](#查看图片信息identify)
      * [转换图片格式convert](#转换图片格式convert)
      * [软连接的删除](#软连接的删除)
   * [VIM](#vim)
      * [基础操作](#基础操作)

<!-- Added by: luyl, at: 2019-01-29T10:21+08:00 -->

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


----

# 基础命令

## 查看图片信息`identify`

## 转换图片格式`convert`

## 软连接的删除

**软连接文件夹的删除**

如果dir不是普通文件夹，`rm -r dir` 和 `rm -r dir/` 都不会删除
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
* 替换`^@`：`:%s/\%x00/ /g`


----

# zsh

* [小试shell中的神器zsh](http://www.zxzyl.com/archives/1001)
* [http://www.zxzyl.com/archives/1001](https://www.zhihu.com/question/21418449)

