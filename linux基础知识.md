# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [基础命令](#基础命令)
      * [查看图片信息identify](#查看图片信息identify)
      * [转换图片格式convert](#转换图片格式convert)
   * [VIM](#vim)
      * [基础操作](#基础操作)

<!-- Added by: luyl, at: 2018-12-25T17:37+08:00 -->

<!--te-->

----

# 基础命令

## 查看图片信息`identify`
## 转换图片格式`convert`

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
