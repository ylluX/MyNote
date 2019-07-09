
# 目录
<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
[TOC]
<!--ts-->
* [目录](#)
* [python之禅](#python)
* [python核心概念](#python)
   * [GIL和互斥锁](#gil)
   * [进程、线程、协程](#)
* [1. python基础](#1-python)
   * [基础](#)
      * [1. 字典格式化输出](#1-)
      * [2. `str.split('\\n')`与`str.splitlines`区别](#2-strsplitnstrsplitlines)
      * [3. `exec`, `eval`和`repr`区别](#3-exec-evalrepr)
      * [4. 查看内建函数](#4-)
      * [5. 查看模块的所有属性和方法](#5-)
      * [6. `input`的新特性](#6-input)
      * [7. python的标准流与shell的管道联用](#7-pythonshell)
      * [8. 列表推导式中使用多个for](#8-for)
      * [9. 智能排序](#9-)
      * [10. 排列组合](#10-)
      * [11.\_\_import\_\_ 与动态加载 python module](#11__import__--python-module)
      * [12. print带汉字的字典或列表](#12-print)
      * [13. 通过配置文件共享全局变量](#13-)
      * [14. @staticmethod 和 @classmethod的区别](#14-staticmethod--classmethod)
      * [15. pip使用国内镜像](#15-pip)
      * [16. python内存变量保存到磁盘, 方便下次读入](#16-python-)
      * [17. 查看内存汇总的所有变量](#17-)
      * [18. python的搜索路径](#18-python)
      * [18.1 python的环境变量](#181-python)
      * [19. 数据的归一化/标准化/正则化](#19-)
      * [20. for...else...语法](#20-forelse)
      * [21. 将png合成gif](#21-pnggif)
      * [22. 捕获警告](#22-)
      * [23. 将PDF转成PNG](#23-pdfpng)
      * [24. os.walk()和os.path.walk()区别](#24-oswalkospathwalk)
      * [25. 以非root身份安装module](#25-rootmodule)
      * [26. 执行shell命令](#26-shell)
      * [27. Python 对数字的千分位处理](#27-python-)
      * [28. 按位运算](#28-)
      * [29. 进制](#29-)
      * [30. 模拟SSH登录和SCP传输](#30-sshscp)
      * [31. 获得本机IP](#31-ip)
      * [32. 获得两个概率密度函数交集区域内的概率](#32-)
      * [33. 将pandas数据和matplotlib绘图嵌入html文件](#33-pandasmatplotlibhtml)
      * [34. python读写excel文件](#34-pythonexcel)
      * [35. 编译好的包](#35-)
   * [高级](#)
      * [1. 装饰器（Decorator）](#1-decorator)
      * [2. 回调函数](#2-)
      * [3. 魔法方法](#3-)
      * [4. 工厂函数](#4-)
      * [5. 多进程（multiprocessing和subprocess）](#5-multiprocessingsubprocess)
      * [6. 多线程](#6-)
      * [协程](#)
      * [7. 字符编码](#7-)
      * [8. 内建函数](#8-)
   * [python3新特性](#python3)
      * [1. pathlib](#1-pathlib)
      * [2. f-string](#2-f-string)
* [2. 常用模块](#2-)
   * [标准模块](#)
      * [1. `sys`](#1-sys)
      * [2. `os`](#2-os)
      * [3. `os.path`](#3-ospath)
      * [4. `functools`](#4-functools)
      * [5. `subprocess`](#5-subprocess)
      * [6. `msvcrt`](#6-msvcrt)
      * [7.`math`](#7math)
      * [8. itertools](#8-itertools)
      * [9. str](#9-str)
      * [10. collections](#10-collections)
      * [11. logging](#11-logging)
      * [12. `time` 和 `datetime`](#12-time--datetime)
      * [13. `inspect`](#13-inspect)
      * [14. operator](#14-operator)
      * [15. contextlib](#15-contextlib)
      * [16. PIL](#16-pil)
      * [17. re](#17-re)
      * [18. struct 解析二进制或socket数据](#18-struct-socket)
   * [第三方模块](#)
      * [1. `scipy.stats`](#1-scipystats)
      * [scipy](#scipy)
      * [2. pandas](#2-pandas)
      * [3. numpy](#3-numpy)
      * [4. click](#4-click)
      * [5. sqlite3](#5-sqlite3)
      * [6. JSON 和 pickle](#6-json--pickle)
      * [7. six](#7-six)
      * [8. pathlib](#8-pathlib)
      * [9. schedule](#9-schedule)
      * [10. PyPDF2 和 Reportlab](#10-pypdf2--reportlab)
      * [11. matplotlib](#11-matplotlib)
      * [12. Bokeh](#12-bokeh)
      * [13. tqdm](#13-tqdm)
      * [14. statsmodels](#14-statsmodels)
      * [15. sklearn](#15-sklearn)
      * [15. seaborn](#15-seaborn)
   * [黑客模块](#)
      * [1. pywin32](#1-pywin32)
      * [2. psutil](#2-psutil)
      * [3. pypcap](#3-pypcap)
      * [4. pyhook](#4-pyhook)
      * [5. PyUserInput](#5-pyuserinput)
      * [6. pydivert](#6-pydivert)
      * [7. redsails](#7-redsails)
* [3. 模块比较](#3-)
   * [3.1. xml解析模块](#31-xml)
* [4. 学习资料](#4-)
   * [4.1 Python 资源大全中文版](#41-python-)
   * [4.2 \<\<Python Cookbook\>\>](#42-python-cookbook)
   * [4.3 python各路大神](#43-python)
   * [4.4 Python Code Examples](#44-python-code-examples)
   * [4.5 openCV](#45-opencv)
* [5. 编写规范](#5-)
   * [5.1 软件目录结构规范](#51-)
   * [5.2 宏基因组项目框架](#52-)
* [6. 常见问题](#6-)
   * [6.1 `mkl_serv_getenv: undefined symbol: mkl_serv_getenv`](#61-mkl_serv_getenv-undefined-symbol-mkl_serv_getenv)
   * [6.2 `nicodeEncodeError: 'charmap' codec can't encode characters in position 7-8: character maps to <undefined>`](#62-nicodeencodeerror-charmap-codec-cant-encode-characters-in-position-7-8-character-maps-to-undefined)
* [7. 优秀框架](#7-)
   * [爬虫](#)
      * [pyspider](#pyspider)
      * [scrapy](#scrapy)
   * [web服务](#web)
      * [Flask](#flask)
      * [Django](#django)
* [8. 第三方包安装教程](#8-)
   * [8.1 pypcap](#81-pypcap)
* [9. 常见问题及解决方案](#9-)
   * [9.1 numpy: ImportError: DLL load failed](#91-numpy-importerror-dll-load-failed)
<!--te-->

----

# python之禅

>Beautiful is better than ugly.

\# 优美胜于丑陋（Python以编写优美的代码为目标）

>Explicit is better than implicit.

\# 明了胜于晦涩（优美的代码应当是明了的，命名规范，风格相似） 

>Simple is better than complex.

\# 简洁胜于复杂（优美的代码应当是简洁的，不要有复杂的内部实现） 

>Complex is better than complicated.

\# 复杂胜于凌乱（如果复杂不可避免，那代码间也不能有难懂的关系，要保持接口简洁）

>Flat is better than nested.

\# 扁平胜于嵌套（优美的代码应当是扁平的，不能有太多的嵌套） 

>Sparse is better than dense.

\# 间隔胜于紧凑（优美的代码有适当的间隔，不要奢望一行代码解决问题） 

>Readability counts.

\# 可读性很重要（优美的代码是可读的） 

>Special cases aren't special enough to break the rules. 
<br>Although practicality beats purity.

\# 即便假借特例的实用性之名，也不可违背这些规则（这些规则至高无上） 

>Errors should never pass silently. 
<br>Unless explicitly silenced.

\# 不要包容所有错误，除非你确定需要这样做（精准地捕获异常，不写except:pass风格的代码） 

>In the face of ambiguity, refuse the temptation to guess.

\# 当存在多种可能，不要尝试去猜测 

>There should be one-- and preferably only one --obvious way to do it.

\# 而是尽量找一种，最好是唯一一种明显的解决方案（如果不确定，就用穷举法） 

>Although that way may not be obvious at first unless you're Dutch.

\# 虽然这并不容易，因为你不是 Python 之父（这里的Dutch是指Guido）

>Now is better than never.
<br>Although never is often better than *right* now.

\# 做也许好过不做，但不假思索就动手还不如不做（动手之前要细思量）

>If the implementation is hard to explain, it's a bad idea.
<br>If the implementation is easy to explain, it may be a good idea.

\# 如果你无法向人描述你的方案，那肯定不是一个好方案；反之亦然（方案测评标准） 

>Namespaces are one honking great idea -- let's do more of those!

\# 命名空间是一种绝妙的理念，我们应当多加利用（倡导与号召）

----

# python核心概念

## GIL和互斥锁

* [python面试不得不知道的点——GIL](https://blog.csdn.net/weixin_41594007/article/details/79485847)

以下是几个面试会遇到的问题，希望对大家有所帮助：

问题1: 什么时候会释放Gil锁

1. 遇到像 i/o操作这种 会有时间空闲情况 造成cpu闲置的情况会释放Gil
2. 会有一个专门ticks进行计数 一旦ticks数值达到100 这个时候释放Gil锁 线程之间开始竞争Gil锁(说明:
    ticks这个数值可以进行设置来延长或者缩减获得Gil锁的线程使用cpu的时间)

问题2: 互斥锁和Gil锁的关系

Gil锁  : 保证同一时刻只有一个线程能使用到cpu

互斥锁 : 多线程时,保证修改共享数据时有序的修改,不会产生数据修改混乱


首先假设只有一个进程,这个进程中有两个线程 Thread1,Thread2, 要修改共享的数据date, 并且有互斥锁

执行以下步骤

1. 多线程运行，假设Thread1获得GIL可以使用cpu，这时Thread1获得 互斥锁lock,Thread1可以改date数据(但并
没有开始修改数据)
2. Thread1线程在修改date数据前发生了 i/o操作 或者 ticks计数满100 (注意就是没有运行到修改data数据),这个
时候 Thread1 让出了Gil,Gil锁可以被竞争
3. Thread1 和 Thread2 开始竞争 Gil (注意:如果Thread1是因为 i/o 阻塞 让出的Gil Thread2必定拿到Gil,如果
Thread1是因为ticks计数满100让出Gil 这个时候 Thread1 和 Thread2 公平竞争)
4. 假设 Thread2正好获得了GIL, 运行代码去修改共享数据date,由于Thread1有互斥锁lock，所以Thread2无法更改共享数据
date,这时Thread2让出Gil锁 , GIL锁再次发生竞争 
5. 假设Thread1又抢到GIL，由于其有互斥锁Lock所以其可以继续修改共享数据data,当Thread1修改完数据释放互斥锁lock,
Thread2在获得GIL与lock后才可对data进行修改


## 进程、线程、协程

* [进程、线程、协程及IO模型](https://www.cnblogs.com/xuyaping/p/6825115.html)

----

# 1. python基础

## 基础

### 1. 字典格式化输出

使用`"%(key1)s" % Dict`格式

```
>>> d = {'a':'ABC', 'b':'DEF','c':'GHI', 'd':'JKL'}
>>> x = '%(a)s <=> %(b)s <=> %(c)s'
>>> print x %d
'ABC <=> DEF <=> GHI'
```

使用`str.format`方法

```
>>> d = {'a':'ABC', 'b':'DEF','c':'GHI', 'd':'JKL'}
>>> print '{a} <=> {b} <=> {c}'.format(**d)
'ABC <=> DEF <=> GHI'
```

### 2. `str.split('\\n')`与`str.splitlines`区别

`str.splitlines()`效果类似与`str.split('\n')`，不过不用在末尾加' '

```
>>> a='abc\ndef\nghi\n'
>>> a.split('\n')
['abc', 'def', 'ghi', '']
>>> a.splitlines()
['abc', 'def', 'ghi']
```
### 3. `exec`, `eval`和`repr`区别

`exec`：用来执行存储在字符串或文件中的python语句
`eval`：用来执行存储在字符串或文件中的python语句
`repr`：来取得对象的规范字符串表示。反引号（也称转换符）可以完成相同的功能。注意，在大多数时候有eval（repr（object））==object
将字符串转换为整形
```
>>> exec 'a = 1'
>>> a
1
>>> eval('3+4*7+2**-2')
31.25
>>> i = ['item']
>>> repr(i)
"['item']"
```
### 4. 查看内建函数

使用`__builtins__`或`__builtin__`

```
>>> dir(__builtins__)
```
```
>>> import __builtin__
>>> dir()
```

### 5. 查看模块的所有属性和方法

```
>>> import 模块
>>> dir(模块)
```

### 6. `input`的新特性

```
#可以接受两端带有空白的数字
>>> int(" 123    ")
123
#可以处理\n, \t
>>> int(" 123 \t \n ")
123
```

### 7. python的标准流与shell的管道联用

`sorter.py` <font color="gray"> # 一次性从stdin中读取所有输入 </font>

```
import os
lines = sys.stdin.readlines()
lines.sort()
for line in lines: print(line, end="")
```

`sorter2.py` <font color="gray"> # 一次性从stdin读取一行 </font>

```
import sys
lines = []
while True:
    lines.append(sys.stdin.readline())
    if not line: break
lines.sort()
for line in lines: print(line, end="")
```

`adder.py`   <font color="gray"> # 每次只读取一行 </font>

```
sum = 0
while True:
    try:
        line = input()
    except EOFError:
        break
    else:
        sum += int(line)
print(sum)
```

`data.txt`

```
123
000
999
042
```

和shell的管道联用

```
> cat data.txt | sorter.py | adder.py
1164
```

实际上，这两个脚本可以更精简，使用内部的sorted函数生成器表达式、文件迭代器 :

`sorterSmall.py`

```
import sys
for line in sorted(sys.stdin): print(line, end="")
```

`adderSmall.py`

```
import sys
print(sum(int(line) for line in sys.stdin))
```

### 8. 列表推导式中使用多个for

```
>>> a=['A','B','C','D']
>>> [(i,ii) for i in a for ii in a if i<ii]
[('A', 'B'), ('A', 'C'), ('A', 'D'), ('B', 'C'), ('B', 'D'), ('C', 'D')]
```

### 9. 智能排序

[根据字符串中的数字排序，如f10应该在f2后面](https://blog.csdn.net/houyj1986/article/details/22966799)

```
# 排序后效果：['M1','M2','M3','M10','M11']
# 如果使用sorted函数或sort方法，排序后结果为：['M1','M10','M11','M2','M3']，不是我们希望的
import re

def strnum(s):
    p = re.split(r'(\d+)',s)
    p[1::2] = map(int, p[1::2])
    return p

x = ['M1','M10','M11','M2','M3']
print sorted(x, key=strnum) # ['M1','M2','M3','M10','M11']
```

**根据某个列表对另一个列表排序**

```
import numpy as np
a=['b','d','a','c']
b=[2,4,1,3]
# 根据b对a排序
ind=np.lexsort((a,b)) #array([2, 0, 3, 1])
print [a[i] for i in ind] #['a', 'b', 'c', 'd']
```

**根据字典的值排序**

```
sorted(dict.items(), key=lambda e:e[1], reverse=True)
```


### 10. 排列组合

[Python 排列组合的计算](http://blog.csdn.net/lanchunhui/article/details/51824602)

$$A_2^3=6,  \binom{3}{2}=3$$

* 调用scipy计算排列组和的具体数值

```
>>> from scipy.special import comb.perm
>>> perm(3, 2)
6.0
>>> comb(3, 2)
3.0
```

* 调用itertools获取排列组合的全部情况数

```
>>> from itertools import combinations, permutations
>>> permutations([1, 2, 3], 2)
<itertools.permutations at 0x7febfd880fc0>
>>> list(permutations([1, 2, 3], 2))
[(1,2), (1,3), (2,1), (2,3), (3,1), (3,2)]
>>> list(combinations([1, 2, 3], 2))
[(1,2), (1,3), (2,3)]
```

### 11.\_\_import\_\_ 与动态加载 python module

[http://python.jobbole.com/87492/](http://python.jobbole.com/87492/)

>Direct use of \_\_import\_\_() is rare, except in cases where you want to import a module whose name is only known at runtime.

本文介绍 python module 的动态加载，我们有时希望从配置文件等地获取要被动态加载的 module，但是所读取的配置项通常为字符串类型，无法用 import 加载，例如：

```
>>> import 'os'
 File "<stdin>", line 1
 import 'os'
 ^
SyntaxError: invalid syntax
```

Python 提供内建函数 \_\_import\_\_ 动态加载 module，\_\_import\_\_ 的用法如下：

```
__import__ (name[, globals[, locals[, fromlist[, level]]]])
```

* name (required): 被加载 module 的名称
* globals (optional): 包含全局变量的字典，该选项很少使用，采用默认值 global()
* locals (optional): 包含局部变量的字典，内部标准实现未用到该变量，采用默认值 local()
* fromlist (Optional): 被导入的 submodule 名称
* level (Optional): 导入路径选项，默认为 -1，表示同时支持 absolute import 和 relative import

```
>>> os_module = __import__('os')
>>> print os_module.path
<module 'posixpath' from '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/posixpath.pyc'>
```

事实上，import 本质上是调用 \_\_import\_\_ 加载 module 的，比如：

```
import foo

最终调用如下函数实现

foo = __import__('foo', globals(), locals(), [], -1)
```

`import numpy as np`

相当于

`np = __import__("numpy",fromlist=[""])`

`from pandas import Series,Dataframe`

相当于：

`__import__("pandas",fromlist=["Series","Dataframe"])`

但如果使用不善，也容易踩坑：

```
>>> __import__("os")
<module 'os' from '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/os.pyc'>

>>> __import__("os.path")
<module 'os' from '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/os.pyc'>
```

如果输入的参数如果带有 “.”，采用 \_\_import\_\_ 直接导入 module 容易造成意想不到的结果。 OpenStack 的 oslo.utils 封装了 \_\_import\_\_，支持动态导入 class, object 等。

```
import sys
import traceback


def import_class(import_str):
    """Returns a class from a string including module and class.
    .. versionadded:: 0.3
    """
    mod_str, _sep, class_str = import_str.rpartition('.')
    __import__(mod_str)
    try:
        return getattr(sys.modules[mod_str], class_str)
    except AttributeError:
        raise ImportError('Class %s cannot be found (%s)' %
                          (class_str,
                           traceback.format_exception(*sys.exc_info())))


def import_object(import_str, *args, **kwargs):
    """Import a class and return an instance of it.
    .. versionadded:: 0.3
    """
    return import_class(import_str)(*args, **kwargs)


def import_module(import_str):
    """Import a module.
    .. versionadded:: 0.3
    """
    __import__(import_str)
    return sys.modules[import_str]
```

### 12. print带汉字的字典或列表

如果print带汉字的变量，显示的就是汉字，但是，如果print带汉字的字典或列表，显示的却是字节码。

```
>>> x = "中国"
>>> x
\xe4\xb8\xad\xe5\x9b\xbd    #字节码
>>> print x
中国
```
为什么 `x` 和 `print x`显示的结果不同呢？在查看print官方文档时发现，在python里面print是一个非常厉害的小家伙：它能把几乎任何常见类型的对象打印成一串文字，甚至包括列表、字典、元组等等。这在别的语言里是不可理解的，所以给从其他语言转过来的人埋了个大坑。总之：Python中出现的任何中文，虽然我们在编辑器里看到的是中文，但是背地里全是一串编码。千万不要轻易信任print！print xx给你显示出来的，其实并不是xx的真实面貌！
具体可查看[Python中文字符的理解：str()、repr()、print](https://www.cnblogs.com/omg24/p/5048319.html)
但是，字典和列表就不同了：
```
>>> y = {"lang": "汉字", "country":"中国"}
>>> y
{'country': '\xe4\xb8\xad\xe5\x9b\xbd', 'lang': '\xe6\xb1\x89\xe5\xad\x97'}
>>> print y
{'lang': '\xe6\xb1\x89\xe5\xad\x97', 'country': '\xe4\xb8\xad\xe5\x9b\xbd'}
```

为什么字典和列表中的汉字没有被print正确显示出来呢？
个人理解为：print会将所有对象都转化为字符串，然后在打印出来，及 `print obj = print str(obj)`  或者说`print obj = print obj.__str__()`。那么我们来看看str函数或者__str__方法是什么吧。

```
>>> x = "中国"
>>> y = {"lang": "汉字", "country":"中国"}
>>> x
'\xe4\xb8\xad\xe5\x9b\xbd'
>>> str(x)
'\xe4\xb8\xad\xe5\x9b\xbd'
>>> x.__str__()
'\xe4\xb8\xad\xe5\x9b\xbd'
>>> y
{'country': '\xe4\xb8\xad\xe5\x9b\xbd', 'lang': '\xe6\xb1\x89\xe5\xad\x97'}
>>> str(y)
"{'lang': '\\xe6\\xb1\\x89\\xe5\\xad\\x97', 'country': '\\xe4\\xb8\\xad\\xe5\\x9b\\xbd'}"
>>> y.__str__()
"{'lang': '\\xe6\\xb1\\x89\\xe5\\xad\\x97', 'country': '\\xe4\\xb8\\xad\\xe5\\x9b\\xbd'}"
```

可以看到str(字符串)还是它本身，但是str(字典或列表)被转化为了标准化的字符串，即"\x"转义成了"\\\x"，所以再调用print时，看到的还是"\x"。那么如果不让"\x"转义为"\\\x"时，是否就能正常使用print了呢？让我们验证一下

```
>>> print "{'country': '\xe4\xb8\xad\xe5\x9b\xbd', 'lang': '\xe6\xb1\x89\xe5\xad\x97'}"
{'country': '中国', 'lang': '汉字'}
```
bingo! 但接下来又有一个问题，怎么阻止转义呢？可以使用<font color="red">**`str.decode("string_escape")`**</font>来实现
参考：[python：print含有中文的list](http://blog.csdn.net/poinsettia/article/details/52021845)
```
>>> y = {"lang": "汉字", "country":"中国"}
>>> z = str(y).decode("string_escape")
>>> z
"{'lang': '\xe6\xb1\x89\xe5\xad\x97', 'country': '\xe4\xb8\xad\xe5\x9b\xbd'}"
>>> print z
{'lang': '汉字', 'country': '中国'}
```

### 13. 通过配置文件共享全局变量

[python通过配置文件共享全局变量](http://blog.csdn.net/suzyu12345/article/details/51534015)

[Python实现跨文件全局变量的方法](https://www.cnblogs.com/rnckty/p/7722603.html)

[python读conf配置文件--ConfigParser](http://blog.chinaunix.net/uid-24585858-id-4820471.html)

[python的ConfigParser模块](http://blog.csdn.net/miner_k/article/details/77857292)

在使用Python编写的应用的过程中，有时会遇到多个文件之间传递同一个全局变量的情况，此时通过配置文件定义全局变量是一个比较好的选择。
首先配置config.py模块，config需要设置get_xxx和set_xxx的方法提供对外的接口。

```
class global_var:
    '''需要定义全局变量的放在这里，最好定义一个初始值'''
    name = 'my_name'
# 对于每个全局变量，都需要定义get_value和set_value接口 
def set_name(name):
    global_var.name = name 
def get_name():
    return global_var.name
```

然后在其他模块引用：
test.py

```
import config 
# 引用全局变量 
name = config.get_name() 
# 修改全局变量 
config.set_name('new_name') 
# 查看修改后的全局变量 
print(config.get_name())
```

注意： 
1. import配置文件时，不要from xxx import *, 而要import config.py 
2. 在config.py文件中，用set_xxxValue()和get_xxxValue来提供外部访问接口，这个好处是，可以让全局变量在每次调用的时候都能得到刷新 
3. 其他文件使用get_xxxValue()获取到全局变量的最新值
另外，对于global这个声明，他只是在同一个文件中有效，并不能跨文件，就是夸module.所以不要妄想通过global来控制不同文件间的共享变量。


### 14. @staticmethod 和 @classmethod的区别

[飘逸的python - @staticmethod和@classmethod的作用与区别](http://blog.csdn.net/handsomekang/article/details/9615239)

[Python 中的 classmethod 和 staticmethod 有什么具体用途？ - 李保银的回答](https://www.zhihu.com/question/20021164/answer/18224953)

一般来说，要使用某个类的方法，需要先实例化一个对象再调用方法。
而使用@staticmethod或@classmethod，就可以不需要实例化，直接类名.方法名()来调用。
这有利于组织代码，把某些应该属于某个类的函数给放到那个类里去，同时有利于命名空间的整洁。

既然@staticmethod和@classmethod都可以直接类名.方法名()来调用，那他们有什么区别呢
从它们的使用上来看,
* @staticmethod不需要表示自身对象的self和自身类的cls参数，就跟使用函数一样。
* @classmethod也不需要self参数，但第一个参数需要是表示自身类的cls参数。

如果在@staticmethod中要调用到这个类的一些属性方法，只能直接类名.属性名或类名.方法名。
而@classmethod因为持有cls参数，可以来调用类的属性，类的方法，实例化对象等，避免硬编码。


### 15. pip使用国内镜像

[让PIP源使用国内镜像，提升下载速度和安装成功率。](https://www.cnblogs.com/microman/p/6107879.html)

对于Python开发用户来讲，PIP安装软件包是家常便饭。但国外的源下载速度实在太慢，浪费时间。而且经常出现下载后安装出错问题。所以把PIP安装源替换成国内镜像，可以大幅提升下载速度，还可以提高安装成功率。

**国内源：**

* 新版ubuntu要求使用https源，要注意。
* 清华：https://pypi.tuna.tsinghua.edu.cn/simple
* 阿里云：http://mirrors.aliyun.com/pypi/simple/
* 中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/
* 华中理工大学：http://pypi.hustunique.com/
* 山东理工大学：http://pypi.sdutlinux.org/ 
* 豆瓣：http://pypi.douban.com/simple/

**临时使用：**

可以在使用pip的时候加参数-i https://pypi.tuna.tsinghua.edu.cn/simple
例如：pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pyspider，这样就会从清华这边的镜像去安装pyspider库。

**永久修改，一劳永逸：**

Linux下，修改 ~/.pip/pip.conf (没有就创建一个文件夹及文件。文件夹要加“.”，表示是隐藏文件夹)
内容如下：

```
[global] 
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install] 
trusted-host=mirrors.aliyun.com
```

windows下，直接在user目录中创建一个pip目录，如：C:\Users\xx\pip，新建文件pip.ini。内容同上。


### 16. python内存变量保存到磁盘, 方便下次读入

[http://blog.csdn.net/u012605050/article/details/77940798](http://blog.csdn.net/u012605050/article/details/77940798)

保存变量:

```
import numpy as np
import dill

T='Hiya'
val=[1,2,3]
a = np.zeros([4,5])

filename= 'globalsave.pkl'
dill.dump_session(filename)
```

读取变量:

```
import numpy as np
import dill

# load the session again
dill.load_session(filename)
```


### 17. 查看内存汇总的所有变量

```
In [3]: who
In Out abund abund1 abund2 abund3 abund_file dill filename  
groups i mpl np pd x y z
```

### 18. python的搜索路径

python搜索包是会从几个地方来查找路径：

1. 当前路径
2. $PYTHONPATH
3. /lib/python2.7/site-package/*.pth
4. /lib/python2.7/site-package  [默认]

### 18.1 python的环境变量

```
export PATH=/share/public/software/python/2.7.14/bin:$PATH
export LD_LIBRARY_PATH=/share/public/software/python/2.7.14/lib:$LD_LIBRARY_PATH
```

`LD_LIBRARY_PATH`可以设置PYTHONPATH为`/share/public/software/python/2.7.14/lib/python2.7`


### 19. 数据的归一化/标准化/正则化

[http://www.cnblogs.com/chaosimple/p/4153167.html](http://www.cnblogs.com/chaosimple/p/4153167.html)

**标准化（Z-Score），或者去除均值和方差缩放**

公式为：(X-mean)/std  计算时对每个属性/每列分别进行。
将数据按期属性（按列进行）减去其均值，并处以其方差。得到的结果是，对于每个属性/每列来说所有数据都聚集在0附近，方差为1。
实现时，有两种不同的方式：

1. 使用sklearn.preprocessing.scale()函数，可以直接将给定数据进行标准化。

```
>>> from sklearn import preprocessing
>>> import numpy as np
>>> X = np.array([[ 1., -1.,  2.],
...               [ 2.,  0.,  0.],
...               [ 0.,  1., -1.]])
>>> X_scaled = preprocessing.scale(X)
 
>>> X_scaled                                          
array([[ 0.  ..., -1.22...,  1.33...],
       [ 1.22...,  0.  ..., -0.26...],
       [-1.22...,  1.22..., -1.06...]])
 
>>>#处理后数据的均值和方差
>>> X_scaled.mean(axis=0)
array([ 0.,  0.,  0.])
 
>>> X_scaled.std(axis=0)
array([ 1.,  1.,  1.])
```

2. 使用sklearn.preprocessing.StandardScaler类，使用该类的好处在于可以保存训练集中的参数（均值、方差）直接使用其对象转换测试集数据。

```
>>> scaler = preprocessing.StandardScaler().fit(X)
>>> scaler
StandardScaler(copy=True, with_mean=True, with_std=True)
 
>>> scaler.mean_                                      
array([ 1. ...,  0. ...,  0.33...])
 
>>> scaler.std_                                       
array([ 0.81...,  0.81...,  1.24...])
 
>>> scaler.transform(X)                               
array([[ 0.  ..., -1.22...,  1.33...],
       [ 1.22...,  0.  ..., -0.26...],
       [-1.22...,  1.22..., -1.06...]])
 
 
>>>#可以直接使用训练集对测试集数据进行转换
>>> scaler.transform([[-1.,  1., 0.]])                
array([[-2.44...,  1.22..., -0.26...]])
```

**将属性缩放到一个指定范围**

除了上述介绍的方法之外，另一种常用的方法是将属性缩放到一个指定的最大和最小值（通常是1-0）之间，这可以通过preprocessing.MinMaxScaler类实现。
使用这种方法的目的包括：
1、对于方差非常小的属性可以增强其稳定性。
2、维持稀疏矩阵中为0的条目。

```
>>> X_train = np.array([[ 1., -1.,  2.],
...                     [ 2.,  0.,  0.],
...                     [ 0.,  1., -1.]])
...
>>> min_max_scaler = preprocessing.MinMaxScaler()
>>> X_train_minmax = min_max_scaler.fit_transform(X_train)
>>> X_train_minmax
array([[ 0.5       ,  0.        ,  1.        ],
       [ 1.        ,  0.5       ,  0.33333333],
       [ 0.        ,  1.        ,  0.        ]])
 
>>> #将相同的缩放应用到测试集数据中
>>> X_test = np.array([[ -3., -1.,  4.]])
>>> X_test_minmax = min_max_scaler.transform(X_test)
>>> X_test_minmax
array([[-1.5       ,  0.        ,  1.66666667]])
 
 
>>> #缩放因子等属性
>>> min_max_scaler.scale_                             
array([ 0.5       ,  0.5       ,  0.33...])
 
>>> min_max_scaler.min_                               
array([ 0.        ,  0.5       ,  0.33...])
```

当然，在构造类对象的时候也可以直接指定最大最小值的范围：feature_range=(min, max)，此时应用的公式变为：
```
X_std=(X-X.min(axis=0))/(X.max(axis=0)-X.min(axis=0))

X_scaled=X_std/(max-min)+min
```

**正则化（Normalization）**

正则化的过程是将每个样本缩放到单位范数（每个样本的范数为1），如果后面要使用如二次型（点积）或者其它核方法计算两个样本之间的相似性这个方法会很有用。
Normalization主要思想是对每个样本计算其p-范数，然后对该样本中每个元素除以该范数，这样处理的结果是使得每个处理后样本的p-范数（l1-norm,l2-norm）等于1。
             p-范数的计算公式：||X||p=(|x1|^p+|x2|^p+...+|xn|^p)^1/p
该方法主要应用于文本分类和聚类中。例如，对于两个TF-IDF向量的l2-norm进行点积，就可以得到这两个向量的余弦相似性。

1. 可以使用preprocessing.normalize()函数对指定数据进行转换：

```
>>> X = [[ 1., -1.,  2.],
...      [ 2.,  0.,  0.],
...      [ 0.,  1., -1.]]
>>> X_normalized = preprocessing.normalize(X, norm='l2')
 
>>> X_normalized                                      
array([[ 0.40..., -0.40...,  0.81...],
       [ 1.  ...,  0.  ...,  0.  ...],
       [ 0.  ...,  0.70..., -0.70...]])
```

2. 可以使用processing.Normalizer()类实现对训练集和测试集的拟合和转换：

```
>>> normalizer = preprocessing.Normalizer().fit(X)  # fit does nothing
>>> normalizer
Normalizer(copy=True, norm='l2')
 
>>>
>>> normalizer.transform(X)                            
array([[ 0.40..., -0.40...,  0.81...],
       [ 1.  ...,  0.  ...,  0.  ...],
       [ 0.  ...,  0.70..., -0.70...]])
 
>>> normalizer.transform([[-1.,  1., 0.]])             
array([[-0.70...,  0.70...,  0.  ...]])
```


### 20. for...else...语法

[Python循环语句中else的用法总结](http://www.jb51.net/article/92440.htm)

```
#coding:utf-8

def findn(n):
    for i in range(5):
        if i == n:
            print "find {}".format(n)
            break
    else:
        print "not find {}".format(n)

findn(5)
findn(3)
```

总结：`for...else...`和`while...else...`语法在满足一下情况时，`else`会被执行：

- `for`或`while`循环里的语句执行完成
- `for`或`while`循环里的语句没有被`break`或`return`语句打断


### 21. 将png合成gif

[Python3.4.3中使用imageio库png合成gif](https://blog.csdn.net/qq_30650153/article/details/78374647?locationNum=5&fps=1)

分解操作步骤

* step1：找到所有给定的png图片 
* step2：使用glob将所有png图片放入一个list 
* step3：Save them as frames into a gif

demo

```
#!/bin/python3

import imageio
import glob
import re

def create_gif(image_list, gif_name):  

    frames = []  
    for image_name in image_list:  
        frames.append(imageio.imread(image_name))  
    # Save them as frames into a gif   
    imageio.mimsave(gif_name, frames, 'GIF', duration = 0.8)  

    return 
def find_all_png():

    png_filenames = glob.glob(r"/home/py_learning/createGIF/*.png") 
    buf=[]
    for png_file in png_filenames:
        buf.append(png_file)
    return buf

if __name__ == '__main__':

    buff = find_all_png()
    create_gif(buff,'created_gif.gif' )
```


### 22. 捕获警告

[python捕获警告的方法](https://blog.csdn.net/YMD8005/article/details/77980718)

```
 import warnings
 warnings.filterwarnings('error')

 try:
    ...
except Warning:
    print 'Warning was raised as an exception!'
```

### 23. 将PDF转成PNG

[windows下用Python把pdf文件转化为图片(png格式)](https://blog.csdn.net/sqlserverdiscovery/article/details/51425543)

[PythonMagick](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pythonmagick) 需要先安装ImageMagick，还需要安装ghostscript

ghostscript 需要先安装 [Ghostscript](https://www.ghostscript.com/download/gsdnld.html)


### 24. os.walk()和os.path.walk()区别

[python os.walk()和os.path.walk()](https://www.cnblogs.com/zmlctt/p/4222621.html)

> os.path.walk()在python3中被取消


### 25. 以非root身份安装module

`pip`

```
pip install six --target="/usr/lib/python2.7/dist-packages"
```

`setup.py`

```
```


### 26. 执行shell命令

这篇文章主要介绍了python中执行shell命令的几个方法,本文一共给出4种方法实现执行shell命令,需要的朋友可以参考下

最近有个需求就是页面上执行shell命令，第一想到的就是`os.system`，

 ```
 os.system('cat /proc/cpuinfo')
 ```

但是发现页面上打印的命令执行结果 0或者1，当然不满足需求了。

 
尝试第二种方案 `os.popen()`

```
output = os.popen('cat /proc/cpuinfo')
print output.read()
```

通过 `os.popen()` 返回的是 file read 的对象，对其进行读取 `read()` 的操作可以看到执行的输出。但是无法读取程序执行的返回值）

 

尝试第三种方案 `commands.getstatusoutput()` 一个方法就可以获得到返回值和输出，非常好用。

python3中为`subprocess.getstatusoutput()`

```
(status, output) = commands.getstatusoutput('cat /proc/cpuinfo')
print status, output
```

Python Document 中给的一个例子，

```
>>> import commands
>>> commands.getstatusoutput('ls /bin/ls')
(0, '/bin/ls')
#【返回一个元组（status，output）】
>>> commands.getstatusoutput('cat /bin/junk')    
(256, 'cat: /bin/junk: No such file or directory')
>>> commands.getstatusoutput('/bin/junk')
(256, 'sh: /bin/junk: not found')
#【判断Shell命令的输出内容】【会阻塞】
>>> commands.getoutput('ls /bin/ls') 
'/bin/ls'
#【返回Shell命令返回值的方法， 但是这个结果只能判读其成功执行与否】
#【该函数已被python丢弃，不建议使用，它返回ls -ld file 的结果（String）】
>>> commands.getstatus('/bin/ls')  
'-rwxr-xr-x 1 root 13352 Oct 14 1994 /bin/ls'
```
 

第四种方法`subprocess.call`

```
import subprocess
subprocess.call(['ls','-a','/'])
subprocess.Popen('ls -a /',shell=True)
```

如果通过subrpocess利用nohup向后台提交一个任务，怎么获得后台运行任务的pid：

```
a=subprocess.Popen('nohup python a.py >nohup.out & echo $!', shell=True,stdout=subprocess.PIPE)
a.communicate()   【缺点：只有等待后台任务运行完毕，才能获得pid】，记得要加参数：stdout=subprocess.PIPE
a.pid()  【注意：返回的是当前脚本的pid，而不是后台任务的pid】
```

更好的方法，还没有想到！，有个折中的方法：

```
a=subprocess.Popen('nohup python a.py >nohup.out & echo "$!\ta.py">>run.pid', shell=True)
```


### 27. Python 对数字的千分位处理

法1：

```
>>> "{:,}".format(56381779049)
'56,381,779,049'
>>> "{:,}".format(56381779049.1)
'56,381,779,049.1'
```

法2：

```
>>> import re
>>> subject = '1234567'
>>> result = re.sub(r"(?<=\d)(?=(?:\d\d\d)+$)", ",", subject)
>>> result
'1,234,567'
```

法3：

```
>>> import re
>>> subject = '1234567'
>>> result = re.sub(r"(\d)(?=(\d\d\d)+(?!\d))", r"\1,", subject)
>>> result
'1,234,567'
```


### 28. 按位运算

win32api用SendMessage函数向窗口发送鼠标消息时，其中鼠标坐标就用到了按位运算，
我们先来看一下SendMessage函数的定义：

```
# Send a message to a window.
LRESULT SendMessage(
	hwnd,        # PyHANDLE, 目标窗口的句柄
	idMessage,   # int, 要发送的消息, 鼠标左击消息为：WM_NCLBUTTONDOWN
	wParam,      # int/string, 其含义是指当鼠标按键被点击时，其他功能键是否被按下
	lParam       # int/string, 其含义是指鼠标单击的位置，其中X坐标为低字节，Y坐标为高字节，
	             # 由于int型为32位，因此我们只需将Y坐标左移16位,然后再加上X坐标即可，即X + (Y << 16)
)
```

假如鼠标坐标为(500,400)，那么lParam的值应该为：`500 + (400 << 16) = 26214900`

那么加入我们只知道lParam的值，怎么推导出鼠标坐标呢? 直接上代码：

```
lParam = 26214900
x = (lParam & 0x0000FFFF)           # 500
y = (lParam & 0xFFFF0000) >> 16     # 400
```

上面运用的就是按位与运算，下面我们再来看看其它按位运算：

```
a = 26214900
hex(a)            # a的16进制表示法: '0xC0FFEE'
oct(a)            # a的8进制表示法: '0o144000764'
bin(a)            # a的2进制表示法: '0b1100100000000000111110100'

a & 0xFF          # 按位与运算    244
a | 0xFF          # 按位或运算    26214911
a ^ 0xFF          # 按位异或运算  26214667
~a                # 取反,非运算   -26214901
a << 2            # 左移          104859600
a >> 2            # 右移          6553725
```


### 29. 进制


**进制间的相互转化**

```
a10 = 100
a2 = bin(a10)      # '0b1100100'
a8 = oct(a10)      # '0o144'
a16 = hex(a10)     # '0x64'
a2 = int(a16, 16)
a2 = int(a8, 8)
a2 = int(a2, 2)
```

| 进制 | 2进制 | 8进制 | 10进制 | 16进制 |
| :----- | ------ | ------ | ------ | ------ |
| 2进制 | - | bin(int(x, 8)) | bin(int(x, 10)) | bin(int(x, 16)) |
| 8进制 | oct(int(x, 2)) | - | oct(int(x, 10)) | oct(int(x, 16)) |
| 10进制 | int(x, 2) | int(x, 8) | - | int(x, 16) |
| 16进制 | hex(int(x, 2)) | hex(int(x, 8)) | hex(int(x, 10)) | - |



**字符串 - 字节 - 二进制 - 十六进制 间的相互转换**

```
def encode(s):
    return ' '.join([bin(ord(c)).replace('0b', '') for c in s])
 
def decode(s):
    return ''.join([chr(i) for i in [int(b, 2) for b in s.split(' ')]])

>>>encode('hello')
'1101000 1100101 1101100 1101100 1101111'
>>>decode('1101000 1100101 1101100 1101100 1101111')
'hello'

### 将字符串转换成字节 (str to bytes)
# py2没有encoding参数，返回的是用字符表示的字节
# py3必须使用encoding参数, 返回的是字节
bytes(s, encoding = "utf8")
# 或
str.encode(s)

# 以python3为例
>>> bytes("abc",encoding="ASCII")
b'abc'
>>> bytes("中国", encoding="utf-8")
b'\xe4\xb8\xad\xe5\x9b\xbd'
>>> bytes("中国", encoding="gbk")
b'\xd6\xd0\xb9\xfa'
>>> str.encode("中国", encoding="gbk")

### 将字节转成二进制
>>> bt = bytes("中国", encoding="gbk") # b'\xd6\xd0\xb9\xfa'
>>> [i for i in bt]
[214, 208, 185, 250]
>>> [bin(i) for i in bt]
['0b11010110', '0b11010000', '0b10111001', '0b11111010']

### 将ints(0<=n<256)列表转成bytes
>>> bt = bytes([214, 208, 185, 250])
b'\xd6\xd0\xb9\xfa'


# 将字节转成字符串(bytes to str)
str(b, encoding = "utf-8")
# 或
bytes.decode(b)

>>> str(bt, encoding="gbk")
'中国'
>>> bytes.decode(bt, encoding="gbk")


### 字符串与十六进制间的相互转换

def encode(s):
	return (' '.join([hex(ord(c)).replace('0x', '') for c in s])).upper()

def decode(s):
	return ''.join([chr(i) for i in [int(b,16) for b in s.split(' ')]])

>>>encode('hello')
'68 65 6C 6C 6F'
>>>decode('68 65 6C 6C 6F')
'hello'
```

**浮点数 - 二进制 间的转换**

* [十进制浮点数转成二进制(IEEE 754 在线计算器)](https://blog.csdn.net/zhengyanan815/article/details/78550073?locationNum=2&fps=1)
* [从Python的0.1输出0.1000000000000001说浮点数的二进制](https://blog.csdn.net/u012843100/article/details/60885763)



### 30. 模拟SSH登录和SCP传输

* [Python的scp小工具](https://www.jianshu.com/p/aa7411f346cc)
* [_scp_read_response checking for wrong response values](https://bitbucket.org/ericvsmith/scpclient/issues/7/_scp_read_response-checking-for-wrong)
* [paramiko 详解](https://blog.csdn.net/weixin_39912556/article/details/80576624)
* []()

scp是我们在shell上经常使用的命令，用来远程传输文件。python上也能做到scp的功能，需要依赖以下库：

pip install paramiko

pip install scpclient

实际实现也就几行代码：

```
#创建ssh访问
ssh = paramiko.SSHClient()
ssh.load_system_host_keys()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())#允许连接不在know_hosts文件中的主机
sh.connect(hostname, port=22, username=zhangsan, password=password)#远程访问的服务器信息
   
#创建scp
with closing(scpclient.Write(ssh.get_transport(), remote_path=remote_path)) as scp:
    scp.send_file(local_filename, preserve_times=True, remote_filename=remote_filename)
```

其中，`ssh.connect()`中需要指定远程访问的服务器的ip端口，用户名以及密码；`scpclient.Write()`中指定
远程服务器的路径remote_path；`scp.send_file()`中指定本地传输的文件名(全路径)，远程主机的文件
名remote_filename。大概就是这些地方需要注意的。

scpclient模块的主要函数：

* Read：从远程服务器下载文件
* ReadDir：从远程服务器下载文件夹
* Write：将文件上传到远程服务器
* WriteDir：将文件夹上传到远程服务器

需要注意：scpclient中Read和ReadDir函数好像不能正常使用，但Write和WriteDir正常

当需要从远程服务器下载文件或文件夹时，可以使用paramiko模块的SFTPClient.from_transport函数：

```
# FTP下载
# sftp = paramiko.SFTPClient.from_transport(ssh.get_transport())
def sftp_backdir(sftp, remote_dir, local_dir):                                                                                      
    mkdir(local_dir)
    for dfile in sftp.listdir_attr(remote_dir):
        remote_dfile = os.path.join(remote_dir, dfile.filename)
        local_dfile = os.path.join(local_dir, dfile.filename)
        if dfile.filename[0] == ".":
            continue
        if dfile.longname[0] == "d":  # 判断远程服务器上该文件是否是文件夹
            sftp_backdir(sftp, remote_dfile, local_dfile)
        else:
            sftp.get(remote_dfile, local_dfile)

```


### 31. 获得本机IP

```
import socket

def get_host_ip():
    """
    查询本机ip地址
    :return: ip
    """
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
        s.connect(('8.8.8.8', 80))
        ip = s.getsockname()[0]
    finally:
        s.close()

    return ip

if __name__ == '__main__':
    print(get_host_ip())
```

### 32. 获得两个概率密度函数交集区域内的概率

* [非参数估计：核密度估计KDE](https://blog.csdn.net/pipisorry/article/details/53635895)
* [scipy.stats.gaussian_kde](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.gaussian_kde.html)
* [statsmodels.nonparametric.kde.KDEUnivariate](http://www.statsmodels.org/devel/generated/statsmodels.nonparametric.kde.KDEUnivariate.html)
* [Source code for statsmodels.nonparametric.kde](http://www.statsmodels.org/stable/_modules/statsmodels/nonparametric/kde.html#KDEUnivariate.cdf)
* [Kernel Density Estimation in Python(python各模块中密度核函数比较)](https://jakevdp.github.io/blog/2013/12/01/kernel-density-estimation/)

虽然采用不同的核函数都可以获得一致性的结论（整体趋势和密度分布规律性基本一致），
但核密度函数也不是完美的。除了核算法的选择外，带宽（bandwidth）也会影响密度估计，
过大或过小的带宽值都会影响估计结果。

```
import seaborn as sns
import matplotlib.pyplot as plt
import statsmodels
import scipy
import numpy as np

data = np.random.sample(1000)
data1 = data + 0.3

fig,ax = plt.subplots()
# 绘制核密度图(高斯密度核函数，带宽(bw))
# 如果安装了statsmodels模块，使用statsmodels.nonparametric.kde.KDEUnivariate(),
# 否则使用scipy.stats.gaussian_kde()来估计核密度
# 这两组数据的密度图完全一致，data1只是向右平移了0.3
sns.kdeplot(data, ax=ax, kernel='gau', bw='scott', gridsize=100, cut=3, clip=None)
sns.kdeplot(data1, ax=ax, kernel='gau', bw='scott', gridsize=100, cut=3, clip=None)

# sns.kdeplot返回的ax，没有密度函数，为了计算这两个密度图交集的面积，我们需要重新
# 计算kde
kde = statsmodels.nonparametric.kde.KDEUnivariate(data)
kde.fit(kernel="gau", bw="scott", fft="gau", gridsize=100, cut=3)
# 为了计算两个密度函数交集区域的面积，需要先获得焦点的x值。
# 为了偷懒，将两峰间x轴分为n=30份，如果xi点在图1上的密度值大于图2上的密度值,
# x(i+1)点在图1上的密度值小于图2上的密度值，则焦点的x值肯定大于等于xi,小于等于
# x(i+1)，我们姑且让其等于平均值
# 注意：如果想要准确求得该交点x值，需要使用符号运算
peak_x = kde.support[kde.density.argmax()] # 获得峰值对应的x的值
peak_interval = 0.3 # 两图峰值对应x值的间距
seek_bin = 0.01 # 将x分为30份，每份长度0.01
points = np.arange(peak_x, peak_x+peak_interval, seek_bin) # 获得所有xi
# 粗略求得交点的x值(pp)
for i in range(len(points)-1):
    if i == 0:
        r0 = kde.evaluate(points[i])[0]
        l0 = kde.evaluate(points[i]-peak_interval)[0]
        continue
    r1 = kde.evaluate(points[i]+seek_bin)[0]
    l1 = kde.evaluate(points[i]+seek_bin-peak_interval)[0]
    if r0 == l0:
        pp = points[i]
        break
    elif r1 == l0:
        pp = points[i] + seek_bin
        break
    elif r0 > l0 and r1 < l1:
        pp = points[i] + seek_bin/2.0
        break
    else:

        r0, l0 = r1, l1
# 准确求交点的x值
def f(x):  # 计算误差函数
    if x<2 or x>2+peak_interval:
        return np.inf
    else:
        return kde.evaluate(x) - kde.evaluate(x-peak_interval)
pp=scipy.optimize.leastsq(f,2) # 传递误差函数和待确定参数的初始值

# 计算各累积分布值
func = lambda x,s: kde.kernel.density(s,x)
cdf1 = scipy.integrate.quad(func, -np.inf, pp, args=kde.endog)[0]
cdf2 = scipy.integrate.quad(func, -np.inf, pp-peak_interval, args=kde.endog)[0]
cdf_inter = 1 - cdf1 + cdf2 # 交集的面积，及概率
```


### 33. 将pandas数据和matplotlib绘图嵌入html文件

* [python 实现将 pandas 数据和 matplotlib 绘图嵌入 html 文件](https://blog.csdn.net/XnCSD/article/details/79231205)

**实现原理**

python 的 lxml 库的 etree 模块可以实现解析 HTML 代码并写入 html 文件。如下所示：

```
from lxml import etree
root = """
<title>lxml example</title>
<h1>Hello lxml!</h1>
"""
html = etree.HTML(root)
tree = etree.ElementTree(html)
tree.write('hellolxml.html')
```

pandas 的 DataFrame 数据，可直接调用 df.to_html() 函数将 DataFrame 数据转为 HTML 代码字符串。

从 HTML 文件中可以发现，内嵌的图片是以 base64 代码的形式嵌入的。具体形式为 
`<img src="data:image/png;base64,iVBORw...>`。后面的 iVBORw…即为图像的 Base64 编码信息。
故而只需将图像转为 base64 代码即可将图像嵌入 HTML 代码字符串中。python 的 base64 模块可
以实现将二进制文件转为 base64 编码，而 matplotlib 的 pyplot.savefig() 函数可以将绘图窗口
保存为二进制文件格式。

**python 代码实现**

最终便可使用 python 实现将将 pandas 的 DataFrame 数据以及 matplotlib 绘图的图像保存为 HTML
 文件，代码如下。（以下代码基于 python 3.6 实现的。）

```
# 导入所需模块
import pandas as pd
import matplotlib.pyplot as plt
from io import BytesIO
from lxml import etree
import base64
import urllib


# 获取数据集，用 urllib 库下载 iris 数据集作为示例
url = "http://aima.cs.berkeley.edu/data/iris.csv"
setl = urllib.request.Request(url)
iris_p = urllib.request.urlopen(setl)
iris = pd.read_csv(iris_p, sep=',',decimal='.',header=None, names=['Sepal_Length','Sepal_Width','Petal_Length','Petal_Width','Species'])

# pandas 的 DataFrame 数据直接装换为 html 代码字符串
iris_des = """<h1>Iris Describe Stastic</h1>"""+iris.describe().T.to_html()

# matplotlib 任意绘制一张图
fig,axes = plt.subplots(1,4,sharey = True)
for n in range(4):
    axes[n].hist( iris.iloc[:,n],bins = 15,color = 'b',alpha = 0.5,rwidth= 0.8 )
    axes[n].set_xlabel(iris.columns[n])
plt.subplots_adjust(wspace = 0)
# figure 保存为二进制文件
buffer = BytesIO()
plt.savefig(buffer)  
plot_data = buffer.getvalue()

# 图像数据转化为 HTML 格式
imb = base64.b64encode(plot_data)  
#imb = plot_data.encode('base64')   # 对于 Python 2.7可用 
ims = imb.decode()
imd = "data:image/png;base64,"+ims
iris_im = """<h1>Iris Figure</h1>  """ + """<img src="%s">""" % imd   

root = "<title>Iris Dataset</title>"
root = root + iris_des + iris_im  #将多个 html 格式的字符串连接起来

# lxml 库的 etree 解析字符串为 html 代码，并写入文件
html = etree.HTML(root)
tree = etree.ElementTree(html)
tree.write('iris.html')

# 最后使用默认浏览器打开 html 文件
import webbrowser
webbrowser.open('iris.html',new = 1)
```


### 34. python读写excel文件


python处理excel已经有大量包，主流代表有：

* xlwings：简单强大，可替代VBA，**只能在windows和macOS系统上使用**
* openpyxl：简单易用，功能广泛  **所有系统均可使用，但速度较慢**
* pandas：使用需要结合其他库，数据处理是pandas立身之本  
* win32com：不仅仅是excel，可以处理office;不过它相当于是 windows COM 的封装，新手使用起来略有些痛苦。
* Xlsxwriter：丰富多样的特性，缺点是不能打开/修改已有文件，意味着使用 xlsxwriter 需要从零开始。
* DataNitro：作为插件内嵌到excel中，可替代VBA，在excel中优雅的使用python
* xlutils：结合xlrd/xlwt，老牌python包，需要注意的是你必须同时安装这三个库

各包速度和功能对比：

![](https://images2017.cnblogs.com/blog/846822/201709/846822-20170922180351790-690554626.png)


**1. openpyxl的使用**

* **[Python_Openpyxl 浅谈（最全总结 足够初次使用）](https://blog.csdn.net/weixin_43094965/article/details/82226263)**
* [python操作Excel模块openpyxl](https://www.cnblogs.com/zeke-python-road/p/8986318.html)
* [python 读写 Excel文件](https://www.cnblogs.com/shaosks/p/6098282.html)

```
import openpyxl

xlsxs = ["test"+str(i)+".xlsx" for i in range(1,4)]
outfile = "a.xlsx"

def add_sheet(in_xlsx, x, outfile):
     xlsx = openpyxl.load_workbook(in_xlsx)
     osheet = x.create_sheet(in_xlsx.split(".")[0])
     sheet = xlsx["Sheet1"]
     nrows = sheet.max_row
     ncols = sheet.max_column
     for i in range(nrows):
         for j in range(ncols):
             osheet.cell(None, i+1, j+1, sheet.cell(None, i+1, j+1).value)
     x.save(outfile)

xo = openpyxl.Workbook()

for xlsx in xlsxs:
	add_sheet(xlsx, xo, outfile)

sheet = xo.get_sheet_by_name("Sheet")
xo.remove(sheet)
xo.save(outfile)
xo.close()
```



**2. xlwings的使用**

* [翻译：xlwings快速入门](https://www.jianshu.com/p/a9d95691c89f)
* [插上翅膀，让Excel飞起来——xlwings（一）](https://www.jianshu.com/p/e21894fc5501)
* [插上翅膀，让Excel飞起来——xlwings（二）](https://www.jianshu.com/p/b534e0d465f7)
* [插上翅膀，让Excel飞起来——xlwings（三）](https://www.jianshu.com/p/de7efe591c12)
* [插上翅膀，让Excel飞起来——xlwings（四）](https://www.jianshu.com/p/7d6f53e3e6e9)


### 35. 编译好的包

[Unofficial Windows Binaries for Python Extension Packages](https://www.lfd.uci.edu/~gohlke/pythonlibs/)


</br>

## 高级

### 1. 装饰器（Decorator）

**基础装饰器**

[简单 12 步理解 Python 装饰器](http://python.jobbole.com/85056/)

>使用函数来实现装饰器

```
def logger(func):
      def inner(*args, **kwargs): #1
            print "Arguments were: %s, %s" % (args, kwargs)
            return func(*args, **kwargs) #2
     return inner

@logger
def foo1(x, y=1):
      return x * y

@logger
def foo2():
       return 2

foo1(5, 4)
foo1(1)
foo2()
```
结果：
```
Arguments were: (5, 4), {}
20

Arguments were: (1,), {}
1

Arguments were: (), {}
2
```

**带参数的装饰器**

[Decorators I: Introduction to Python Decorators](http://www.artima.com/weblogs/viewpost.jsp?thread=240808)

[Python Decorators II: Decorator Arguments](http://www.artima.com/weblogs/viewpost.jsp?thread=240845)

[更多装饰器的例子](https://wiki.python.org/moin/PythonDecoratorLibrary)

>分别使用对象和函数来实现带参数的装饰器

```
class qsub(object):
    def __init__(self, shfile, **kwargs):
        self.shfile = shfile
        self.kwargs = kwargs

    def __call__(self, func):
        def wrapper(*args, **kwargs):
            cmd = func(*args, **kwargs)
            with open(self.shfile, "w") as f:
                f.write(cmd)
            self.qsubOrDie(self.shfile, **self.kwargs)
        return wrapper

    def qsubOrDie(self, shfile, **kwargs):
        print "I will use the parameter {} to qsub the {}.".format(kwargs, shfile)

@qsub(shfile="temp.sh", queue="general.q", maxproc=50, reqsub=True)
def sleep(time=10):
    cmd = "I will sleep {} s.\n".format(time)
    return cmd

sleep(10)
```
结果：
```
I will use the parameter {'reqsub': True, 'maxproc': 50, 'queue': 'general.q'} to qsub the temp.sh.
```

还可以使用函数来实现：

```
def qsubOrDie(shfile, **kwargs):
    print "I will use the parameter {} to qsub the {}.".format(kwargs, shfile)

def qsub(shfile, **qsub_kwargs):
    def wrap(func):
        def wrapper(*args, **kwargs):
            cmd = func(*args, **kwargs)
            with open(shfile, "w") as f:
                f.write(cmd)
            qsubOrDie(shfile, **qsub_kwargs)
        return wrapper
    return wrap

@qsub(shfile="temp.sh", queue="general.q", maxproc=50, reqsub=True)
def sleep(time=10):
    cmd = "I will sleep {} s.\n".format(time)
    return cmd 

sleep(10)
```


**可带参数也可不带参数的装饰器**

[廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001386819879946007bbf6ad052463ab18034f0254bf355000#0)

能否写出一个`@log`的decorator，使它既支持

```
@log 
def f():
    pass
```
又支持：
```
@log('execute') 
def f():
    pass
```

可以这样写：

```
import functools
from types import FunctionType
def log(*params, **kwparams):
    if params and callable(params[0]):
    # 或者
    # if params and type(params[0]) == FunctionType:
        func = params[0]
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            call_result = func(*args, **kwargs)
            return call_result
        return wrapper
    else:
        def decorator(func):
            @functools.wraps(func)
            def wrapper(*args, **kwargs):
                call_result = func(*args, **kwargs)
                return call_result
            return wrapper
        return decorator
```

这样就可以调用：

```
@log
@log()
@log("xxx")
```
参考：[Python怎么将两个功能相同的装饰器高阶函数，一个带参数一个不带参数的合并成一个装饰器？请前辈指点一二，十分感谢？](https://segmentfault.com/q/1010000007149687)



**装饰器的深入理解**

```
def before(func):
    print "callback before"
    def decorator(*args, **kwargs):
        print "add <before>"
        f = func(*args, **kwargs)
        print "<before>"+f
        return "<before>"+f
    return decorator

def after(func):
    print "callback after"
    def decorator(*args, **kwargs):
        print "add </after>"
        f = func(*args, **kwargs)
        print f+"</after>"
        return f+"</after>"
    return decorator

@argument
@after
def hello():
    return "hello world!"
```

返回的结果是什么？？？

```
callback after
callback before
add <before>
add </after>
hello world!</after>
<before>hello world!</after>
```

和我们想的不一样？为什么是这个结果呢？

1. after先装饰hello，  所以先输出："callback after"， 然后返回after_decorator(hello)函数
2. before再装饰after装饰过的hello, 所以再输出："callback before"， 然后返回before_decorator(after_decorator(hello))函数
3. 调用before_decorator(after_decorator(hello))()函数，所以接着输出："add <before>"
4. 然后调用after_decorator(hello)()函数， 再接着输出："add </after>"
5. 最后调用hello()函数， 返回"hello world!"
6. after_decorator(hello)()函数获得了hello()函数的返回值，进行修饰，所以输出： "hello world!</after>"
7. before_decorator(after_decorator(hello))()函数获得了after_decorator(hello)()函数修饰后的结果，再进行修饰，所以输出："<before>hello world!</after>"




### 2. 回调函数

从查看pyspider源码知道的回调函数


### 3. 魔法方法

[Python的魔法方法](http://blog.csdn.net/wangbowj123/article/details/76910743)

[Python魔法方法指南](https://zhuanlan.zhihu.com/p/26488074?refer=passer)

[Python的魔法方法](https://www.cnblogs.com/A-FM/p/5678231.html)

**__get__、__getattr__、__getitem__、__getattribute__之间的差异与联系**

[python总结(五)：__get__、__getattr__、__getitem__、__getattribute__之间的差异与联系](http://blog.csdn.net/yiifaa/article/details/78068962)

python的一切数据都是对象，包括函数、基本数据类型、自定义数据类型等等，这其中最复杂的就是对象内部存储的数据结构(引用)，包括类属性、数据描述符、实例属性及非数据描述符，不仅它们的优先级不一样，而且它们的回调函数也存在很大的差异，这也是本文需要阐述的地方。

如果以前有过Javascript的编程经验，初上Python肯定会对“.”运算符与“[]”之间的差异难以理解，它们不仅不能替换，而且完全不相关，如下：

```
mem = {'username': 'yiifaa'} 
# 无法通过.运算符进行计算 
mem.username 
# 声明String 
name = str('yiifaa') 
# 无法使用“[]”运算符 
name['upper']
```
***为实例添加“[]”运算符支持***

这也是“_ getattribute_”与“_ getitem_”的最大差异，示例如下： 

1. <font color="red">“_ getattribute_”只适用于所有的“.”运算符； </font>
2. <font color="red"> “_ getitem_”只适用于所有的“[]”运算符；</font>

```
class Employee(object):

    def __init__(self, username, age):
        self.username = username
        self.age = age

    def __getattribute__(self, attr):
        return super(Employee, self).__getattribute__(attr)

    def __getitem__(self, attr):
        return super(Employee, self).__getattribute__(attr)

em = Employee('yiifaa', 32) 
print em.username 
#   现在支持“[]”运算符 
print em['username']
```

通过实现“_ getitem_”回调接口，现在Employee可以支持“[]”运算符。

***避免语法错误***

在对象属性的调用中，如果没有调用了不存在的属性，则Python解释器会报错，如下：
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module> 
AttributeError: 'str' object has no attribute 'length'
```

通过覆盖实现“_ getattr_”回调接口可以解决此问题，如下：

```
#   直接返回空对象，将此方法添加到类Employee的声明中 
def __getattr__(self, attr):
    return None 
 # 现在调用不存在的属性也不会报错 
print em.company
```

那“_ getattribute_”与“_ getattr_”的最大差异在于： 

1. <font color="red">无论调用对象的什么属性，包括不存在的属性，都会首先调用“_ getattribute_”方法； </font>
2. <font color="red">只有找不到对象的属性时，才会调用“_ getattr_”方法；</font>

***将对象作为数据[描述符](http://wiki.jikexueyuan.com/project/the-python-study-notes-second-edition/descriptor.html)***

这就是“_ get_”的作用了，将整个对象都作为数据描述符，但是请记住，要想““_ get_””作为数据描述符，那么此对象只能作为类属性，作为实例属性则无效，如下：

```
class Dept(object):

      def __init__(self, name):
          self.name = name

      # target是拥有此属性的对象
      def __get__(self, target, type=None):
        # 默认返回self与obj都可以
        return 'Dept' 

 class Company(object):
    #   一定要作为类属性，作为实例属性无效
    dept = Dept('organ') 

 # 现在的测试结果 
x = Company() 
#   返回True 
print type(x.dept) == str
```

***获取对象属性数据的三种方法***

对象的所有属性都存储在“_ dict_”中（启用了“_ slots_”除外），所以访问对象的属性数据有如下三种方法：

```
print yiifaa.name 
print yiifaa.__dict__['name'] 
print getattr(yiifaa, 'name')
```

***结论***

每个以“__ get”为前缀的方法都是获取对象内部数据的钩子，但名称不一样，用途也存在较大的差异，只有在实践中理解它们，才能真正掌握它们的用法。

***pyspider实例***

```
class ObjectDict(dict):
    """ 
    Object like dict, every dict[key] can visite by dict.key

    If dict[key] is `Get`, calculate it's value.
    """

    def __getattr__(self, name):
        ret = self.__getitem__(name)
        if hasattr(ret, '__get__'):
            return ret.__get__(self, ObjectDict)
        return ret 
```

</br>

**__get__; __set__; __delete__**

[描述符](http://wiki.jikexueyuan.com/project/the-python-study-notes-second-edition/descriptor.html)


**__str__, __repr__, str(), repr()**

[Python中str()与__str__、repr()与__repr__、eval()、__unicode__的关系与区别](http://blog.csdn.net/foryouslgme/article/details/51658057)

首先, 先弄清楚str()与__str__、repr()与__repr__ 的区别，str()与repr()都是python中的内置函数，是直接用来格式化字符串的函数。而__str__与__repr__ 是在类(对象)中对类(对象)本身进行字符串处理。

其次，需要弄清楚str与repr之间的区别。

【str】: 

    返回一个可以用来表示对象的可打印的友好的字符串

    对字符串，返回本身。 

    没有参数，则返回空字符串 

    对类，可通过__str__() 成员控制其行为。该成员不存在，则使用其 __repr__() 成员。

    与 repr 区别：不总是尝试生成一个传给 eval 的字符串，其目标是可打印字符串。

【repr】：

    返回一个可以用来表示对象的可打印字符串

    首先，尝试生成这样一个字符串，将其传给 eval()可重新生成同样的对象 

    否则，生成用尖括号包住的字符串，包含类型名和额外的信息(比如地址) 

    一个类(class)可以通过 __repr__() 成员来控制repr()函数作用在其实例上时的行为。

示例：

```
#test2.py 
class A(object):
    def __str__(self):
        return "__str__"
    def __repr__(self):
        return "__repr__" 

 a = A() 
b = A
```
```
>>> import test2 
>>> test2.a 
__repr__ 
>>> print(test2.a) 
__str__ 
>>> test2.b 
<class 'test2.A'> 
>>> print(test2.b) 
<class 'test2.A'>
```

**python 将对象设置为可迭代有两种实现方式**

python 将对象设置为可迭代有两种实现方式：

1. 实现  __getitem__(self)

```
class Library(object):
    def __init__(self):
        self.value=['a','b','c','d','e']

    def __getitem__(self, i):
        if i>=len(self.value):
            raise IndexError("out of index")
        value=self.value[i]
        return value
```

调用的时候，系统默认从0 开始传入，并使得i=i+1

2. 实现 __iter__(self),next(self)

```
class Library2(object):
    def __init__(self):
        self.value=['a','b','c','d','e']
        self.i=-1

    def __iter__(self):
        return self

    def next(self):
        self.i += 1
        if self.i>=len(self.value):
            raise StopIteration
        return self.value[self.i]
        
test=Library2()
print test.next()
print test.next()
```

在这里可以像生成器一样使用


### 4. 工厂函数

今天在学习python时看到了一段代码甚是震惊. 大家都说python 是一门动态语言,刚开始我还没有很深刻的认识到什么叫
动态语言,但是看到这段代码后终于明白了,废话不多说,上代码:

```
def maker(N):
    def action(X):
        return X ** N
    return action
```

这是一段很简单的代码, 看看运行后的结果:

```
def maker(N):
    def action(X):
        return X ** N
    return action
 
f = maker(2)
 
f(3) #结果是9
 
g = maker(3)
g(3) #结果是27
```

结果我写在后面了, 可以看到每次maker()后都产生了一个新的函数对象,这么简单的一段代码这实现了工厂函数的功能真
是让我大开眼界.

PS:到现在为此,我对python的理解是:它类似于String中控制反转的道理,原来许多的工作是由程序员来完成,但现在由编译
器来完成.连对象的类型也是由编译器来识别,所以大大简化了程序员的工作.



### 5. 多进程（multiprocessing和subprocess）

[廖雪峰的官方网站-多进程](
https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001431927781401bb47ccf187b24c3b955157bb12c5882d000)

[python的threading和multiprocessing模块初探](https://blog.csdn.net/mydear_11000/article/details/52767976)

多进程

要让Python程序实现多进程（multiprocessing），我们先了解操作系统的相关知识。
Unix/Linux操作系统提供了一个`fork()`系统调用，它非常特殊。普通的函数调用，调用一次，返回一次，但是`fork()`调用一次，返回两次，因为操作系统自动把当前进程（称为父进程）复制了一份（称为子进程），然后，分别在父进程和子进程内返回。

子进程永远返回0，而父进程返回子进程的ID。这样做的理由是，一个父进程可以fork出很多子进程，所以，父进程要记下每个子进程的ID，而子进程只需要调用getppid()就可以拿到父进程的ID。

Python的os模块封装了常见的系统调用，其中就包括`fork`，可以在Python程序中轻松创建子进程：

```
import os 
print('Process (%s) start...' % os.getpid()) 
# Only works on Unix/Linux/Mac: 
pid = os.fork() 
if pid == 0:
    print('I am child process (%s) and my parent is %s.' % (os.getpid(), os.getppid())) 
else:
    print('I (%s) just created a child process (%s).' % (os.getpid(), pid))
```

运行结果如下：

```
Process (876) start... 
I (876) just created a child process (877). 
I am child process (877) and my parent is 876.
```

由于Windows没有`fork`调用，上面的代码在Windows上无法运行。由于Mac系统是基于BSD（Unix的一种）内核，所以，在Mac下运行是没有问题的，推荐大家用Mac学Python！

有了`fork`调用，一个进程在接到新任务时就可以复制出一个子进程来处理新任务，常见的Apache服务器就是由父进程监听端口，每当有新的http请求时，就fork出子进程来处理新的http请求。

**multiprocessing**

如果你打算编写多进程的服务程序，Unix/Linux无疑是正确的选择。由于Windows没有fork调用，难道在Windows上无法用Python编写多进程的程序？

由于Python是跨平台的，自然也应该提供一个跨平台的多进程支持。`multiprocessing`模块就是跨平台版本的多进程模块。

`multiprocessing`模块提供了一个`Process`类来代表一个进程对象，下面的例子演示了启动一个子进程并等待其结束：

```
from multiprocessing import Process
import os

# 子进程要执行的代码
def run_proc(name):
    print('Run child process %s (%s)...' % (name, os.getpid()))

if __name__=='__main__':
    print('Parent process %s.' % os.getpid())
    p = Process(target=run_proc, args=('test',))
    print('Child process will start.')
    p.start()
    p.join()
    print('Child process end.')
```

执行结果如下：

```
Parent process 928.
Process will start.
Run child process test (929)...
Process end.
```

创建子进程时，只需要传入一个执行函数和函数的参数，创建一个`Process`实例，用`start()`方法启动，这样创建进程比`fork()`还要简单。

`join()`方法可以等待子进程结束后再继续往下运行，通常用于进程间的同步。

**Pool**

* [multiprocessing Pool的异常处理问题](https://blog.csdn.net/hedongho/article/details/79139606)
* [multiprocessing解析(二):Pool解析](https://blog.csdn.net/liuxingen/article/details/72605343)

如果要启动大量的子进程，可以用进程池的方式批量创建子进程：

```
from multiprocessing import Pool
import os, time, random

def long_time_task(name):
    print('Run task %s (%s)...' % (name, os.getpid()))
    start = time.time()
    time.sleep(random.random() * 3)
    end = time.time()
    print('Task %s runs %0.2f seconds.' % (name, (end - start)))

if __name__=='__main__':
    print('Parent process %s.' % os.getpid())
    p = Pool(4)
    for i in range(5):
        p.apply_async(long_time_task, args=(i,))
    print('Waiting for all subprocesses done...')
    p.close()
    p.join()
    print('All subprocesses done.')
```

执行结果如下：

```
Parent process 669.
Waiting for all subprocesses done...
Run task 0 (671)...
Run task 1 (672)...
Run task 2 (673)...
Run task 3 (674)...
Task 2 runs 0.14 seconds.
Run task 4 (673)...
Task 1 runs 0.27 seconds. 
Task 3 runs 0.86 seconds.
Task 0 runs 1.41 seconds.
Task 4 runs 1.91 seconds.
All subprocesses done.
```

代码解读：

对`Pool`对象调用`join()`方法会等待所有子进程执行完毕，调用`join()`之前必须先调用`close()`，调用`close()`之后就不能继续添加新的`Process`了。

请注意输出的结果，task 0，1，2，3是立刻执行的，而task 4要等待前面某个task完成后才执行，这是因为Pool的默认大小在我的电脑上是4，因此，最多同时执行4个进程。这是Pool有意设计的限制，并不是操作系统的限制。如果改成：

p = Pool(5) 
就可以同时跑5个进程。

由于Pool的默认大小是CPU的核数，如果你不幸拥有8核CPU，你要提交至少9个子进程才能看到上面的等待效果。

**子进程**

很多时候，子进程并不是自身，而是一个外部进程。我们创建了子进程后，还需要控制子进程的输入和输出。

`subprocess`模块可以让我们非常方便地启动一个子进程，然后控制其输入和输出。

下面的例子演示了如何在Python代码中运行命令nslookup www.python.org，这和命令行直接运行的效果是一样的：

```
import subprocess 

print('$ nslookup www.python.org')
r = subprocess.call(['nslookup', 'www.python.org'])
print('Exit code:', r)
```

运行结果：

```
$ nslookup www.python.org
Server:        192.168.19.4
Address:    192.168.19.4#53

Non-authoritative answer:
www.python.org    canonical name = python.map.fastly.net.
Name:    python.map.fastly.net
Address: 199.27.79.223

Exit code: 0
```

如果子进程还需要输入，则可以通过`communicate()`方法输入：

```
import subprocess

print('$ nslookup')
p = subprocess.Popen(['nslookup'], stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
output, err = p.communicate(b'set q=mx\npython.org\nexit\n')
print(output.decode('utf-8'))
print('Exit code:', p.returncode)
```

上面的代码相当于在命令行执行命令`nslookup`，然后手动输入：

```
set q=mx
python.org
exit
```

运行结果如下：

```
$ nslookup
Server:        192.168.19.4
Address:    192.168.19.4#53

Non-authoritative answer:
python.org    mail exchanger = 50 mail.python.org.
Authoritative answers can be found from:
mail.python.org    internet address = 82.94.164.166
mail.python.org    has AAAA address 2001:888:2000:d::a6

Exit code: 0
```

**进程间通信**

Process之间肯定是需要通信的，操作系统提供了很多机制来实现进程间的通信。Python的`multiprocessing`模块包装了底层的机制，提供
了`Queue`、`Pipes`等多种方式来交换数据。

我们以`Queue`为例，在父进程中创建两个子进程，一个往`Queue`里写数据，一个从`Queue`里读数据：

```
from multiprocessing import Process, Queue
import os, time, random

# 写数据进程执行的代码:
def write(q):
    print('Process to write: %s' % os.getpid())
    for value in ['A', 'B', 'C']:
        print('Put %s to queue...' % value)
        q.put(value)
        time.sleep(random.random())

# 读数据进程执行的代码:
def read(q):
    print('Process to read: %s' % os.getpid())
    while True:
        value = q.get(True)
        print('Get %s from queue.' % value)

if __name__=='__main__':
    # 父进程创建Queue，并传给各个子进程：
    q = Queue()
    pw = Process(target=write, args=(q,))
    pr = Process(target=read, args=(q,))
    # 启动子进程pw，写入:
    pw.start()
    # 启动子进程pr，读取:
    pr.start()
    # 等待pw结束:
    pw.join()
    # pr进程里是死循环，无法等待其结束，只能强行终止:
    pr.terminate()
```

运行结果如下：

```
Process to write: 50563
Put A to queue...
Process to read: 50564
Get A from queue.
Put B to queue...
Get B from queue.
Put C to queue...
Get C from queue.
```
在Unix/Linux下，`multiprocessing`模块封装了`fork()`调用，使我们不需要关注`fork()`的细节。由于Windows没有`fork`调用，因此，`multiprocessing`需要“模拟”出`fork`的效果，父进程所有Python对象都必须通过`pickle`序列化再传到子进程去，所有，如果`multiprocessing`在Windows下调用失败了，要先考虑是不是`pickle`失败了。

**小结**

在Unix/Linux下，可以使用`fork()`调用实现多进程。

要实现跨平台的多进程，可以使用`multiprocessing`模块。

进程间通信是通过`Queue`、`Pipes`等实现的。


**捕捉异常**

可以使用get()方法，或者使用logger捕捉。下面我们先看简单方法get：

```
from multiprocessing import Pool

def test(x):
    a = 1. / x
    return a

p = Pool(2)
result = []
for i in [2,0,1]:
    result.append(p.apply_async(test, args=(i,)))                                                                           
p.close()
p.join()

for i in result:
    try:
        print(i.get())
    except:
        raise

print("END")
```

结果为：
```
0.5
Traceback (most recent call last):
  File "test1.py", line 16, in <module>
    print(i.get())
  File "/share/public/software/python/2.7.14/lib/python2.7/multiprocessing/pool.py", line 572, in get
    raise self._value
ZeroDivisionError: integer division or modulo by zero
```

我们再看看logger捕捉异常：

```
import sys
import logging
from multiprocessing import Pool

logger = logging.getLogger("AppName")
formatter = logging.Formatter('%(asctime)s %(levelname)-8s: %(message)s')
console_handler = logging.StreamHandler(sys.stdout)
console_handler.formatter = formatter
logger.addHandler(console_handler)
logger.setLevel(logging.INFO)

def test(x):
    logger.info("process-{}".format(x))
    try:
        a = 1. / x
        return a
    except:
        logger.exception("process-{}".format(x))

p = Pool(2)

result = []
for i in [2,0,1]:
    result.append(p.apply_async(test, args=(i,)))
p.close()
p.join()

print("END")
```

结果为：

```
2018-11-16 11:22:09,956 INFO    : process-2
2018-11-16 11:22:09,957 INFO    : process-1
2018-11-16 11:22:09,957 INFO    : process-0
2018-11-16 11:22:09,957 ERROR   : process-0
Traceback (most recent call last):
  File "test2.py", line 15, in test
    a = 1. / x
ZeroDivisionError: float division by zero
END
```

请注意最后的"END", 这说明logging捕获到异常时，并不会使程序中断。我们可以对上述代码进行优化：

```
import sys
import logging
from multiprocessing import Pool

logger = logging.getLogger("AppName")
formatter = logging.Formatter('%(asctime)s %(levelname)-8s: %(message)s')
console_handler = logging.StreamHandler(sys.stdout)
console_handler.formatter = formatter
logger.addHandler(console_handler)
logger.setLevel(logging.INFO)

def test(x):
    logger.info("process-{}".format(x))
    try:
        a = 1. / x
        return a
    except:
        logger.exception("process-{}".format(x))
        raise

p = Pool(2)

result = []
for i in [2,0,1]:
    result.append(p.apply_async(test, args=(i,)))
p.close()
p.join()

for i in result:
	try:
		i.get()    #  主程序捕获不到logger.exception错误，但是能够捕获到下一句的raise
	except:
		exit(1)    #  虽然主程序捕获不到logger.exception错误，但logger已将错误打印输出，
		           #  此时我们不需要再raise一边错误，只需exit(1)退出就好

print("END")
```

结果为：

```
2018-11-16 11:22:09,956 INFO    : process-2
2018-11-16 11:22:09,957 INFO    : process-1
2018-11-16 11:22:09,957 INFO    : process-0
2018-11-16 11:22:09,957 ERROR   : process-0
Traceback (most recent call last):
  File "test2.py", line 15, in test
    a = 1. / x
ZeroDivisionError: float division by zero
END
```


**小心exit**

```
1  from multiprocessing import Pool
2
3  def test(i):
4     if i == 0:
5         exit(1)
6
7  p = Pool(3)
8  process = []
9
10 for i in range(4):
11    process.append(p.apply_async(test, args=(i,)))
12
13 p.close()
14 p.join()
15 print("multiprocess end!")
16
17 print("END")
```

请注意第5行的exit, 在第一个子进程中(i=0), 会执行exit，使主进程退出，导致其他子线程无法回收，而
成为僵尸进程。

针对这种情况，有两种解决方案：

1. 将exit改为raise，并在主进程中捕捉异常。
2. 通过消息，通知主进程关闭所有子进程后再退出。[multiprocessing.Process 产生的子进程如何正常退出？](http://bbs.chinaunix.net/thread-4133313-1-1.html)




### 6. 多线程

* [Python：使用threading模块实现多线程编程一[综述]](https://blog.csdn.net/bravezhe/article/details/8585437)
* [Python-threading并发操作](http://blog.csdn.net/y2701310012/article/details/40863145)


### 协程

* [Python异步IO之协程(一):从yield from到async的使用](https://blog.csdn.net/SL_World/article/details/86597738)
* [Python协程深入理解](https://www.cnblogs.com/zhaof/p/7631851.html)
* [异步协程太吊了！以亲测！简直完美，Python异步协程的葵花宝典！](https://blog.csdn.net/qq_42156420/article/details/81138062)
* [python3之协程](https://www.cnblogs.com/zhangxinqi/p/8337207.html)

### 7. 字符编码

* [浅析Python3中的bytes和str类型](https://www.cnblogs.com/chownjy/p/6625299.html)
* [Python中文字符的理解：str()、repr()、print](https://www.cnblogs.com/omg24/p/5048319.html)
* [python中文编码问题深入分析（二）：print打印中文异常及显示乱码问题分析与解决](https://www.cnblogs.com/litaozijin/p/6416133.html)
* [廖雪峰的官方网站-字符串和编码](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001431664106267f12e9bef7ee14cf6a8776a479bdec9b9000)
* [Python中的str与unicode处理方法](http://python.jobbole.com/81244/)
* [从原理上搞定编码-- Base64编码](http://www.cnblogs.com/chengxiaohui/articles/3951129.html) 


<font color="red">
**`变量`在`内存`中以`unicode`编码存储，但在`硬盘`、`网络传输`、`终端`等以`ascii`、`utf-8`、`gbk`等编码方式存储。**

比较难理解的是`print`，`print`是将`变量`在`终端`显示。

如果`变量`的类型是`str`，则操作系统直接将`变量`交付给`终端`进行显示；

如果`变量`的类型是`unicode`，则操作系统首先将`变量`编码成`str`类型的对象（编码方式取决于stdout的编码格式），然后再交由`终端`进行显示。在`终端`显示时，如果`str`类型的`变量`的编码方式和`终端`设置的编码方式不一致，很可能会出现乱码问题。

查看系统的默认编码，可以调用`sys.getdefaultencoing()`函数
</font>





python2.x中处理中文，是一件头疼的事情。网上写这方面的文章，测次不齐，而且都会有点错误，所以在这里打算自己总结一篇文章。
我也会在以后学习中，不断的修改此篇博客。

这里假设读者已有与编码相关的基础知识,本文不再再次介绍，包括什么是utf-8，什么是unicode，它们之间有什么关系。

**str与字节码**

```
s = "人生苦短"
```
s是个字符串，它本身存储的就是字节码。那么这个字节码是什么格式的？
如果这段代码是在解释器上输入的，那么这个s的格式就是解释器的编码格式，对于windows的cmd而言，就是gbk。
如果将段代码是保存后才执行的，比如存储为utf-8，那么在解释器载入这段程序的时候，就会将s初始化为utf-8编码。

**unicode与str**

unicode是一种编码标准，具体的实现标准可能是utf-8，utf-16，gbk ……

python 在内部使用两个字节来存储一个unicode，使用unicode对象而不是str的好处，就是unicode方便于跨平台。

你可以用如下两种方式定义一个unicode:

```
s1 = u"人生苦短"
s2 = unicode("人生苦短", "utf-8")
```

encode与decode

在python中的编码解码是这样的：

所以我们可以写这样的代码：

```
# -*- coding:utf-8 -*-
su = "人生苦短"
# ： su是一个utf-8格式的字节串
u  = s.decode("utf-8")
# ： s被解码为unicode对象，赋给u
sg = u.encode("gbk")
# ： u被编码为gbk格式的字节串，赋给sg
print sg
# 打印sg
```

但是事实情况要比这个复杂，比如看如下代码：

```
s = "人生苦短"
s.encode('gbk')
```

看！str也能编码，(事实上unicode对象也能解码，但是意义不大)

这样为什么可以？看上图的编码流程的箭头，你就能想到原理，当对str进行编码时，会先用默认编码将自己解码为unicode，然后在将unicode编码为你指定编码。

这就引出了python2.x中在处理中文时，大多数出现错误的原因所在：python的默认编码，defaultencoding是ascii

看这个例子：

```
# -*- coding: utf-8 -*-
s = "人生苦短"
s.encode('gbk')
```

上面的代码会报错，错误信息：UnicodeDecodeError: ‘ascii’ codec can’t decode byte ……

因为你没有指定defaultencoding,所以它其实在做这样的事情:

```
# -*- coding: utf-8 -*-
s = "人生苦短"
s.decode('ascii').encode('gbk')
```

**设置defaultencoding**

设置defaultencoding的代码如下：

```
reload(sys)
sys.setdefaultencoding('utf-8')
```

如果你在python中进行编码和解码的时候，不指定编码方式，那么python就会使用defaultencoding。

比如上一节例子中将str编码为另一种格式，就会使用defaultencoding。

```
s.encode("utf-8") 等价于 s.decode(defaultencoding).encode("utf-8")
```

再比如你使用str创建unicode对象时，如果不说明这个str的编码格式，那么程序也会使用defaultencoding。

```
u = unicode("人生苦短") 等价于 u = unicode("人生苦短",defaultencoding)
```

默认的defaultcoding：ascii是许多错误的原因，所以早早的设置defaultencoding是一个好习惯。

**文件头声明编码的作用**

这要感谢这篇博客关于python文件头部分知识的讲解。

顶部的:# -*- coding: utf-8 -*-目前看来有三个作用。

.如果代码中有中文注释，就需要此声明

.比较高级的编辑器（比如我的emacs），会根据头部声明，将此作为代码文件的格式。

.程序会通过头部声明，解码初始化 u”人生苦短”，这样的unicode对象，（所以头部声明和代码的存储格式要一致）


**关于requests库**

requests是一个很实用的Python HTTP客户端库，编写爬虫和测试服务器响应数据时经常会用到。

其中的Request对象在访问服务器后会返回一个Response对象，这个对象将返回的Http响应字节码保存到content属性中。

但是如果你访问另一个属性text时，会返回一个unicode对象，乱码问题就会常常发成在这里。

因为Response对象会通过另一个属性encoding来将字节码编码成unicode，而这个encoding属性居然是responses自己猜出来的。

所以要么你直接使用content(字节码)，要么记得把encoding设置正确，比如我获取了一段gbk编码的网页,就需要以下方法才能得到正确的unicode。

```
import requests
url = "http://xxx.xxx.xxx"
response = requests.get(url)
response.encoding = 'gbk'
 
print response.text
```

**不仅仅要原理，更要使用方法！**

***基本设置***

主动设置defaultencoding。（默认的是ascii）

代码文件的保存格式要与文件头部的# coding:xxx一致

如果是中文，程序内部尽量使用unicode，而不用str

***关于打印***

你在打印str的时候，实际就是直接将字节流发送给shell。如果你的字节流编码格式与shell的编码格式不相同，就会乱码。
而你在打印unicode的时候，系统自动将其编码为shell的编码格式，是不会出现乱码的。

***程序内外要统一***

如果说程序内部要保证只用unicode，那么在从外部读如字节流的时候，一定要将这些字节流转化为unicode，在后面的代码中去处理unicode，而不是str。

```
with open("test") as f:
    for i in f:
        # 将读入的utf-8字节流进行解码
        u = i.decode('utf-8')
        ....
```

如果把连接程序内外的这段数据流比喻成通道的的话，那么与其将通道开为字节流，读入后进行解码，不如直接将通道开为unicode的。

```
# 使用codecs直接开unicode通道
file = codecs.open("test", "r", "utf-8")
for i in file:
    print type(i)
    # i的类型是unicode的
```

所以python处理中文编码问题的关键是你要清晰的明白，自己在干什么，打算读入什么格式的编码，声明的的这些字节是什么格式的，str到unicode是如何转换的，str的一种编码到另一种编码又是如何进行的。 还有，你不能把问题变得混乱，要自己主动去维护一种统一。

**自我总结**

```
>>> x = u"汉字"
>>> y = "汉字"
>>> x
u'\u6c49\u5b57'  # unicode编码标准
>>> y
'\xe6\xb1\x89\xe5\xad\x97'  # 字节码
>>> type(x)
unicode
>>> type(y)
str
>>> y.decode("utf-8")
u'\u6c49\u5b57'
>>> x.encode("utf-8")
'\xe6\xb1\x89\xe5\xad\x97'

>>> z = "\u6c49\u5b57"
>>> z
'\\u6c49\\u5b57'
>>> type(z)
str
>>> z.decode("unicode_escape")
u'\u6c49\u5b57'
>>> a = u'\xe6\x8a\xa5\xe8\xa1\xa8'
>>> print a
æ<8a>¥è¡¨ 
>>> print a.encode("raw_unicode_escape")
报表 

# 将字符串转成二进制
bytes(s, encoding = "utf8") # 法1
str.encode(s)               # 法2

#将二进制转成字符串  
 str(b, encoding = "utf-8") # 法1
 bytes.decode(b)            # 法2

```

<font color="blue">**将字节码类字符串转化为正确的输出**</font>

```
>>> x = "\xe4\xb8\xad\xe5\x9b\xbd"
>>> print unicode(x, "gbk")
拒绝访问。
>>> print unicode(x, "utf-8")
UnicodeDecodeError                        Traceback (most recent call last)
<ipython-input-428-8770cff73855> in <module>()
----> 1 print unicode('\xbe\xdc\xbe\xf8\xb7\xc3\xce\xca\xa1\xa3','utf-8')

UnicodeDecodeError: 'utf8' codec can't decode byte 0xbe in position 0: invalid start byte
>>>
>>> y = "\\u8bc4\\u4ef7\\u7ebf\\u6027\\u6a21\\u578b"
>>> print y.decode("unicode-escape")
评价线性模型
```

**将8进制转换成中文字符**

```
import chardet

a = b"\345\260\274\345\217\244\346\213\211\346\226\257\350\265\265\345\233\233"
# 如果是python2.7，应写成：
# a = "\345\260\274\345\217\244\346\213\211\346\226\257\350\265\265\345\233\233" (少了b)
# 判断当前字符串的格式（编码类型）
fencoding = chardet.detect(a) 
# {'confidence': 0.99, 'encoding': 'utf-8', 'language': ''}

# 编码类型为打印出来的fencoding编码类型
a = a.decode('utf-8')
print(a)
```

来点有些难度的，现有如下乱码字符：

\xe4\xbd\xa0\xe5\xa5\xbd\xef\xbc\x8c\xe9\xba\xbb\xe7\x83\xa6\xe6\x8e\xa7\xe5\x88\xb6
\xe4\xb8\x80\xe4\xb8\x8b\xe4\xbd\xa0\xe5\x9c\xa80\xe5\x8f\xb7\xe8\x8a\x82\xe7\x82\xb9
\xe8\xbf\x90\xe8\xa1\x8c\xe7\x9a\x84\xe7\xba\xbf\xe7\xa8\x8b\xe6\x95\xb0\xef\xbc\x8c0
\xe5\x8f\xb7\xe8\x8a\x82\xe7\x82\xb9\xe6\x9c\x89\xe5\x95\x86\xe4\xb8\x9a\xe6\xa0\xb7
\xe6\x9c\xac\xe5\x9c\xa8\xe8\xbf\x90\xe8\xa1\x8c\xef\xbc\x8c\xe5\xa6\x82\xe6\x9e\x9c
\xe5\x8f\xaf\xe4\xbb\xa5\xe7\x9a\x84\xe8\xaf\x9d\xef\xbc\x8c\xe8\xaf\xb7\xe6\x8d\xa2
\xe4\xb8\xaa\xe8\xae\xa1\xe7\xe5\x85\xb6\xe4\xbb\x96\xe7\x9a\x84\xe8\xae\xa1\xe7\xae
\x97\xe8\x8a\x82\xe7\x82\xb9

请将其翻译成中文。我们可以先用chardet试试

```
>>> import chardet

>>> a = b"\xe4\xbd\xa0\xe5\xa5\xbd\xef\xbc\x8c\xe9\xba\xbb\xe7\x83\xa6\xe6\x8e\xa7\xe5\x88
\xb6\xe4\xb8\x80\xe4\xb8\x8b\xe4\xbd\xa0\xe5\x9c\xa80\xe5\x8f\xb7\xe8\x8a\x82\xe7\x82
\xb9\xe8\xbf\x90\xe8\xa1\x8c\xe7\x9a\x84\xe7\xba\xbf\xe7\xa8\x8b\xe6\x95\xb0\xef\xbc
\x8c0\xe5\x8f\xb7\xe8\x8a\x82\xe7\x82\xb9\xe6\x9c\x89\xe5\x95\x86\xe4\xb8\x9a\xe6\xa0
\xb7\xe6\x9c\xac\xe5\x9c\xa8\xe8\xbf\x90\xe8\xa1\x8c\xef\xbc\x8c\xe5\xa6\x82\xe6\x9e
\x9c\xe5\x8f\xaf\xe4\xbb\xa5\xe7\x9a\x84\xe8\xaf\x9d\xef\xbc\x8c\xe8\xaf\xb7\xe6\x8d
\xa2\xe4\xb8\xaa\xe8\xae\xa1\xe7\xe5\x85\xb6\xe4\xbb\x96\xe7\x9a\x84\xe8\xae\xa1\xe7
\xae\x97\xe8\x8a\x82\xe7\x82\xb9"

>>> chardet.detect(a)
{'confidence': 0.3597696002270644,
 'encoding': 'windows-1251',
 'language': 'Russian'}

>>> a.decode("windows-1251")
'дЅ\xa0еҐЅпјЊйє»зѓ¦жЋ§е€¶дёЂдё‹дЅ\xa0ењЁ0еЏ·иЉ‚з‚№иїђиЎЊзљ„зєїзЁ‹ж•°пјЊ0еЏ·иЉ‚з‚
№жњ‰е•†дёљж\xa0·жњ¬ењЁиїђиЎЊпјЊе¦‚жћњеЏЇд»Ґзљ„иЇќпјЊиЇ·жЌўдёЄи®Ўзе…¶д»–зљ„и®Ўз®—иЉ‚з‚№'

# 发现为乱码，说明chardet识别的不对，其置信度也只有0.35
# 怎么办呢，我们可以试试常见的编码格式
# 先试试gbk
>>> a.decode("gbk")
---------------------------------------------------------------------------
UnicodeDecodeError                        Traceback (most recent call last)
<ipython-input-28-a12a1ac95270> in <module>()
----> 1 b.decode("gbk")
UnicodeDecodeError: 'gbk' codec can't decode byte 0xa8 in position 32: illegal multibyte sequence

# gbk编码不对，再试试utf-8
>>> a.decode("utf-8")
---------------------------------------------------------------------------
UnicodeDecodeError                        Traceback (most recent call last)
<ipython-input-29-2643b56e8e14> in <module>()
----> 1 b.decode("utf-8")
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe7 in position 134: invalid continuation byte

# 看来还不对，那接下来怎么办呢？别急，我们发现decode有error参数，再试试它：
>>> a.decode("gbk", error="ignore")
'浣犲ソ锛岄夯鐑︽帶鍒朵竴涓嬩綘鍦0鍙疯妭鐐硅繍琛岀殑绾跨▼鏁帮紝0鍙疯妭鐐规湁鍟
嗕笟鏍锋湰鍦ㄨ繍琛岋紝濡傛灉鍙浠ョ殑璇濓紝璇锋崲涓璁＄鍏朵粬鐨勮＄畻鑺傜偣'

# 没报错了，但是还是不对，我们再试试utf-8
>>> a.decode("utf-8", error="ignore")
'你好，麻烦控制一下你在0号节点运行的线程数，0号节点有商业样本在运行，如果可以的话，
请换个计其他的计算节点'

# 哈哈，这下正确了吧。
```


### 8. 内建函数

* `abs(x)`: abs()函数返回数字（可为普通型、长整型或浮点型）的绝对值。如果给出复数，返回值就是该复数的模.
* `apply(function,args[,keywords])`: apply()函数将args参数应用到function上。function参数必须是可调用对象（函数、方法或其他可调用对象）。args参数必须以序列形式给出。列表在应用之前被转换为元组。function对象在被调用时，将args列表的内容分别作为独立的参数看待。例如： apply(add,(1,3,4))等价于add(1,3,4). 在以列表或元组定义了一列参数，且需要将此列表参数分别作为个个独立参数使用的情况下，必须使用apply()函数。在要把变长参数列应用到已函数上时，apply()函数非常有用。可选项keywords参数应是个字典，字典的关键字是字符串。这些字符串在apply()函数的参数列末尾处给出，它们将被用作关键字参数。
* `buffer(object[,offset[,size]])`: 如果object对象支持缓存调用接口buffer()函数就为object对象创建一个新缓存。这样的对象包括字符串、数组和缓存。该新缓存通过使用从offset参数值开始知道该对象末尾的存储片段或从offset参数值开始直到size参数给出的尺寸为长度的存储片段来引用object对象。如果没给出任何选项参数，缓存区域就覆盖整个序列，最终得到的缓存对象是object对象数据的只读拷贝。缓存对象用于给某个对象类型创建一个更友好的接口。比如，字符串对象类型通用缓存对象而变得可用，允许逐个字节地访问字符串中的信息。
* `callable(object)`: callable()函数在object对象是可调用对象的情况下，返回真(true)；否则假(false)，可调用对象包括函数、方法、代码对象、类（在调用时返回新的实例）和已经定义‘调用’方法的类实例
* `chr(i)`: chr()函数返回与ASCII码i相匹配的一个单一字符串，如下例所示：`>>>print chr(72)+chr(101)+chr(108)+chr(111)`结果为`hello`.
chr()函数是ord()函数的反函数，其中ord()函数将字符串转换回ASCII整数码，参数i的取值应在0~255范围内。如果参数i的取值在此范围之外，将引发ValueError异常。
* `cmp(x,y)`: cmp()函数比较x和y这两个对象，且根据比较结果返回一个整数。如果xy，则返回正数。请注意，此函数特别用来比较数值大小，而不是任何引用关系，因而有下面的结果：
```
>>>a=99
>>>b=int('99')
>>>cmp(a,b)
0
```
* `coerce(x,y)`: coerce()函数返回一个元组，该元组由两个数值型参数组成。此函数将两个数值型参数转换为同一类型数字，其转换规则与算术转换规则一样。一下是两个例子：
```
>>>a=1
>>>b=1.2
>>>coerce(a,b)
(1.0,1.2)
>>>a=1+2j
>>>b=4.3e10
>>>coerce(a,b)
((1+2j),(43000000000+0j))
```
* `compile(string,filename,kind)`: compile()函数将string编译为代码对象，编译生成的代码对象接下来被exec语句执行，接着能利用eval()函数对其进行求值。filename参数应是代码从其中读出的文件名。如果内部生成文件名，filename参数值应是相应的标识符。kind参数指定string参数中所含代码的类别，有关kind可能取值的详细信息，请参见表8-1,举例如下： 
```
>>>a=compile(‘print “Hello World”’,’’,’single’)
>>>exec(a)
Hello World
>>>eval(a)
Hello World
``` 
由compile()函数编译的代码的类别
``` 
Kind取值 编译生成的代码
exec 语句序列 
eval 简单表达式
Single 简单交互语句
```
* `complex(real,[image])`: Complex()函数返回一个复数，其实部为real参数值。如果给出image参数的值，则虚部就为image；如果默认image参数，则虚部为0j。
* `delattr(object,name)`: delattr()函数在object对象许可时，删除object对象的name属性，此函数等价于如下语句: `del object.attr`,而delattr()函数允许利用编程方法定义来定义object和name参数，并不是在代码中显示指定。
* `dir([object])`: 当没有提供参数时，dir()函数列出在当前局部符号表中保存的名字，如下例所示：
```
>>>import sys
>>>dir(sys)
``` 
* `divmod(a,b)`: devmod()函数返回一个元组，该元组包含a除以b的商和余数，如下例所示：
```
>>>divmod(7,4)
(1,3)
``` 
对整数而言，返回值与a/b和a%b相同。如果给出的参数值是浮点数，则结果就是（q,a%b），其中：q通常是math.floor(a/b)，但是也可能比这小1，不管在什么情况下，q*b+a%b都非常逼近a；如果a%b是个非零值，则其正负号与b相同，并且有0<=abs(a%b) 
```
>>>divmod(3.75,1.125)
(3.0,0.375)
>>>divmod(4.99,1.001)
(4.0,0.98600000000000065)
>>>divmod(-3.5,1.1)
(-4.0,0.90000000000000036)
```
* `eval(expression[,global[,locals]])`: eval()函数将expression字符串作为python标准表达式进行分析并求值，返回expression字符串的值，当不可调用其他可选参数时，expression访问调用该函数的程序段的全局和局部对象。另一个选择是：以字典形式给出全局和局部符号表（参见后面部分对global()和local()函数的论述）。Eval()函数的返回值是被求职表达式的值，如下例所示： 
```
>>>a=99
>>>eval(‘divmod(a,7)’)
(14,1)
```
任何求职操作的语法错误，都将引发成异常. eval()函数还能用来编译诸如由complie()函数创建的代码对象，但仅当该代码对象用“eval”模式编译过后才可用eval()函数编译。要执行混合了语句和表达式的python任意代码，请使用exec语句或使用execfile()函数来动态地执行含有任意代码的文件。
* `execfile(file[,globals[,locals]])`: execfile()函数与exec语句等价，不同之处在于：execfile()函数执行文件中的语句，而exec语句处理字符串。其中globals和locals参数应是字典，该字典包含文件在执行期间有效的符号表；如果locals参数省略，则所有的引用都使用globals名称空间。如果两个可选参数都省略，文件就访问运行期间的当前符号表。
* `filter(function,list)`: filter()函数根据function参数返回的结果是否为真(true)来过滤list参数中的项，最后返回一个新列表，如下例所示：
```
a=[1,2,3, 4, 5,6,,7,8,9]
b=filter(lambda x:x>6,a)
print b
[7,8,9]
```
如果function参数值为None，就是用identity函数，list参数中的所有为假(false)的元素都被删除。
* `flaot(x)`: float()函数将x参数转换为浮点数，其中:x可以是字符串，也可以是数字。
* `getattr(object,name[,default])`: getattr()函数返回object的name属性值。在语法上，以下语句：`getattr(x,’myvalue’)`等价于`x.myvalue`. 如果name参数不存在，但给出defalut参数的值，则此函数就返回default参数值；否则引发AttributeError异常
* `globals()`: globals()函数返回一个表示当前全局符号表的字典。这个字典通常就是当前模块的字典。如果globals()函数是在一函数或方法中被调用，它就返回定义该函数或方法的模块的符号表，而不是调用此函数的模块的符号表。
* `hasattr(object,name)`: 如果object对象具有与name字符串相匹配的属性，hasattr()函数返回真(true)；否则返回0。
* `hash(object)`: hash()函数返回关于object对象的整数散列值。如任何两个对象比较起来是等价的，则它们的散列值是一样的。此函数不应用于可便对向上。
* `hex(x)`: hex()函数将一整数转换为十六进制字符串，该字符串是个有效的python表达式、
* `id(object)`: id()函数返回值为一个整数(或长整型整数)——该对象的“标识“——该标识在其对应对象的生命期内，确保是唯一的和恒定不变的。
* `input([prompt])`: input()函数与eval(raw_input(prompt))等价。
* `int(x,[radix])`: int()函数将使数字或字符串x转换为“普通”整数。如果给出radix参数的值，则radix参数值用作转换的基数，该参数应是2~36范围内的一个整数。
* `intern(string)`: intern()函数将string加入到保留字符串的表，返回值为保留的版本号。“保留字符串”通过指针可用，而不是一个纯的字符串；因此允许利用指针比较代替字符串比较来进行字典关键字的查找，这比通常的字符串比较方法功能有所改善。在python名称空间表和用于保留模块、类或实力属性的字典中使用的名字通常被保留用以加速脚本执行。保留字符串定义后不能被作为无用单元收集，所以必须注意在大字典关键字集上使用保留字符串将大大增加内存需求，即使字典关键字应急超出了作用域。
* `isinstance(object,class)`: isinstance()函数在object参数是class参数的一个实例时，返回真。函数值的确定服从普通继承法则和子类。如果object参数是在types模块中利用类型类定义的特殊类型的实例，也能用isinstance()函数来识别。如果class参数不是类，也不是类型对象，就引发TypeError异常
* `issubclass(class1,class2)`: 如果class1参数是class2参数的子类，issubclass()函数则返回真。类通常被认为是其自身的子类。若两个参数中任一个都不是类对象，则引发TypeError异常
* `len(s)`: len()函数返回一序列（字符串、元组或列表）或字典对象的长度
* `list(sequence)`: list()函数返回以列表。该列表的项及顺序与sequence参数的项及顺序相同，如下例所示：
* `locals()`: locals()函数返回表示当前局部符号表的字典
* `long(x)`: long()函数将字符串或数字转换为长整型数，对浮点数的转换遵循与int()相同的规则
* `map(function,list,…)`: map()函数将function运用到list中的每一项上，并返回新的列表，如下例所示：
```
>>>a=[1,2,3,4]
>>>map(lambda x:pow(x,2),a)
[1,4,9,16]
```
若提供附加的列表，则它们就被并行地提供给function。在后续无元素的列表增加None，直到所有参数列表达到相同的长度为止。如果function参数值为None，则假定为identify函数，将使map()函数返回删除所有为假的参数的list。如果function参数值为None，且给定多个列表参数，返回的列表由一个个元组组成，这些元组由函数中的每一个参数列表内相同对应位置上的参数组成，如下例所示：
``` 
>>>map(None,[1,2,3,4],[4,5,6,7])
[(1,4),(2,5),(3,6),(4,7)]
``` 
上例的结果与zip()函数产生的结果等价
* `max(s,[,args…])`: 当仅给定一个参数时，max()函数返回序列s的最大值。当给定一列参数时，max()函数返回给定参数的最大参数
* `min(s[,args…])`: 当仅给定一个参数时，min()函数返回序列s的最小值。当给定一列参数时，min()函数返回给定参数中的最小值。记住：多参数调用的序列不被遍历，每个列表参数作为一个整体进行比较，如：
``` 
min([1,2,3],[4,5,6])
返回
[1,2,3]
```
而不是通常所想的结果为1，要得到一个或多个列表中元素的最小值，可将所有列表连成一串，如下所示：
``` 
min([1,2,3]+[4,5,6])
```
* `oct(x)`: 该函数将整数转换为八进制字符串。其结果是个有效的python表达式，如下例所示：`>>>oct(2001)`:`'03721'`. 请注意，返回值通常是无符号数。这样致使oct(-1)在32位机器上产生’037777777777’的结果
* `open(filename[,mode[,bufsize]])`: open()函数通过使用mode和缓存bufsize类型来打开filename标识的文件。此函数返一文件对象. 其中mode与系统函数fopen()使用的模式相同。如果mode参数省略，其默认取值为r. 模式含义
```
r 打开用于读
w 打开用于写
a 打开用于附加(打开期间，文件位置自动移到文件末尾)
r+ 打开用于更新(读和写)
w+ 截断(或清空)文件，接着打开文件用于读写
a+ 打开文件用于读和写，并自动改变当前为止到文件尾. 当附加任何模式选项时，以二进制模式而不是文本模式，打开文件(这种模式
b 仅对windows、dos和其他一些操作系统有效，对Unix、MacOS和BeOS则不管选项为何值，以二进制模式对待所有文件)
```
open()函数的bufsize选项参数决定从文件中读取数据时所使用的缓存的大小，如果bufsize省略，就使用系统默认的缓存容量. bufsize值 说明
```
禁用缓存
行缓存
>1 使用大小近似为bufsize字符长度的缓存
<0 使用系统默认
``` 
* `ord(c)`: 该函数返回由一个字符c组成的字符串的ASCII码值或Unicode数字码。ord()函数是chr()函数和nuichr()函数的反函数
* `pow(x,y[,z])`: 该函数返回以x为底数以y为指数的幂值。如果给出z，该函数就计算x的y次幂值被z取模的值，这样的计算比利用：`pow(x,y)%z`
的效率更高. 提供给pow()函数的参数应是数值型，并且给定的类型决定返回值的类型。如果计算得出的数值不能用给定参数值的类型表示，则引发异常，比如，以下对pow()的调用将失败： `pow(2,-1)`, 但是`pow(2.0,-1)`是有效的
* `range([start,]stop[,step])`: 该函数返回数值列表，该数值列表从start开始，以step为步长，于stop之前结束。所有的数字都应列出，并且以普通整型数返回。如果step省略，则默认取1.如果start省略，则从0开始求值。如果以两个参数形式调用，则认作给定的参数是start和stop，如果要定义步长就必须给出全部的三个参数。下面对range()函数的调用使用了值为正数的步长step: `>>>range(5,25,5)`. 请注意，最后的数值是stop减去step，range()函数的返回值从小递增到大，趋近stop的值，但不包含stop这个值. 如果step的给定值是负数，range()函数的返回值从大递增到小，而不是递增，stop必须比stop小；否则返回的列表为空。下列说明了step取值为负数的运用情况：`>>>range(10,0,-1)`
* `raw_input([prompt])`: 该函数从sys.stdin接受原始输入并返回字符串。输入以换行符为结束，其中换行符在输入字符串返回给调用者之前被去除。如果给出prompt，末尾不含换行符的prompt就被写到sys.stdout中，并用作输入的提示，如下例所示：`>>>name=raw_input(‘Name?’)`. 如果已加载readline模块，则诸如行编辑和历史记录的特性在输入期间就得到支持
* `reduce(function,sequence[,initializer])`: 该函数一次应用function（支持两个函数）到sequence中的每个元素上，逐渐缩短整个语句直到为一个单一的值。举例，下面的语句模拟了算术运算符“！”：`reduce(lambda x,y:x*y,[1,2,3,4,5])`, 其结果如同执行以下计算一样：`（（（（1*2）*3）*4）*5）`, 结果等于120. 如果给出initializer参数值，则initializer参数值就被用作序列的第一个元素，如下列所示：`>>>reduce(lambda x,y:x*y,[1,2,3,4,5],10)`结果等于1200
* `reload(module)`: reload()函数将以前导入过的模块再加载一次。重新加载(reload)包括最初导入模块是应用的分析过程和初始化过程。这样就允许在不退出解释器的情况重新加载已更改的python模块。使用reload()函数的若干注意事项如下： 1.如果模块在语法上是正确的，但在初始化过程中失败，则导入过程不能正确地将模块的名字绑定到符号表中，这时，必须在模块能被重新加载之前使用import()函数加载该模块。2.重新加载的模块不删除最初旧版本在符号表中的登记项。对于有恒定名字的对象和函数，这当然不是问题；但是，若对一模块实体更改了名字，模块名在重新加载后仍保持在符号表中. 3.支持扩展模块(它依赖与内置的或所支持的动态加载的函数库)的重新加载，但可能是无目标的，并且确定可能导致失败，这完全依赖于动态加载的函数库的行为. 4.如果以模块利用from…import…方式从另一个模块导入对象，reload()函数不重定义导入的对象，可利用import…形式避免这个问题. 5.提供类的重新加载模块不影响所提供类的任何已存实例——已存实例将继续使用原来的方法定义；只有该类的新实例使用新格式。这个原则对派生类同样适用.
* `repr(object)`: repr()函数返回对象的字符串表示。这与将对象或属性适用单反引号(‘)的结果是一致的。返回的字符串产生一个对象，该对象的值与将object传递给eval()函数产生的值一样，如下例所示：
```
>>>dict={‘One’:1,’Two:2’,’Many’:{‘Many’:4,’ManyMany’:8}}
>>>repr(dict)
“{‘One’:1,’Many’:{‘Many’:4,’ManyMany’:8},’Two’:2}”
```
* `round(x[,n])`: round()函数返回浮点型参数x舍入到十进制小数点后n位的值，如下例所示：
```
>>>round(0.4)
0.0
>>>round(0.5)
1.0
>>>round(-0.5)
-1.0
>>>round(1985,-2)
2000.0
```
* `setattr(object,name,value)`: 该函数将object参数的name属性设置为value参数值。setattr()函数是getattr()函数的反函数，后者仅获得信息，以下语句：`setattr(myattr’,’new value’)`等价于`myobj.myattr=’new value’`. setattr()函数能用在这样的情况下：属性是通过name参数以编程方式命名，而不是显式地命名属性
* `slice([start,]stop,[,step])`: 该函数返回已序列切片(slice)对象，该对象表示由range(start,stop,step)指定的索引集。如果给出一个参数，此参数就作为stop参数值；如果给出两个参数，它们就作为start和stop的参数值；任何未给出参数值的参数默认取值为None。序列切片对象有3个属性(start,stop,和step)，这3个属性仅仅返回要提供给slice()函数的参数
* `str(object)`: 返回对象的一个字符串表示。这与repr()函数相似，唯一不同之处在于：此函数返回值设计为可打印字符串而不是与eval()函数相兼容的字符串 
* `tuple(object)`: tuple()函数返回一个元组，该元组的项及项的顺序与sequence参数完全一样，以下就是tuple()函数的举例：
* `type(object)`: 该函数返回object参数的类型。返回值是个如类型模块所描述一样的类型对象，举例如下：
* `unichr(i)`: 该函数返回代码是一个整型参数i的Unicode字符的Unicode字符串。此函数等价于前面论述的chr()函数。请注意，要将Unicode字符转换回其整数格式，可使用ord()函数；没有uniord()函数、如果给出的整数超出0~65535这个范围，则引发ValueError异常
* `unicode(string[,encoding[,errors]]))`: 该函数利用编码格式解码器将给定的字符串从一种格式解码为另一种格式。编码的任何错误都用errors参数定义的字符串标记. 此函数特别用于在字符串和Unicode编码格式之间转换。默认（当不给出encoding参数值）操作是以严格方式将字符串解码为UTF-8格式，发生errors错误时就引发ValueError异常。有关合适的解码列表，请见codecs模块
* `vars([object])`: 该函数返回对应于当前局部符号表的字典。当给出模块、类或实例时，vars()函数返回对应那个对象的符号表的字典。因为结果是非定义的，所以一定不要修改返回的字典
* `xrange([start,]stop[,step])`: 该函数的作用与range()函数一样，唯一的区别是：xrange()函数返回一个xrange对象。xrange()对象是个不透明对象类型，此类型返回的信息与所请求的参数列表是一致的，但是它不必存储列表中每个独立的元素。在创建非常巨大列表的情况下，此函数特别有用；利用xrange()函数节省下来的内存比起用range()函数是相当可观的
* `zip(seq1,…)`: zip()函数处理一系列序列，将这些序列返回一个元组列表。其中，每个元组包含了给定的每个序列的第n个元素。
* `exec`: exec语句被设计为执行能使用函数和语句的任意组合的python的任何代码片段。执行的代码访问相同的全局定义和局部定义的对象、类和方法或函数。以下是使用exec语句的简单例子：`exec “print ‘Hello World’”` 也能通过提供一个包含对象及其取值的列表的字典来限定对exec语句有效的资源，如下例这样：`exec “print message”in myglobals,mylocals` 能用globals()和locals()函数来获得当前的字典. 请注意，exec语句执行表达式和语句、或者对表达式和语句求值，但是exec语句不返回任何值。因为exec是语句不是函数，所以任何获取返回值的试图都将导致语法错误
* `execfile()函数`: 该函数执行与exec语句同样的操作，正如前面所描述的那样，它们的不同之处在于：execfile()函数从问几十年中读取被执行的语句，执行的对象不是字符串，不是代码对象；execfile()函数的其他所有方面都与exec语句等价
* `eval()函数`: 该函数不允许执行任意的python语句。eval()函数被设计为：执行一个python表达式，并返回值，如下例中一样：`result=eval(userexpression)` 或者在语句中更显式地给出表达式，如下例所示：`result=eval(“3+6”)` 不能使用eval()函数去执行语句，根据经验，通常使用eval()函数开将一表达式求值并返回一个值，而在其他所有情况下则使用exec语句`exec()`



## python3新特性


### 1. pathlib

* [8. pathlib](#8-pathlib)



### 2. f-string

[python3 f-string格式化字符串的高级用法](http://www.mlln.cn/2018/05/19/python3%20f-string%E6%A0%BC%E5%BC%8F%E5%8C%96%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E9%AB%98%E7%BA%A7%E7%94%A8%E6%B3%95/)





</br>

----

# 2. 常用模块

## 标准模块

### 1. `sys`

* `sys.platform`：查看底层操作系统名称
* `sys.maxsize`：查看计算机上可容纳的最大的“原生”整型（python3.X版本中整型可以是任意长）
* `sys.version`：查看python版本
* `sys.modules`：查看已加载模块表
* `sys.getrefcount`：查看对象的引用次数
* `sys.builtin_module_names`：查看python可执行程序的内置模块名称
* `sys.exc_info`：返回异常的`(类型，值，追踪对象)`，可以使用`traceback.print_tb(追踪对象)`来显示详细信息。
* `sys.stdin` 、`sys.stdout`、`sys.stderr`: 标准输入，标准输出，错误输出
* `sys.stdin.isatty()`：判断标准输入是否是控制台（console），如果从windows的DOS，或者类unix的终端输入，则为console，如果将stdin重定向到文件（< filename）以及通过管道（|）将内容输出到stdin则不是console
* `sys.getsizeof()`: 查看变量占用内存大小

### 2. `os`

* `os.name` : 判断平台，Windows 返回 'nt'; Linux 返回'posix'
* `os.getpid`：查看调用函数的进程ID
* `os.pathsep`：平台的路径分隔符（win平台：';'）
* `os.sep`：平台的目录分隔符（win平台：'\\\'）
* `os.pardir`：平台的父目录指示器（win平台：'..'）
* `os.curdir`：平台的当前目录指示器（win平台：'.'）
* `os.linesep`：平台的底层计算机所采用的换行符（win平台：'\r\n'）
* `os.system` : 在python脚本中运行shell命令
* `os.popen` : 运行shell脚本并与其输入或输出流相连接 【可使用较新的subprocess模块来对生成的shell命令流进行精确控制，但会增加代码复杂性】
* `os.startfile` : 类似鼠标点击图标，如`os.startfile("webpage.html")`：在浏览器中打开文件。
* `os.environ` : 获取和设置shell环境变量
* `os.fork` : 在类unix系统下派生新的子进程
* `os.pipe` : 负责程序间通信
* `os.execlp` : 启动新程序
* `os.spawnv` : 启动带有底层控制的新程序
* `os.open` : 打开基于底层描述符的文件
* `os.mkfifo` : 创建新的命名管道
* `os.stat` : 获取文件底层信息
* `os.walk` : 将函数或循环应用于整个目录树的各部分
*`os.symlink`: 符号链接

### 3. `os.path`

* `os.path.normpath`：将混合了Unix和Windows分隔符的路径转化为统一分隔符的路径

### 4. `functools`

functools，用于高阶函数：指那些作用于函数或者返回其它函数的函数，通常只要是可以被当做函数调用的对象就是这个模块的目标。
在Python 2.7 中具备如下方法，
`cmp_to_key`，将一个比较函数转换关键字函数；
`partial`，针对函数起作用，并且是部分的；
`reduce`，与python内置的reduce函数功能一样；
`total_ordering`，在类装饰器中按照缺失顺序，填充方法；
`update_wrapper`，更新一个包裹（wrapper）函数，使其看起来更像被包裹（wrapped）的函数；
`wraps`，可用作一个装饰器，简化调用update_wrapper的过程；

**`cmp_to_key`**

将老式的比较函数（comparison function）转换为关键字函数（key function），与接受key function的工具一同使用（例如sorted，min，max，heapq.nlargest，itertools.groupby），该函数主要用于将程序转换成Python 3格式的，因为Python 3中不支持比较函数。
比较函数是可调用的，接受两个参数，比较这两个参数并根据他们的大小关系返回负值、零或者正值中的一个。关键字函数也是可调用的，接受一个参数，同时返回一个可以用作排序关键字的值。

```
from functools import cmp_to_key 
 def compare(ele1,ele2):

   
        return ele2 - ele1 
 a = [2,3,1] 
print sorted(a, key = cmp_to_key(compare))
```
输出：`[3, 2, 1]`

**`partial`**

functools.partial(func, *args, **keywords)，函数装饰器，返回一个新的partial对象。调用partial对象和调用被修饰的函数func相同，只不过调用partial对象时传入的参数个数通常要少于调用func时传入的参数个数。当一个函数func可以接收很多参数，而某一次使用只需要更改其中的一部分参数，其他的参数都保持不变时，partial对象就可以将这些不变的对象冻结起来，这样调用partial对象时传入未冻结的参数，partial对象调用func时连同已经被冻结的参数一同传给func函数，从而可以简化调用过程。
如果调用partial对象时提供了更多的参数，那么他们会被添加到args的后面，如果提供了更多的关键字参数，那么它们将扩展或者覆盖已经冻结的关键字参数。
partial对象的调用如下，

```
import functools 
 def add(a,b):

   
        return a + b 
 add3 = functools.partial(add,3) 
add5 = functools.partial(add,5) 
 print add3(4) 
 print add5(10)
```

输出：

```
7
15
```

**`reduce`**

与Python内置的reduce函数一样，为了向Python3过渡；

```
import functools 
 a = range(1,6) 
print functools.reduce(lambda x,y:x+y,a)
```

控制台输出: `15`

**`total_ordering`**

这是一个类装饰器，给定一个类，这个类定义了一个或者多个比较排序方法，这个类装饰器将会补充其余的比较方法，减少了自己定义所有比较方法时的工作量；

被修饰的类必须至少定义 `__lt__()`， `__le__()`，`__gt__()`，`__ge__()`中的一个，同时，被修饰的类还应该提供 `__eq__()`方法。

```
from functools import total_ordering 
 class Person:

   
        # 定义相等的比较函数

   
        def __eq__(self,other):
                return ((self.lastname.lower(),self.firstname.lower()) ==
                            (other.lastname.lower(),other.firstname.lower()))
        # 定义小于的比较函数
        def __lt__(self,other):
                return ((self.lastname.lower(),self.firstname.lower()) <
                            (other.lastname.lower(),other.firstname.lower())) 
p1 = Person() 
p2 = Person() 
p1.lastname = "123" 
p1.firstname = "000" 
p2.lastname = "1231" 
p2.firstname = "000" 
print p1 < p2 
print p1 <= p2 
print p1 == p2 
print p1 > p2 
print p1 >= p2
```
控制台输出:
```
True 
True 
False 
False 
False
```

**`update_wrapper`**

更新一个包裹（wrapper）函数，使其看起来更像被包裹（wrapped）的函数。
可选的参数指定了被包裹函数的哪些属性直接赋值给包裹函数的对应属性，同时包裹函数的哪些属性要更新而不是直接接受被包裹函数的对应属性，参数assigned的默认值对应于模块级常量WRAPPER_ASSIGNMENTS（默认地将被包裹函数的 `__name__`，` __module__`，和 `__doc__` 属性赋值给包裹函数），参数updated的默认值对应于模块级常量`WRAPPER_UPDATES`（默认更新wrapper函数的 `__dict__` 属性）。
这个函数的主要用途是在一个装饰器中，原函数会被装饰（包裹），装饰器函数会返回一个wrapper函数，如果装饰器返回的这个wrapper函数没有被更新，那么它的一些元数据更多的是反映wrapper函数定义的特征，无法反映wrapped函数的特性。

**`wraps`**

这个函数可用作一个装饰器，简化调用update_wrapper的过程，调用这个函数等价于调用`partial(update_wrapper, wrapped = wrapped, assigned = assigned,updated = updated)`。

```
from functools import wraps 
 def my_decorator(f):

   
        @wraps(f)
        def wrapper(*args,**kwds):
                print "Calling decorated function"
                return f(*args,**kwds)
                return wrapper 
@my_decorator 
def example():

   
        """DocString"""
        print "Called example function" 
 example() 
print example.__name__ 
print example.__doc__
```

控制台输出:

```
Calling decorated function 
Called example function 
example 
DocString
```

可以看到，最终调用函数example时，是经过 @my_decorator装饰的，装饰器的作用是接受一个被包裹的函数作为参数，对其进行加工，返回一个包裹函数，代码使用 @functools.wraps装饰将要返回的包裹函数wrapper，使得它的 __name__， __module__，和 __doc__ 属性与被装饰函数example完全相同，这样虽然最终调用的是经过装饰的example函数，但是某些属性还是得到维护。

如果在 @my_decorator的定义中不使用 @function.wraps装饰包裹函数，那么最终example.__name__ 将会变成'wrapper'，而example.__doc__ 也会丢失。

将 @wraps(f)注释掉，然后运行程序，控制台输出，

```
Calling decorated function 
Called example function 
wrapper 
None
```

### 5. `subprocess`

* `subprocess.call` : 类似os.system(), 注意参数shell=True，在windows下，需要shell=True的参数传给call等shuprocess工具和popen工具，才能运行shell内建命令， 在类unix平台，shell=False时，程序命令直接有os.execvp运行，shell=True时，程序转而由shell运行，而且用其他参数指定shell。
* `subprocess.Popen` 类似os.popen, 

### 6. `msvcrt`

* `msvcrt.putch()` : 
* `msvcrt.getche()` : 

### 7.`math`

|  函数 | 说明 | 实例 |
| ----- | ----:|:---- |
|  math.e | 自然常数e | math.e #2.718281828459045 |
|  math.pi | 圆周率pi | math.pi #3.141592653589793 |
|  math.degrees(x) | 弧度转度 | math.degrees(math.pi) #180.0 |
|  math.radians(x) | 度转弧度 | math.radians(45) #0.7853981633974483 |
|  math.exp(x) | 返回e的x次方 | math.exp(2) #7.38905609893065 |
|  math.expm1(x) | 返回e的x次方减1 | math.expm1(2) #6.38905609893065 |
|  math.log(x[, base]) | 返回x的以base为底的对数，base默认为e | math.log(math.e) #1.0 <br>math.log(2, 10) #0.30102999566398114 |
|  math.log10(x) | 返回x的以10为底的对数 | math.log10(2) #0.30102999566398114 |
|  math.log1p(x) | 返回1+x的自然对数（以e为底） | math.log1p(math.e-1) #1.0 |
|  math.pow(x, y) | 返回x的y次方 | math.pow(5,3) #125.0 |
|  math.sqrt(x) | 返回x的平方根 | math.sqrt(3) #1.7320508075688772 |
|  math.ceil(x) | 返回不小于x的整数 | math.ceil(5.2) #6.0 |
|  math.floor(x) | 返回不大于x的整数 | math.floor(5.8) #5.0 |
|  math.trunc(x) | 返回x的整数部分 | math.trunc(5.8) #5 |
|  math.modf(x) | 返回x的小数和整数 | math.modf(5.2) #(0.20000000000000018, 5.0) |
|  math.fabs(x) | 返回x的绝对值 | math.fabs(-5) #5.0 |
|  math.fmod(x, y) | 返回x%y（取余） | math.fmod(5,2) #1.0 |
|  math.fsum([x, y, ...]) | 返回无损精度的和 | 0.1+0.2+0.3 #0.6000000000000001 math.fsum([0.1, 0.2, 0.3]) #0.6 |
|  math.factorial(x) | 返回x的阶乘 | math.factorial(5) #120 |
|  math.isinf(x) | 若x为无穷大，返回True；否则，返回False | math.isinf(1.0e+308) #False math.isinf(1.0e+309) #True |
|  math.isnan(x) | 若x不是数字，返回True；否则，返回False | math.isnan(1.2e3) #False |
|  math.hypot(x, y) | 返回以x和y为直角边的斜边长 | math.hypot(3,4) #5.0 |
|  math.copysign(x, y) | 若y<0，返回-1乘以x的绝对值； 否则，返回x的绝对值 | math.copysign(5.2, -1) #-5.2 |
|  math.frexp(x) | 返回m和i，满足m乘以2的i次方 | math.frexp(3) #(0.75, 2) |
|  math.ldexp(m, i) | 返回m乘以2的i次方 | math.ldexp(0.75, 2) #3.0 |
|  math.sin(x) | 返回x（弧度）的三角正弦值 | math.sin(math.radians(30)) #0.49999999999999994 |
|  math.asin(x) | 返回x的反三角正弦值 | math.asin(0.5) #0.5235987755982989 |
|  math.cos(x) | 返回x（弧度）的三角余弦值 | math.cos(math.radians(45)) #0.7071067811865476 |
|  math.acos(x) | 返回x的反三角余弦值 | math.acos(math.sqrt(2)/2) #0.7853981633974483 |
|  math.tan(x) | 返回x（弧度）的三角正切值 | math.tan(math.radians(60)) #1.7320508075688767 |
|  math.atan(x) | 返回x的反三角正切值 | math.atan(1.7320508075688767) #1.0471975511965976 |
|  math.atan2(x, y) | 返回x/y的反三角正切值 | math.atan2(2,1) #1.1071487177940904 |
|  math.sinh(x) | 返回x的双曲正弦函数 |  |
|  math.asinh(x) | 返回x的反双曲正弦函数 |  |
|  math.cosh(x) | 返回x的双曲余弦函数 |  |
|  math.acosh(x) | 返回x的反双曲余弦函数 |  |
|  math.tanh(x) | 返回x的双曲正切函数 |  |
|  math.atanh(x) | 返回x的反双曲正切函数 |  |
|  math.erf(x) | 返回x的误差函数 |  |
|  math.erfc(x) | 返回x的余误差函数 |  |
|  math.gamma(x) | 返回x的伽玛函数 |  |
|  math.degrees(x) | 弧度转度 | math.degrees(math.pi) #180.0 |
|  math.radians(x) | 度转弧度 | math.radians(45) #0.7853981633974483 |
|  math.exp(x) | 返回e的x次方 | math.exp(2) #7.38905609893065 |
|  math.expm1(x) | 返回e的x次方减1 | math.expm1(2) #6.38905609893065 |
|  math.log(x[, base]) | 返回x的以base为底的对数，base默认为e | math.log(math.e) #1.0 math.log(2, 10) #0.30102999566398114 |
|  math.log10(x) | 返回x的以10为底的对数 | math.log10(2) #0.30102999566398114 |
|  math.log1p(x) | 返回1+x的自然对数（以e为底） | math.log1p(math.e-1) #1.0 |
|  math.pow(x, y) | 返回x的y次方 | math.pow(5,3) #125.0 |
|  math.sqrt(x) | 返回x的平方根 | math.sqrt(3) #1.7320508075688772 |
|  math.ceil(x) | 返回不小于x的整数 | math.ceil(5.2) #6.0 |
|  math.floor(x) | 返回不大于x的整数 | math.floor(5.8) #5.0 |
|  math.trunc(x) | 返回x的整数部分 | math.trunc(5.8) #5 |
|  math.modf(x) | 返回x的小数和整数 | math.modf(5.2) #(0.20000000000000018, 5.0) |
|  math.fabs(x) | 返回x的绝对值 | math.fabs(-5) #5.0 |
|  math.fmod(x, y) | 返回x%y（取余） | math.fmod(5,2) #1.0 |
|  math.fsum([x, y, ...]) | 返回无损精度的和 | 0.1+0.2+0.3 #0.6000000000000001 math.fsum([0.1, 0.2, 0.3]) #0.6 |
|  math.factorial(x) | 返回x的阶乘 | math.factorial(5) #120 |
|  math.isinf(x) | 若x为无穷大，返回True；否则，返回False | math.isinf(1.0e+308) #False math.isinf(1.0e+309) #True |
|  math.isnan(x) | 若x不是数字，返回True；否则，返回False | math.isnan(1.2e3) #False |
|  math.hypot(x, y) | 返回以x和y为直角边的斜边长 | math.hypot(3,4) #5.0 |
|  math.copysign(x, y) | 若y<0，返回-1乘以x的绝对值； 否则，返回x的绝对值 | math.copysign(5.2, -1) #-5.2 |
|  math.frexp(x) | 返回m和i，满足m乘以2的i次方 | math.frexp(3) #(0.75, 2) |
|  math.ldexp(m, i) | 返回m乘以2的i次方 | math.ldexp(0.75, 2) #3.0 |
|  math.sin(x) | 返回x（弧度）的三角正弦值 | math.sin(math.radians(30)) #0.49999999999999994 |
|  math.asin(x) | 返回x的反三角正弦值 | math.asin(0.5) #0.5235987755982989 |
|  math.cos(x) | 返回x（弧度）的三角余弦值 | math.cos(math.radians(45)) #0.7071067811865476 |
|  math.acos(x) | 返回x的反三角余弦值 | math.acos(math.sqrt(2)/2) #0.7853981633974483 |
|  math.tan(x) | 返回x（弧度）的三角正切值 | math.tan(math.radians(60)) #1.7320508075688767 |
|  math.atan(x) | 返回x的反三角正切值 | math.atan(1.7320508075688767) #1.0471975511965976 |
|  math.atan2(x, y) | 返回x/y的反三角正切值 | math.atan2(2,1) #1.1071487177940904 |
|  math.sinh(x) | 返回x的双曲正弦函数 |  |
|  math.asinh(x) | 返回x的反双曲正弦函数 |  |
|  math.cosh(x) | 返回x的双曲余弦函数 |  |
|  math.acosh(x) | 返回x的反双曲余弦函数 |  |
|  math.tanh(x) | 返回x的双曲正切函数 |  |
|  math.atanh(x) | 返回x的反双曲正切函数 |  |
|  math.erf(x) | 返回x的误差函数 |  |
|  math.erfc(x) | 返回x的余误差函数 |  |
|  math.gamma(x) | 返回x的伽玛函数 |  |
|  math.lgamma(x) | 返回x的绝对值的自然对数的伽玛函数 | =ath.lgamma(x) | 返回x的绝对值的自然对数的伽玛函数 |  |


### 8. itertools

[廖雪峰的官方网站-itertools](https://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001415616001996f6b32d80b6454caca3d33c965a07611f000)

[Python中的分组函数（groupby、itertools）- 爱做梦的鱼](https://www.cnblogs.com/dreamer-fish/p/5522687.html)

itertools模块可创建的迭代器一般分为三类:

* **无限迭代器** （Infinite Iterators）
* **终止于最短输入序列的迭代器**   （Iterators terminating on the shortest input sequence）
* **组合生成器** （Combinatoric generators）


1. **无限迭代器**

`count` : itertools.count(start, step)  # count(5, 2): 从5开始的整数循环器，每次增加2，即5, 7, 9, 11, 13, 15 ...

`cycle` : itertools.cycle(iterable)     # cycle('abc'): 重复序列的元素，既a, b, c, a, b, c ...

`repeat` : itertools.repeat(object[, times])   # repeat(1.2): 重复1.2，构成无穷循环器，即1.2, 1.2, 1.2, ...

2. **终止于最短输入序列的迭代器**

`chain` : itertools.chain(*iterables)  # chain([1, 2, 3], [4, 5, 7]): 连接两个迭代器成为一个。1, 2, 3, 4, 5, 7

`compress` : itertools.compress(data, selectors)  # data为数据对象, selectors为选择器(规则), compress([1,2,3], True,False,True]): 返回数据对象中对应规则为True的元素 1,3

### 9. str

`str.partition` : 根据指定的分隔符将字符串进行分割。 "os.path.abspath".partition(".")   # ('os', '.', 'path.abspath')

`str.rpartition` : 类似`str.partiton`。 "os.path.baspath".rpartition(".") # ('os.path', '.', 'abspath')


### 10. collections

`collections`是Python内建的一个集合模块，提供了许多有用的集合类。

**namedtuple**

我们知道`tuple`可以表示不变集合，例如，一个点的二维坐标就可以表示成：

```
>>> p = (1, 2)
```

但是，看到(1, 2)，很难看出这个tuple是用来表示一个坐标的。

定义一个`class`又小题大做了，这时，`namedtuple`就派上了用场：

```
>>> from collections import namedtuple
>>> Point = namedtuple('Point', ['x', 'y'])  # 或者Point=namedtuple('Point', 'x y')
>>> p = Point(1, 2)
>>> p.x
1
>>> p.y
2
```

`namedtuple`是一个函数，它用来创建一个自定义的tuple对象，并且规定了tuple元素的个数，并可以用属性而不是索引来引用tuple的某个元素。

这样一来，我们用`namedtuple`可以很方便地定义一种数据类型，它具备tuple的不变性，又可以根据属性来引用，使用十分方便。

可以验证创建的Point对象是`tuple`的一种子类：

```
>>> isinstance(p, Point)
True
>>> isinstance(p, tuple)
True
```

类似的，如果要用坐标和半径表示一个圆，也可以用`namedtuple`定义：

```
# namedtuple('名称', [属性list]):
Circle = namedtuple('Circle', ['x', 'y', 'r'])
```

**deque**

使用`list`存储数据时，按索引访问元素很快，但是插入和删除元素就很慢了，因为list是线性存储，数据量大的时候，插入和删除效率很低。

`deque`是为了高效实现插入和删除操作的双向列表，适合用于队列和栈：

```
>>> from collections import deque
>>> q = deque(['a', 'b', 'c'])
>>> q.append('x')
>>> q.appendleft('y')
>>> q
deque(['y', 'a', 'b', 'c', 'x'])
```

`deque`除了实现`list`的`append()`和`pop()`外，还支持`appendleft()`和`popleft()`，这样就可以非常高效地往头部添加或删除元素。

**defaultdict**

使用`dict`时，如果引用的`Key`不存在，就会抛出`KeyError`。如果希望`key`不存在时，返回一个默认值，就可以用`defaultdict`：

```
>>> from collections import defaultdict
>>> dd = defaultdict(lambda: 'N/A')
>>> dd['key1'] = 'abc'
>>> dd['key1'] # key1存在
'abc'
>>> dd['key2'] # key2不存在，返回默认值
'N/A'
```

注意默认值是调用函数返回的，而函数在创建`defaultdict`对象时传入。

除了在`Key`不存在时返回默认值，`defaultdict`的其他行为跟`dict`是完全一样的。

**OrderedDict**

使用`dict`时，`Key`是无序的。在对`dict`做迭代时，我们无法确定`Key`的顺序。

如果要保持`Key`的顺序，可以用`OrderedDict`：

```
>>> from collections import OrderedDict
>>> d = dict([('a', 1), ('b', 2), ('c', 3)])
>>> d # dict的Key是无序的
{'a': 1, 'c': 3, 'b': 2}
>>> od = OrderedDict([('a', 1), ('b', 2), ('c', 3)])
>>> od # OrderedDict的Key是有序的
OrderedDict([('a', 1), ('b', 2), ('c', 3)])
```

注意，`OrderedDict`的`Key`会按照插入的顺序排列，不是`Key`本身排序：

```
>>> od = OrderedDict()
>>> od['z'] = 1
>>> od['y'] = 2
>>> od['x'] = 3
>>> od.keys() # 按照插入的Key的顺序返回
['z', 'y', 'x']
```
`OrderedDict`可以实现一个`FIFO`（先进先出）的`dict`，当容量超出限制时，先删除最早添加的`Key`：
```
from collections import OrderedDict

class LastUpdatedOrderedDict(OrderedDict):

    def __init__(self, capacity):
        super(LastUpdatedOrderedDict, self).__init__()
        self._capacity = capacity

    def __setitem__(self, key, value):
        containsKey = 1 if key in self else 0
        if len(self) - containsKey >= self._capacity:
            last = self.popitem(last=False)
            print 'remove:', last
        if containsKey:
            del self[key]
            print 'set:', (key, value)
        else:
            print 'add:', (key, value)
        OrderedDict.__setitem__(self, key, value)
```

**Counter**

`Counter`是一个简单的计数器，例如，统计字符出现的个数：

```
>>> from collections import Counter
>>> c = Counter()
>>> for ch in 'programming':
...     c[ch] = c[ch] + 1
...
>>> c
Counter({'g': 2, 'm': 2, 'r': 2, 'a': 1, 'i': 1, 'o': 1, 'n': 1, 'p': 1})
```

`Counter`实际上也是`dict`的一个子类，上面的结果可以看出，字符'g'、'm'、'r'各出现了两次，其他字符各出现了一次。

**小结**

`collections`模块提供了一些有用的集合类，可以根据需要选用。


### 11. logging

**[Python中内置的日志模块logging用法详解](http://www.jb51.net/article/88449.htm)**

[Python中的logging模块-伯乐在线](http://python.jobbole.com/86887/)

[每个 Python 程序员都要知道的日志实践](http://python.jobbole.com/81666/) : 使用合适的等级(DEBUG, INFO, WARNING, ERROR, CRITICAL)输出日志记录

[python logging日志模块以及多进程日志](http://python.jobbole.com/87300/)

[Python logger模块-浅雨凉](https://www.cnblogs.com/qianyuliang/p/7234217.html)

[python 日志模块 logging 详解](https://my.oschina.net/leejun2005/blog/126713)  : 对Handler类有详细描述

**基本用法**

下面的代码展示了logging最基本的用法。

```
# -*- coding: utf-8 -*-

import logging
import sys

# 获取logger实例，如果参数为空则返回root logger
logger = logging.getLogger("AppName")

# 指定logger输出格式
formatter = logging.Formatter('%(asctime)s %(levelname)-8s: %(message)s')

# 文件日志
file_handler = logging.FileHandler("test.log")
file_handler.setFormatter(formatter)  # 可以通过setFormatter指定输出格式

# 控制台日志
console_handler = logging.StreamHandler(sys.stdout)
console_handler.formatter = formatter  # 也可以直接给formatter赋值

# 为logger添加的日志处理器
logger.addHandler(file_handler)
logger.addHandler(console_handler)

# 指定日志的最低输出级别，默认为WARN级别
logger.setLevel(logging.INFO)

# 输出不同级别的log
logger.debug('this is debug info')
logger.info('this is information')
logger.warn('this is warning message')
logger.error('this is error message')
logger.fatal('this is fatal message, it is same as logger.critical')
logger.critical('this is critical message')

# 2016-10-08 21:59:19,493 INFO    : this is information
# 2016-10-08 21:59:19,493 WARNING : this is warning message
# 2016-10-08 21:59:19,493 ERROR   : this is error message
# 2016-10-08 21:59:19,493 CRITICAL: this is fatal message, it is same as logger.critical
# 2016-10-08 21:59:19,493 CRITICAL: this is critical message

# 移除一些日志处理器
logger.removeHandler(file_handler)
```

除了这些基本用法，还有一些常见的小技巧可以分享一下。

**格式化输出日志**

```
# 格式化输出

service_name = "Booking"
logger.error('%s service is down!' % service_name)  # 使用python自带的字符串格式化，不推荐
logger.error('%s service is down!', service_name)  # 使用logger的格式化，推荐
logger.error('%s service is %s!', service_name, 'down')  # 多参数格式化
logger.error('{} service is {}'.format(service_name, 'down')) # 使用format函数，推荐

# 2016-10-08 21:59:19,493 ERROR   : Booking service is down!
```

**记录异常信息**

当你使用logging模块记录异常信息时，不需要传入该异常对象，只要你直接调用logger.error() 或者 logger.exception()就可以将当前异常记录下来。

```
# 记录异常信息

try:
    1 / 0
except:
    # 等同于error级别，但是会额外记录当前抛出的异常堆栈信息
    logger.exception('this is an exception message')

# 2016-10-08 21:59:19,493 ERROR   : this is an exception message
# Traceback (most recent call last):
#   File "D:/Git/py_labs/demo/use_logging.py", line 45, in 
#     1 / 0
# ZeroDivisionError: integer division or modulo by zero
```

**logging配置要点**

***GetLogger()方法***

这是最基本的入口，该方法参数可以为空，默认的logger名称是root，如果在同一个程序中一直都使用同名的logger，其实会拿到同一个实例，使用这个技巧就可以跨模块调用同样的logger来记录日志。
另外你也可以通过日志名称来区分同一程序的不同模块，比如这个例子。
```
logger = logging.getLogger("App.UI")
logger = logging.getLogger("App.Service")
```
***Formatter日志格式***

Formatter对象定义了log信息的结构和内容，构造时需要带两个参数：

* 一个是格式化的模板fmt，默认会包含最基本的level和 message信息
* 一个是格式化的时间样式datefmt，默认为 2003-07-08 16:49:45,896 (%Y-%m-%d %H:%M:%S)

fmt中允许使用的变量可以参考下表。

* **%(name)s** Logger的名字
* **%(levelno)s** 数字形式的日志级别
* **%(levelname)s** 文本形式的日志级别
* **%(pathname)s** 调用日志输出函数的模块的完整路径名，可能没有
* **%(filename)s** 调用日志输出函数的模块的文件名
* **%(module)s** 调用日志输出函数的模块名|
* **%(funcName)s** 调用日志输出函数的函数名|
* **%(lineno)d** 调用日志输出函数的语句所在的代码行
* **%(created)f** 当前时间，用UNIX标准的表示时间的浮点数表示|
* **%(relativeCreated)d** 输出日志信息时的，自Logger创建以来的毫秒数|
* **%(asctime)s** 字符串形式的当前时间。默认格式是“2003-07-08 16:49:45,896”。逗号后面的是毫秒
* **%(thread)d** 线程ID。可能没有
* **%(threadName)s** 线程名。可能没有
* **%(process)d** 进程ID。可能没有
* **%(message)s** 用户输出的消息

**SetLevel 日志级别**

Logging有如下级别: `DEBUG`，`INFO`，`WARNING`，`ERROR`，`CRITICAL` .默认级别是WARNING，logging模块只会输出指定level以上的log。这样的好处, 就是在项目开发时debug用的log，在产品release阶段不用一一注释，只需要调整logger的级别就可以了，很方便。


有了灵活的日志记录模块后，你可以按适当的等级将日志记录输出到任何地方然后配置它们。那么你可能会问，什么是合适的等级呢？在这儿我将分享一些我的经验。

大多数的情况下，你都不想阅读日志中的太多细节。因此，只有你在调试过程中才会使用 `DEBUG` 等级。我只使用 `DEBUG` 获取详细的调试信息，特别是当数据量很大或者频率很高的时候，比如算法内部每个循环的中间状态。

```
def complex_algorithm(items):
    for i, item in enumerate(items):
        # do some complex algorithm computation

        logger.debug('%s iteration, item=%s', i, item)
```

在处理请求或者服务器状态变化等日常事务中，我会使用 `INFO` 等级。

```
def handle_request(request):
    logger.info('Handling request %s', request)
    # handle request here

    result = 'result'
    logger.info('Return result: %s', result)

def start_service():
    logger.info('Starting service at port %s ...', port)
    service.start()
    logger.info('Service is started')
```

当发生很重要的事件，但是并不是错误时，我会使用 `WARNING` 。比如，当用户登录密码错误时，或者连接变慢时。

```
def authenticate(user_name, password, ip_address):
    if user_name != USER_NAME and password != PASSWORD:
        logger.warn('Login attempt to %s from IP %s', user_name, ip_address)
        return False
    # do authentication here
```

有错误发生时肯定会使用 `ERROR` 等级了。比如抛出异常，IO 操作失败或者连接问题等。

```
def get_user_by_id(user_id):
    user = db.read_user(user_id)
    if user is None:
        logger.error('Cannot find user with user_id=%s', user_id)
        return user
    return user
```

我很少使用 CRITICAL 。当一些特别糟糕的事情发生时，你可以使用这个级别来记录。比方说，内存耗尽，磁盘满了或者核危机（希望永远别发生 :S）。

**Handler 日志处理器**

最常用的是StreamHandler和FileHandler, Handler用于向不同的输出端打log。

Logging包含很多handler, 可能用到的有下面几种

* **StreamHandler** instances send error messages to streams (file-like objects).

使用这个Handler可以向类似与sys.stdout或者sys.stderr的任何文件对象(file object)输出信息。它的构造函数是：

StreamHandler([strm])

* **FileHandler** instances send error messages to disk files.

和StreamHandler类似，用于向一个文件输出日志信息。不过FileHandler会帮你打开这个文件。它的构造函数是：

FileHandler(filename[,mode])

filename是文件名，必须指定一个文件名。

mode是文件的打开方式。参见Python内置函数open()的用法。默认是’a'，即添加到文件末尾。

* **RotatingFileHandler** instances send error messages to disk files, with support for maximum log file sizes and log file rotation.

这个Handler类似于上面的FileHandler，但是它可以管理文件大小。当文件达到一定大小之后，它会自动将当前日志文件改名，然后创建 一个新的同名日志文件继续输出。比如日志文件是chat.log。当chat.log达到指定的大小之后，RotatingFileHandler自动把 文件改名为chat.log.1。不过，如果chat.log.1已经存在，会先把chat.log.1重命名为chat.log.2。。。最后重新创建 chat.log，继续输出日志信息。它的构造函数是：

RotatingFileHandler( filename[, mode[, maxBytes[, backupCount]]])

其中filename和mode两个参数和FileHandler一样。

maxBytes用于指定日志文件的最大文件大小。如果maxBytes为0，意味着日志文件可以无限大，这时上面描述的重命名过程就不会发生。

backupCount用于指定保留的备份文件的个数。比如，如果指定为2，当上面描述的重命名过程发生时，原有的chat.log.2并不会被更名，而是被删除。

* **TimedRotatingFileHandler** instances send error messages to disk files, rotating the log file at certain timed intervals.

这个Handler和RotatingFileHandler类似，不过，它没有通过判断文件大小来决定何时重新创建日志文件，而是间隔一定时间就 自动创建新的日志文件。重命名的过程与RotatingFileHandler类似，不过新的文件不是附加数字，而是当前时间。它的构造函数是：

TimedRotatingFileHandler( filename [,when [,interval [,backupCount]]])

其中filename参数和backupCount参数和RotatingFileHandler具有相同的意义。

interval是时间间隔。

when参数是一个字符串。表示时间间隔的单位，不区分大小写。它有以下取值：

S 秒

M 分

H 小时

D 天

W 每星期（interval==0时代表星期一）

midnight 每天凌晨

* **SocketHandler** instances send error messages to TCP/IP sockets.

* **DatagramHandler** instances send error messages to UDP sockets.

以上两个Handler类似，都是将日志信息发送到网络。不同的是前者使用TCP协议，后者使用UDP协议。它们的构造函数是：
Handler(host, port)

其中host是主机名，port是端口名

* **SMTPHandler** instances send error messages to a designated email address.

**Configuration 配置方法**

logging的配置大致有下面几种方式。

* 通过代码进行完整配置，参考开头的例子，主要是通过getLogger方法实现。
* 通过代码进行简单配置，下面有例子，主要是通过basicConfig方法实现。
* 通过配置文件，下面有例子，主要是通过 logging.config.fileConfig(filepath)

***logging.basicConfig***

basicConfig()提供了非常便捷的方式让你配置logging模块并马上开始使用，可以参考下面的例子。具体可以配置的项目请查阅官方文档。

```
import logging

logging.basicConfig(filename='example.log',level=logging.DEBUG)
logging.debug('This message should go to the log file')

logging.basicConfig(format='%(levelname)s:%(message)s', level=logging.DEBUG)
logging.debug('This message should appear on the console')

logging.basicConfig(format='%(asctime)s %(message)s', datefmt='%m/%d/%Y %I:%M:%S %p')
logging.warning('is when this event was logged.')
```

备注： 其实你甚至可以什么都不配置直接使用默认值在控制台中打log，用这样的方式替换print语句对日后项目维护会有很大帮助。

***通过文件配置logging***

如果你希望通过配置文件来管理logging，可以参考这个官方文档。在log4net或者log4j中这是很常见的方式。

```
# logging.conf
[loggers]
keys=root

[logger_root]
level=DEBUG
handlers=consoleHandler
#,timedRotateFileHandler,errorTimedRotateFileHandler

#################################################
[handlers]
keys=consoleHandler,timedRotateFileHandler,errorTimedRotateFileHandler

[handler_consoleHandler]
class=StreamHandler
level=DEBUG
formatter=simpleFormatter
args=(sys.stdout,)

[handler_timedRotateFileHandler]
class=handlers.TimedRotatingFileHandler
level=DEBUG
formatter=simpleFormatter
args=('debug.log', 'H')

[handler_errorTimedRotateFileHandler]
class=handlers.TimedRotatingFileHandler
level=WARN
formatter=simpleFormatter
args=('error.log', 'H')

#################################################
[formatters]
keys=simpleFormatter, multiLineFormatter

[formatter_simpleFormatter]
format= %(levelname)s %(threadName)s %(asctime)s:   %(message)s
datefmt=%H:%M:%S

[formatter_multiLineFormatter]
format= ------------------------- %(levelname)s -------------------------
 Time:      %(asctime)s
 Thread:    %(threadName)s
 File:      %(filename)s(line %(lineno)d)
 Message:
 %(message)s

datefmt=%Y-%m-%d %H:%M:%S
```

假设以上的配置文件放在和模块相同的目录，代码中的调用如下。

```
import os
filepath = os.path.join(os.path.dirname(__file__), 'logging.conf')
logging.config.fileConfig(filepath)
return logging.getLogger()
```

**多模块使用logging**

logging模块保证在同一个python解释器内，多次调用logging.getLogger('log_name')都会返回同一个logger实例，即使是在多个模块的情况下。所以典型的多模块场景下使用logging的方式是在main模块中配置logging，这个配置会作用于多个的子模块，然后在其他模块中直接通过getLogger获取Logger对象即可。

配置文件：

```
 [loggers] 
 keys=root,main 

 [handlers] 
 keys=consoleHandler,fileHandler 

 [formatters] 
 keys=fmt 

 [logger_root] 
 level=DEBUG 
 handlers=consoleHandler 

 [logger_main] 
 level=DEBUG 
 qualname=main 
 handlers=fileHandler 

 [handler_consoleHandler] 
 class=StreamHandler 
 level=DEBUG 
 formatter=fmt 
 args=(sys.stdout,) 

 [handler_fileHandler] 
 class=logging.handlers.RotatingFileHandler 
 level=DEBUG 
 formatter=fmt 
 args=('tst.log','a',20000,5,) 

 [formatter_fmt] 
 format=%(asctime)s - %(name)s - %(levelname)s - %(message)s 
 datefmt=%Y-%m-%d %H:%M:%S
```

主模块main.py：

```
 import logging 
 import logging.config 

 logging.config.fileConfig('logging.conf') 
 root_logger = logging.getLogger('root') 
 root_logger.debug('test root logger...') 

 logger = logging.getLogger('main')
 logger.info('test main logger') 
 logger.info('start import module \'mod\'...') 

 import mod 

 logger.debug('let\'s test mod.testLogger()') 
 mod.testLogger() 
 root_logger.info('finish test...')
```

子模块mod.py：

```
 import logging 
 import submod 

 logger = logging.getLogger('main.mod') 
 logger.info('logger of mod say something...') 

 def testLogger():
     logger.debug('this is mod.testLogger...')

 
     submod.tst()
```

子子模块submod.py：

```
 import logging 
 logger = logging.getLogger('main.mod.submod') 
 logger.info('logger of submod say something...') 
 def tst():

 
     logger.info('this is submod.tst()...')
```

然后运行python main.py，控制台输出：

```
 2012-03-09 18:22:22,793 - root - DEBUG - test root logger... 
 2012-03-09 18:22:22,793 - main - INFO - test main logger 
 2012-03-09 18:22:22,809 - main - INFO - start import module 'mod'... 
 2012-03-09 18:22:22,809 - main.mod.submod - INFO - logger of submod say something... 
 2012-03-09 18:22:22,809 - main.mod - INFO - logger say something... 
 2012-03-09 18:22:22,809 - main - DEBUG - let's test mod.testLogger() 
 2012-03-09 18:22:22,825 - main.mod - DEBUG - this is mod.testLogger... 
 2012-03-09 18:22:22,825 - main.mod.submod - INFO - this is submod.tst()... 
 2012-03-09 18:22:22,841 - root - INFO - finish test...
```

可以看出，和预想的一样，然后在看一下tst.log，logger配置中的输出的目的地：

```
 2012-03-09 18:22:22,793 - main - INFO - test main logger 
 2012-03-09 18:22:22,809 - main - INFO - start import module 'mod'... 
 2012-03-09 18:22:22,809 - main.mod.submod - INFO - logger of submod say something... 
 2012-03-09 18:22:22,809 - main.mod - INFO - logger say something... 
 2012-03-09 18:22:22,809 - main - DEBUG - let's test mod.testLogger() 
 2012-03-09 18:22:22,825 - main.mod - DEBUG - this is mod.testLogger... 
 2012-03-09 18:22:22,825 - main.mod.submod - INFO - this is submod.tst()...
```

tst.log中没有root logger输出的信息，因为logging.conf中配置了只有main logger及其子logger使用RotatingFileHandler，而root logger是输出到标准输出。


### 12. `time` 和 `datetime`

**time**

在Python中，通常有这几种方式来表示时间：

1. 时间戳(timestamp) ：通常来说，时间戳表示的是从1970年1月1日00:00:00开始按秒计算的偏移量。我们运行“type(time.time())”，返回的是float类型。
2. 格式化的时间字符串 ：按照我们想要的方式输出，比如 2017-05-07-19:37:20
3. 元组(struct_time)   ：struct_time元组共有9个元素共九个元素:(年，月，日，时，分，秒，一年中第几周，一年中第几天，夏令时) 

`时间戳`：`time.time()` 从1970年1月1日00:00:00到此刻的秒数，主要用于计算程序的执行时间等。

`结构化时间`：`time.localtime()`        `time.gmtime()`世界标准时间（格林尼治时间）

`结构化时间`转成`时间戳`：`time.mktime(time.localtime())`

`结构化时间`转成`字符串时间`：`time.strftime('%Y-%m-%d %X',time.localtime())`

`字符串时间`转成`结构化时间`：`time.strptime('2017:05:07:19:47:36','%Y-%m-%d %X')`

<img src="https://images2015.cnblogs.com/blog/1103523/201705/1103523-20170507194943070-1402300767.png" width = "500" height = "500" />

`结构化时间`转`标准字符串显示` : `time.asctime()`

`时间戳`转`标准字符串显示` : `time.ctime()`

<img src="https://images2015.cnblogs.com/blog/1103523/201705/1103523-20170507195016336-212158981.png" width = "500" height = "500" />


时间字符串支持的格式符号：（区分大小写）

```
%a  本地星期名称的简写（如星期四为Thu）       
%A  本地星期名称的全称（如星期四为Thursday）       
%b  本地月份名称的简写（如八月份为agu）     
%B  本地月份名称的全称（如八月份为august）       
%c  本地相应的日期和时间的字符串表示（如：15/08/27 10:20:06）       
%d  一个月中的第几天（01 - 31）   
%f  微妙（范围0.999999）     
%H  一天中的第几个小时（24小时制，00 - 23）       
%I  第几个小时（12小时制，0 - 11）       
%j  一年中的第几天（001 - 366）     
%m  月份（01 - 12）     
%M  分钟数（00 - 59）       
%p  本地am或者pm的相应符       
%S  秒（00 - 61）     
%U  一年中的星期数。（00 - 53星期天是一个星期的开始。）第一个星期天之    前的所有天数都放在第0周。     
%w  一个星期中的第几天（0 - 6，0是星期天）     
%W  和%U基本相同，不同的是%W以星期一为一个星期的开始。     
%x  本地相应日期字符串（如15/08/01）     
%X  本地相应时间字符串（如08:08:10）     
%y  去掉世纪的年份（00 - 99）两个数字表示的年份       
%Y  完整的年份（4个数字表示年份） 
%z  与UTC时间的间隔（如果是本地时间，返回空字符串） 
%Z  时区的名字（如果是本地时间，返回空字符串）       
%%  ‘%’字符  
```


代码演示:

```
>>> import time

# 获得时间截
>>> time.time()
1521505668.901931        # type: float

# 获得结构化时间
>>> time.localtime()
time.struct_time(tm_year=2018, tm_mon=3, tm_mday=20, tm_hour=8, tm_min=29, tm_sec=6, tm_wday=1, tm_yday=79, tm_isdst=0)     # type: time.struct_time

# 结构化时间转字符串
# strftime(format[, tuple]) -> string
>>> time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())
'2018-03-20 08:40:59'
# asctime([tuple]) -> string    # 只能转成标准时间, 不能自定义时间格式
>>> time.asctime(time.localtime())
'Tue Mar 20 08:42:02 2018'

# 字符串转结构化时间
# strptime(string, format) -> struct_time
>>> time.strptime("2018-03-20 08:40:59", "%Y-%m-%d %H:%M:%S")
time.struct_time(tm_year=2018, tm_mon=3, tm_mday=20, tm_hour=8, tm_min=40, tm_sec=59, tm_wday=1, tm_yday=79, tm_isdst=-1)

# 时间截转结构化时间
# localtime([seconds]) -> (tm_year,tm_mon,tm_mday,tm_hour,tm_min, tm_sec,tm_wday,tm_yday,tm_isdst)
>>> time.localtime(1521505668.901931)
time.struct_time(tm_year=2018, tm_mon=3, tm_mday=20, tm_hour=8, tm_min=27, tm_sec=48, tm_wday=1, tm_yday=79, tm_isdst=0)
# gmtime([seconds]) -> (tm_year, tm_mon, tm_mday, tm_hour, tm_min, tm_sec, tm_wday, tm_yday, tm_isdst)
>>> time.gmtime(1521505668.901931)
time.struct_time(tm_year=2018, tm_mon=3, tm_mday=20, tm_hour=0, tm_min=27, tm_sec=48, tm_wday=1, tm_yday=79, tm_isdst=0)

# 结构化转时间截
# mktime(tuple) -> floating point number
>>> time.mktime(time.localtime())
1521506980.0

# 时间截只能转成标准字符串时间. 
# 不能直接转为自定义字符串时间, 可以先转成结构化时间, 再转成自定义字符串时间
# ctime(seconds) -> string
>>> time.ctime(1521505668.901931)
'Tue Mar 20 08:27:48 2018'
```

常见问题:

```
# 今天在这周是星期几
>>> print t.strftime('%w')
4

# 今天是今年的第几天
>>> print t.strftime('%j')
239

# 这周是今年的第几周
>>> print t.strftime('%U')
34
```

</br>

**datetime**

datetime主要有4种时间类型

    `datetime.date`：表示日期的类。常用的属性有year, month, day
    `datetime.time`：表示时间的类。常用的属性有hour, minute, second, microsecond
    `datetime.datetime`：表示日期时间
    `datetime.timedelta`：表示时间间隔，即两个时间点之间的长度

***datetime.date***

表示日期的类。常用的属性有year,month,day

代码演示:

```
# 获得datetime.date类型
>>> datetime.date.today()
datetime.date(2018, 3, 20)   # type: datetime.date
>>> datetime.date(2018,1,1)
datetime.date(2018, 1, 1)
```

***datetime.time***

表示时间的类。常用的属性有hour,minute,second,microsecond

代码演示:

```
>>> datetime.time(12,30,59,99)
datetime.time(12,30,59,99)
```

***datetime.datetime***

表示日期时间

代码演示:

```
>>> datetime.datetime.now()
datetime.datetime(2018, 3, 20, 9, 11, 2, 94777)
>>> datetime.datetime.today()
datetime.datetime(2018, 3, 20, 9, 12, 26, 22006)
>>> datetime.datetime(2018,1,1,10,10,10,1000)
datetime.datetime(2018, 1, 1, 10, 10, 10, 1000)
```

***datetime.timedelta***

表示时间间隔，两个时间点之间的长度

timedelta([days[, seconds[, microseconds[, milliseconds[, minutes[, hours[, weeks]]]]]]])

代码演示:

```
>>> datetime.datetime.now()
datetime.datetime(2018, 3, 20, 9, 15, 26, 809166)
>>> datetime.datetime.now() + datetime.timedelta(days=10, hours=5)
datetime.datetime(2018, 3, 30, 14, 15, 28, 978371)

# 将字符串时间格式化转化为时间
>>> str_to_date = datetime.datetime.strptime("16/11/17 16:30","%d/%m/%y%H:%M") 
>>> str_to_date
datetime.datetime(2017, 11, 16, 16, 30)
# 提取10个小时
>>> datetime.datetime.now() + datetime.timedelta(hours=-10) 
datetime.datetime(2017, 5, 28, 20, 1, 11, 805686)
```

</br>

**time与datetime之间的互相转换**

date.fromtimestamp(timestamp)：根据给定的时间戮，返回一个date对象

```
>>> datetime.datetime.fromtimestamp(time.time()) 
datetime.datetime(2013, 8, 10, 11, 14, 50, 842812)
```

time_struct与datetime之间的转换可以通过中间状态string来完成



### 13. `inspect`

[关于python中inspect模块的一些探究](https://blog.csdn.net/weixin_35955795/article/details/53053762)

[python的inspect模块](https://www.cnblogs.com/walkerwang/archive/2011/08/03/2125903.html)

[inspect模块详解](https://www.cnblogs.com/mosson/p/7244480.html)

根据度娘搜到的，inspect模块主要提供了四种用处：

(1). 对是否是模块，框架，函数等进行类型检查。

(2). 获取源码

(3). 获取类或函数的参数的信息

(4). 解析堆栈


查看源文件发现它提供了不少好用的方法：
```
Here are some of the useful functions provided by this module:

ismodule(), isclass(), ismethod(), isfunction(), isgeneratorfunction(), 
isgenerator(), istraceback(), isframe(), iscode(), isbuiltin(),isroutine() – check object types

getmembers() – get members of an object that satisfy a given condition

getfile(), getsourcefile(), getsource() – find an object’s source code 
getdoc(), getcomments() – get documentation on an object 
getmodule() – determine the module that an object came from 
getclasstree() – arrange classes so as to represent their hierarchy

getargspec(), getargvalues() – get info about function arguments 
formatargspec(), formatargvalues() – format an argument spec 
getouterframes(), getinnerframes() – get info about frames 
currentframe() – get the current stack frame 
stack(), trace() – get info about frames on the stack or in a traceback 
```

**自我总结**

***获得函数的参数***

首先定义一些函数

```
def t1():
  pass

def t2(a):
  pass

def t3(b=1):
  pass

def t4(*c):
  pass

def t5(**d):
  pass

def t6(a,b=1,*c,**d):
  pass

```

`python2`：

```
>>> inspect.getargspec(t1)
ArgSpec(args=[], varargs=None, keywords=None, defaults=None)

>>> inspect.getargspec(t2)
ArgSpec(args=['a'], varargs=None, keywords=None, defaults=None)

>>> inspect.getargspec(t3)
ArgSpec(args=['b'], varargs=None, keywords=None, defaults=(1,))

>>> inspect.getargspec(t4)
ArgSpec(args=[], varargs='c', keywords=None, defaults=None)

>>> inspect.getargspec(t5)
ArgSpec(args=[], varargs=None, keywords='d', defaults=None)

>>> inspect.getargspec(t6)
ArgSpec(args=['a', 'b'], varargs='c', keywords='d', defaults=(1,))

```

`python3`:

python3与python2有所不同，比如定义函数：`def x(a, b=0, *c, d, e=1, **f)`，python3能够正确编译，
但python2就会报错：`SyntaxError: invalid syntax`。具体原因待会再讲，先来看看python3对参数的解析

python3中`inspect.getargspec`函数已经被舍弃，所以可以使用`inspect.getfullargspec`或者`inspect.signature`

```
>>> inspect.getfullargspec(t1)
FullArgSpec(args=[], varargs=None, varkw=None, defaults=None, kwonlyargs=[], kwonlydefaults=None, annotations={})

>>> inspect.getfullargspec(t2)
FullArgSpec(args=['a'], varargs=None, varkw=None, defaults=None, kwonlyargs=[], kwonlydefaults=None, annotations={})

>>> inspect.getfullargspec(t3)
 FullArgSpec(args=['b'], varargs=None, varkw=None, defaults=(1,), kwonlyargs=[], kwonlydefaults=None, annotations={})

>>> inspect.getfullargspec(t4)
FullArgSpec(args=[], varargs='c', varkw=None, defaults=None, kwonlyargs=[], kwonlydefaults=None, annotations={})

>>> inspect.getfullargspec(t5)
FullArgSpec(args=[], varargs=None, varkw='d', defaults=None, kwonlyargs=[], kwonlydefaults=None, annotations={})

>>> inspect.getfullargspec(t6)
FullArgSpec(args=['a', 'b'], varargs='c', varkw='d', defaults=(1,), kwonlyargs=[], kwonlydefaults=None, annotations={})

>>> def t7(a, b=0, *c, d, e=1, **f):
        pass

>>> inspect.getfullargspec(t7):
 FullArgSpec(args=['a', 'b'], varargs='c', varkw='f', defaults=(0,), kwonlyargs=['d', 'e'], kwonlydefaults={'e': 1}, annotations={})

# 使用inspect.signature

>>> x = inspect.signature(t7).parameters

>>> x
mappingproxy({'a': <Parameter "a">,
              'b': <Parameter "b=0">,
              'c': <Parameter "*c">,
              'd': <Parameter "d">,
              'e': <Parameter "e=1">,
              'f': <Parameter "**f">})

>>> for k,v in x.items():
        print("{}.kind: {} ({})".format(k, v.kind, v.kind.name))

a.kind: 1 (POSITIONAL_OR_KEYWORD)
b.kind: 1 (POSITIONAL_OR_KEYWORD)
c.kind: 2 (VAR_POSITIONAL)
d.kind: 3 (KEYWORD_ONLY)
e.kind: 3 (KEYWORD_ONLY)
f.kind: 4 (VAR_KEYWORD)
```

对比python2和python3的结果，我们发现python2中参数有3种类型：`args`(位置参数或关键字参数), `varargs`(可变位置参数), `keywords`(可变关键字参数)；而python3中的参数有4种(其实是5种)类型：`args`(位置参数或关键字参数), `varargs`(可变位置参数), `varkw`(可变关键字参数), `kwonlyargs`(关键字参数)，而且python3还专门为这几种参数类型设置了数据类型：

```
>>> inspect._ParameterKind.__members__
mappingproxy({'KEYWORD_ONLY': <_ParameterKind.KEYWORD_ONLY: 3>,
              'POSITIONAL_ONLY': <_ParameterKind.POSITIONAL_ONLY: 0>,
              'POSITIONAL_OR_KEYWORD': <_ParameterKind.POSITIONAL_OR_KEYWORD: 1>,
              'VAR_KEYWORD': <_ParameterKind.VAR_KEYWORD: 4>,
              'VAR_POSITIONAL': <_ParameterKind.VAR_POSITIONAL: 2>})

# POSITIONAL_ONLY ： 位置参数 (0)
# POSITIONAL_OR_KEYWORD ： 位置或关键字参数 (1)
# VAR_POSITIONAL ： 可变位置参数 (2)
# KEYWORD_ONLY ： 关键字参数 (3)
# VAR_KEYWORD ： 可变关键字参数 (4)

```

### 14. operator

[operator 模块简单介绍](https://www.cnblogs.com/nju2014/p/5568139.html)

简单介绍几个常用的函数，其他的请参考[文档](https://docs.python.org/2/library/operator.html#operator.delitem)。

`operator.concat(a, b)`: 对于 a、b序列，返回 a + b(列表合并）

`operator.countOf(a, b)`: 返回 b 在 a 中出现的次数

`operator.delitem(a, b)`: 删除 a 中索引为 b 的值

`operator.getitem(a, b)`: 返回 a 中索引为 b 的值

`operator.indexOf(a, b)`: 返回 b 在 a 中首次出现位置的索引值。

`operator.setitem(a, b, c)`: 设置 a 中索引值为 b 的项目值更改为 c

operator 模块也为属性和项目的查找提供了一些工具。这些工具使得 map(), sorted(), itertools.groupby() 或其他函数 需要的参数的提取更方便更快速。上面的函数有一个共同点，即均接受函数参数。

`operator.attrgetter(attr)`, `operator.attrgetter(*attrs)`: 返回一个可调用的对象，该对象从运算中获取 'attr' 。如果请求的属性不止一个的话， 返回属性的元组。这些属性的名字可以包括 '.'。比如：

`f = attrgetter('name')`: 调用 `f(b)` 返回 `b.name`

`f = attrgetter('name', 'date')`: 调用 `f(b)` 返回 `(b.name, b.date)`

`f = attrgetter('name.first', 'name.last')`: 调用 `f(b)` 返回 `(b.name.first, b.name.last)`

`operator.itemgetter(item)`, `operator.itemgetter(*items)`: 返回一个可调用的对象，该对象通过运算符的 __getitem__()的方法 从运算中获取 item 。如果指定了多个 item ， 返回查找值的元组。比如：

`f = itemgetter(2)`: 调用 `f(r)` 返回 `r[2]`

`g = itemgetter(2, 5, 3)`, 调用 `f(r)` 返回 `(r[2], r[3], r[3])`

相当于：

```
def itemgetter(*items):
    if len(items) == 1:
        item = items[0]
        def g(obj):
            return obj[item]
    else:
        def g(obj):
            return tuple(obj[item] for item in items)
    return g
```   
 
运算符的`__getitem__()`方法可接受任意类型的项目。字典接收任意的哈希值。列表、元组和字符串接收一个索引或字符片段。

```
>>> itemgetter(1)('ABCDEFG')
'B'
>>> itemgetter(1,3,5)('ABCDEFG')
('B', 'D', 'F')
>>> itemgetter(slice(2,None))('ABCDEFG')
'CDEFG'
```

使用 `itemgetter()` 从元组序列中获取指定的域值，比如：

```
>>> inventory = [('apple', 3), ('banana', 2), ('pear', 5), ('orange', 1)]
>>> getcount = itemgetter(1)
>>> map(getcount, inventory)
[3, 2, 5, 1]
>>> sorted(inventory, key=getcount)
[('orange', 1), ('banana', 2), ('apple', 3), ('pear', 5)]
```

`operator` 相关的信息对应如下：

|名称|符号|函数|
|----|----|----|
|Operation|Syntax|Function|
|Addition|a + b|add(a, b)|
|Concatenation|seq1 + seq2|concat(seq1, seq2)|
|Containment Test|obj in seq|contains(seq, obj)|
|Division|a / b|div(a, b) (without future.division)|
|Division|a / b|truediv(a, b) (with future.division)|
|Division|a // b|floordiv(a, b)|
|Bitwise And|a & b|and_(a, b)|
|Bitwise Exclusive Or|a ^ b|xor(a, b)|
|Bitwise Inversion|~ a|invert(a)|
|Bitwise Or|a b|or_(a, b)|
|Exponentiation|a ** b|pow(a, b)|
|Identity|a is b|is_(a, b)|
|Identity|a is not b|is_not(a, b)|
|Indexed Assignment|obj[k] = v|setitem(obj, k, v)|
|Indexed Deletion|del obj[k]|delitem(obj, k)|
|Indexing|obj[k]|getitem(obj, k)|
|Left Shift|a << b|lshift(a, b)|
|Modulo|a % b|mod(a, b)|
|Multiplication|a * b|mul(a, b)|
|Negation (Arithmetic)|- a|neg(a)|
|Negation (Logical)|not a|not_(a)|
|Positive|+ a|pos(a)|
|Right Shift|a >> b|rshift(a, b)|
|Sequence Repetition|seq * i|repeat(seq, i)|
|Slice Assignment|seq[i:j] = values|setitem(seq, slice(i, j), values)|
|Slice Deletion|del seq[i:j]|delitem(seq, slice(i, j))|
|Slicing|seq[i:j]|getitem(seq, slice(i, j))|
|String Formatting|s % obj|mod(s, obj)|
|Subtraction|a - b|sub(a, b)|
|Truth Test|obj|truth(obj)|
|Ordering|a < b|lt(a, b)|
|Ordering|a <= b|le(a, b)|
|Equality|a == b|eq(a, b)|
|Difference|a != b|ne(a, b)|
|Ordering|a >= b|ge(a, b)|
|Ordering|a > b|gt(a, b)|



### 15. contextlib

[contextlib-廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001478651770626de401ff1c0d94f379774cabd842222ff000)

[详解Python中contextlib上下文管理模块的用法-脚本之家](http://www.jb51.net/article/87533.htm)

[python上下文管理器ContextLib及with语句-CSDN](https://blog.csdn.net/pipisorry/article/details/50444736)


### 16. PIL

[基于Python的PIL库的学习（一）](https://blog.csdn.net/louishao/article/details/69879981)

[python PIL 图像处理 （二）](https://blog.csdn.net/u013378306/article/details/70156842)

[python，使用PIL库对图片进行操作](https://www.cnblogs.com/meitian/p/3699223.html)

[python使用pil在图片上添加中文文字](http://outofmemory.cn/code-snippet/6640/python-draw-chinese-text-with-pil)

代码实战

```
from PIL import Image, ImageDraw, ImageFont

p1 = "../callcnv/14E023-05.cnv.chr1.png"
p2 = "../callcnv/14E023-05.cnv.chr2.png"

i1 = Image.open(p1)
i2 = Image.open(p2)

w, h = i1.size

# 裁剪图片
region = (0, 0, w, h/2)
i2 = i2.crop(region)

# 粘贴图片
i1.paste(i2, (0, int(h/2)))

# 添加字体
font = ImageFont.truetype('simsun.ttc',24)
draw = ImageDraw.Draw(i1)
draw.text( (0,50), unicode(txt,'UTF-8'), font=font)
del draw

# 缩小图片
i1 = i1.resize((int(w/2), int(h/2)))

# 显示图片
#i1.show()

# 保存图片
i1.save("merge.png")
```


### 17. re

[python3正则表达式的几个高级用法](https://blog.csdn.net/isscollege/article/details/80138158)


**1. 数组分组**

每一段正则用一个加圆括起来时，便自动构成一个组，包括(?Ppattern)自定义命名组，也加入到分组序号中 
如果后面有前面圆括中相同部分，则用数字序号表示匹配相同部分 
`r'(正则1)…(正则2)…(正则3) ... \1….\2….\3…'`, 
这里出现`\1`，表示匹配前面第1个圆括号正则内容， 
这里出现`\2`，表示匹配前面第2个圆括号正则内容

```
re.sub(r"(\d+) *(\d+)", r"\1,\2", "[34 22]")
#结果为："[34,22]"
```


### 18. struct 解析二进制或socket数据

* [Python使用struct处理二进制 解析二进制数据 解析socket数据](https://blog.csdn.net/a382486075/article/details/54973612)
* [Python解析二进制文件](https://blog.csdn.net/lovelyaiq/article/details/81988185)




</br>

## 第三方模块

### 1. `scipy.stats`

Scipy的stats模块包含了多种概率分布的随机变量，随机变量分为连续的和离散的两种。
SciPy的stats模块提供了大约80种连续随机变量和10多种离散分布变量，这些分布都依赖于numpy.random函数。

**所有的连续随机变量都是`rv_continuous`的派生类的对象**

|对象方法|说明|
| ----- | ---- |
| rv_continuous([momtype, a, b, xtol, ...]) | A generic continuous random variable class meant for subclassing. |
| rv_continuous.pdf(x, \*args, \*\*kwds) | Probability density function at x of the given RV. <br> 随机变量的概率密度函数 |
| rv_continuous.logpdf(x, \*args, \*\*kwds) | Log of the probability density function at x of the given RV. <br> 概率密度函数的对数 |
| rv_continuous.cdf(x, \*args, \*\*kwds) | Cumulative distribution function of the given RV. <br> 随机变量的累积分布函数 |
| rv_continuous.logcdf(x, \*args, \*\*kwds) | Log of the cumulative distribution function at x of the given RV. <br> 累积分布函数的对数 |
| rv_continuous.sf(x,\ *args, \*\*kwds) | Survival function (1-cdf) at x of the given RV. <br> 随机变量的生存函数(1-cdf) |
| rv_continuous.logsf(x, \*args, \*\*kwds) | Log of the survival function of the given RV. <br> 生存函数的对数 |
| rv_continuous.ppf(q, \*args, \*\*kwds) | Percent point function (inverse of cdf) at q of the given RV. <br> 百分点函数(累积分布函数的反函数) <br> ppf(0.01)为当分布的累积面积达到0.01时对应的x0值，ppf(0.99)为当分布的累积面积达到0.99时对应的x1值，np.linspace(ppf(0.01)，ppf(0.99)) 为获得x0-x1之间的100个值（包含x0和x1）|
| rv_continuous.isf(q, \*args, \*\*kwds) | Inverse survival function at q of the given RV. <br> 生存函数的反函数 |
| rv_continuous.moment(n, \*args, \*\*kwds) | n’th order non-central moment of distribution. <br> n阶非中心矩分布 |
| rv_continuous.stats(\*args, \*\*kwds) | Some statistics of the given RV |
| rv_continuous.entropy(\*args, \*\*kwds) | Differential entropy of the RV. <br> 微分商 |
| rv_continuous.fit(data, \*args, \*\*kwds) | Return MLEs for shape, location, and scale parameters from data. <br> 对一组随机取样进行拟合，找出最适合取样数据的概率密度函数的系数 |
| rv_continuous.expect([func, args, loc, ...]) | Calculate expected value of a function with respect to the distribution. <br> 计算相对于分布的函数的预期值。 |
 
<br>可以通过如下语句获得stats模块中所有的连续随机变量，示例代码：
```
from scipy import stats 
[k for k, v in stats.__dict__.items() if isinstance(v, stats.rv_continuous)]
```
结果为：`ksone`, `kstwobign`, `norm`, `alpha`, `anglit`, `arcsine`, `beta`, `betaprime`, `bradford`, `burr`, `burr12`, `fisk`, `cauchy`, `chi`, `chi2`, `cosine`, `dgamma`, `dweibull`, `expon`, `exponnorm`, `exponweib`, `exponpow`, `fatiguelife`, `foldcauchy`, `f`, `foldnorm`, `frechet_r`, `weibull_min`, `frechet_l`, `weibull_max`, `genlogistic`, `genpareto`, `genexpon`, `genextreme`, `gamma`, `erlang`, `gengamma`, `genhalflogistic`, `gompertz`, `gumbel_r`, `gumbel_l`, `halfcauchy`, `halflogistic`, `halfnorm`, `hypsecant`, `gausshyper`, `invgamma`, `invgauss`, `invweibull`, `johnsonsb`, `johnsonsu`, `laplace`, `levy`, `levy_l`, `levy_stable`, `logistic`, `loggamma`, `loglaplace`, `lognorm`, `gilbrat`, `maxwell`, `mielke`, `kappa4`, `kappa3`, `nakagami`, `ncx2`, `ncf`, `t`, `nct`, `pareto`, `lomax`, `pearson3`, `powerlaw`, `powerlognorm`, `powernorm`, `rdist`, `rayleigh`, `reciprocal`, `rice`, `recipinvgauss`, `semicircular`, `skewnorm`, `trapz`, `triang`, `truncexpon`, `truncnorm`, `tukeylambda`, `uniform`, `vonmises`, `vonmises_line`, `wald`, `wrapcauchy`, `gennorm`, `halfgennorm`
 
<br>下面以标准正态分布（函数表示f(x)=(1/√2π)exp(-x^2/2)）为例，简单介绍随机变量的用法。示例代码：
```
from scipy import stats 
# 设置正态分布参数，其中loc是期望值参数，scale是标准差参数 
X = stats.norm(loc=1.0, scale=2.0) 
# 计算随机变量的期望值和方差 
print(X.stats())
```
运行结果：`(array(1.0), array(4.0))`
 
<br>以上代码说明，norm可以像函数一样调用，通过loc和scale参数可以指定随机变量的偏移和缩放参数。对于正态分布的随机变量来说，这两个参数相当于指定其期望值和标准差，标准差是方差的算术平方根。X的stats()方法，可以计算随机变量X分布的特征值，如期望值和方差。
此外，通过调用随机变量X的rvs()方法，可以得到包含一万次随机取样值的数组x，然后调用NumPy的mean()和var()计算此数组的均值和方差，其结果符合随机变量X的特性，示例代码：
```
#对随机变量取10000个值 
x = X.rvs(size=10000) 
print(np.mean(x), np.var(x))
```
运行结果：`(1.0287787687588861, 3.9944276709242805)`

<br>使用fit()方法对随机取样序列x进行拟合，它返回的是与随机取样值最吻合的随机变量参数，示例代码：
```
#输出随机序列的期望值和标准差 
print(stats.norm.fit(x))
```
运行结果：`(1.0287787687588861, 1.998606432223283)`

<br>在下面的例子中，计算取样值x的直方图统计以及累计分布，并与随机变量的概率密度函数和累积分布函数进行比较。示例代码：
```
pdf, t = np.histogram(x, bins=100, normed=True)  #pdf为直方图柱子的高度，t为x轴上所有柱子的起始点+最后一个柱子的终止点（个数为柱子数+1）
t = (t[:-1]+t[1:])*0.5    #求各柱子在x轴的中心点
cdf = np.cumsum(pdf) * (t[1] - t[0])  #求各柱子在y轴的累积值
p_error = pdf - X.pdf(t) 
c_error = cdf - X.cdf(t) 
print("max pdf error: {}, max cdf error: {}".format(np.abs(p_error).max(), np.abs(c_error).max()))
```
运行结果：`max pdf error: 0.0208405611169, max cdf error: 0.0126874590568`

<br>通过绘图的方式查看概率密度函数求得的理论值（theory value）和直方图统计值（statistic value）的结果，可以看出二者是一致的，示例代码：
```
import pylab as pl 
pl.plot(t, pdf, color="green", label = "statistic value") 
pl.plot(t, X.pdf(t), color="yellow", label ="theory value") 
pl.legend(loc = "best")
pl.show()
```
绘图如下：
<img src="http://upload-images.jianshu.io/upload_images/5013892-1fec19f2ce74db40.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" width = "500" height = "500" />

<br>也可以用同样的方式显示随机变量X的累积分布和数组pdf的累加结果，示例代码：
```
import pylab as pl 
pl.plot(t, cdf, color="green", label = "statistic value") 
pl.plot(t, X.cdf(t), color="yellow", label ="theory value") 
pl.legend(loc = "best") 
pl.show()
```
绘图如下：
<img src="http://upload-images.jianshu.io/upload_images/5013892-8926b550b4ef6c10.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" width = "500" height = "500" />


<br><br>**而所有的离散随机变量都是`rv_discrete`的派生类的对象。**

| 对象方法 | 说明 |
| ---- | ---- |
| rv_discrete([a, b, name, badvalue, ...]) | A generic discrete random variable class meant for subclassing. |
| rv_discrete.rvs(\*args, \*\*kwargs) | Random variates of given type. <br> 对随机变量进行随机取值，通过size参数指定输出数组的大小 |
| rv_discrete.pmf(k, \*args, \*\*kwds) | Probability mass function at k of the given RV. <br> 概率质量函数 |
| rv_discrete.logpmf(k, \*args, \*\*kwds) | Log of the probability mass function at k of the given RV. <br> 概率质量函数的对数 |
| rv_discrete.cdf(k, \*args, \*\*kwds) | Cumulative distribution function of the given RV. <br> 累积分布函数 |
| rv_discrete.logcdf(k, \*args, \*\*kwds) | Log of the cumulative distribution function at k of the given RV <br> 累积分布函数的对数 |
| rv_discrete.sf(k, \*args, \*\*kwds) | Survival function (1-cdf) at k of the given RV. <br> 生存函数(1-cdf)  |
| rv_discrete.logsf(k, \*args, \*\*kwds) | Log of the survival function of the given RV. <br> 生存函数的对数 |
| rv_discrete.ppf(q, \*args, \*\*kwds) | Percent point function (inverse of cdf) at q of the given RV <br> 百分点函数(累积分布函数的反函数) |
| rv_discrete.isf(q, \*args, \*\*kwds) | Inverse survival function (1-sf) at q of the given RV. <br> 生存函数的反函数 |
| rv_discrete.stats(\*args, \*\*kwds) | Some statistics of the given RV |
| rv_discrete.moment(n, \*args, \*\*kwds) | n’th order non-central moment of distribution. |
| rv_discrete.entropy(\*args, \*\*kwds) | Differential entropy of the RV. <br> 微分商 |
| rv_discrete.expect([func, args, loc, lb, ...]) | Calculate expected value of a function with respect to the distribution  <br> 计算相对于分布的函数的预期值 |

<br>投掷有六个面的骰子时，只能获得1到6的整数，因此所得到的概率分布是离散的。我们以值域离散的分布称为离散概率分布，包括泊松分布、二项分布、几何分布等。通常使用概率质量函数（PMF）描述其分布情况，如几何分布函数PMF=(1-p)<sup>(k-1)</sup>p。
在stats模块中所有描述离散分布的随机变量都从rv_discrete类继承，也可以直接用rv_discrete类自定义离散概率分布。假设有一个不均匀的骰子，其各点出现的概率不相等，我们用如下代码定义其分布，示例代码：
```
# 数组x保存骰子的所有可能值，数组p保存每个值出现的概率 
x = range(1, 7) 
p = (0.4, 0.2, 0.1, 0.1, 0.1, 0.1) 
 # 创建表示这个骰子的随机变量dice，调用其rvs()方法投掷此骰子20次，获得符合概率p的随机数 
dice = stats.rv_discrete(values=(x, p)) 
print(dice.rvs(size=20))
```
运行结果：`array([3, 6, 4, 5, 5, 2, 1, 3, 3, 1, 1, 3, 1, 5, 1, 3, 4, 1, 2, 2])`

<br>除了自定义离散概率分布，我们也可以利用stats模块里的函数定义各种分布。下面以生成几何分布为例，其函数是geom()，示例代码：
```
import numpy as np 
from scipy.stats import geom 
 # 设置几何分布的参数 
p = 0.5 
dist = geom(p) 
 # 设置样本区间   
x = np.linspace(0, 5, 1000)   
 # 得到几何分布的 PMF 和CDF   
pmf = dist.pmf(x) 
 cdf = dist.cdf(x)   
 # 生成500个随机数   
sample = dist.rvs(500)
```

<br><br>**连续分布**

| 分布 | 描述 |
| ---- | ---- |
| alpha | An alpha continuous random variable. <br> α分布 |
| anglit | An anglit continuous random variable. |
| arcsine | An arcsine continuous random variable. <br> 反正弦分布 |
| beta | A beta continuous random variable. <br> β分布 |
| betaprime | A beta prime continuous random variable. <br> β初始分布 |
| bradford | A Bradford continuous random variable. <br> 布拉德福德分布 |
| burr | A Burr continuous random variable. <br> 伯尔分布 |
| cauchy | A Cauchy continuous random variable. <br> 柯西分布 |
| chi | A chi continuous random variable. |
| chi2 | A chi-squared continuous random variable. <br> 卡方分布 |
| cosine | A cosine continuous random variable. <br> 余弦分布 |
| dgamma | A double gamma continuous random variable. <br> 双伽马分布 |
| dweibull | A double Weibull continuous random variable. <br> 双威布尔分布 |
| erlang | An Erlang continuous random variable. |
| expon | An exponential continuous random variable. <br> 指数分布 |
| exponweib | An exponentiated Weibull continuous random variable. <br> 指数威布尔分布 |
| exponpow | An exponential power continuous random variable. <br> 指数幂分布 |
| f | An F continuous random variable. <br> F分布 |
| fatiguelife | A fatigue-life (Birnbaum-Sanders) continuous random variable. <br> 疲劳寿命(伯恩鲍姆-桑德斯)分布 |
| fisk | A Fisk continuous random variable. <br> 菲斯克分布 |
| foldcauchy | A folded Cauchy continuous random variable. <br> 折叠柯西分布 |
| foldnorm | A folded normal continuous random variable. <br> 折叠正态分布 | 
| frechet_r | A Frechet right (or Weibull minimum) continuous random variable. <br> Frechet右(威布尔最小值)分布 |
| frechet_l | A Frechet left (or Weibull maximum) continuous random variable. <br> Frechet左(威布尔最大值)分布 |
| genlogistic | A generalized logistic continuous random variable. <br> 广义逻辑分布 |
| genpareto | A generalized Pareto continuous random variable. <br> 广义帕累托分布 |
| genexpon | A generalized exponential continuous random variable. <br> 广义指数分布 |
| genextreme | A generalized extreme value continuous random variable. <br> 广义极值分布 |
| gausshyper | A Gauss hypergeometric continuous random variable. <br> 高斯超几何分布 |
| gamma | A gamma continuous random variable. <br> 伽马分布 |
| gengamma | A generalized gamma continuous random variable. <br> 广义伽马分布 |
| genhalflogistic | A generalized half-logistic continuous random variable. <br> 广义半对数分布 |
| gilbrat | A Gilbrat continuous random variable. <br> 吉尔布拉特分布 |
| gompertz | A Gompertz (or truncated Gumbel) continuous random variable. <br> 姜氏(或者截断冈贝尔)分布 |
| gumbel_r | A right-skewed Gumbel continuous random variable. <br> 右倾冈贝尔分布 |
| gumbel_l | A left-skewed Gumbel continuous random variable. <br> 左倾冈贝尔分布 |
| halfcauchy | A Half-Cauchy continuous random variable. <br> 半柯西分布 |
| halflogistic | A half-logistic continuous random variable. <br> 半逻辑分布 |
| halfnorm | A half-normal continuous random variable. <br> 半正态分布 |
| hypsecant | A hyperbolic secant continuous random variable. <br> 双曲正割分布 |
| invgamma | An inverted gamma continuous random variable. <br> 反伽马分布 |
| invgauss | An inverse Gaussian continuous random variable. <br> 反高斯分布 |
| invweibull | An inverted Weibull continuous random variable. <br> 倒置威布尔分布 |
| johnsonsb | A Johnson SB continuous random variable. <br> 约翰逊SB分布 |
| johnsonsu | A Johnson SU continuous random variable. <br> 约翰逊SU分布 |
| ksone | General Kolmogorov-Smirnov one-sided test. |
| kstwobign | Kolmogorov-Smirnov two-sided test for large N. |
| laplace | A Laplace continuous random variable. <br> 拉普拉斯分布 |
| logistic | A logistic (or Sech-squared) continuous random variable. <br> 逻辑分布 |
| loggamma | A log gamma continuous random variable. <br> 对数伽玛分布 |
| loglaplace | A log-Laplace continuous random variable. <br> 对数拉普拉斯分布 |
| lognorm | A lognormal continuous random variable.  <br> 对数正态分布分布 |
| lomax | A Lomax (Pareto of the second kind) continuous random variable.  <br> 洛马克斯（第二种帕累托）分布 |
| maxwell | A Maxwell continuous random variable.  <br> 麦克斯韦分布 |
| mielke | A Mielke’s Beta-Kappa continuous random variable.  <br> 米尔克的β-卡帕分布 |
| nakagami | A Nakagami continuous random variable. |
| ncx2 | A non-central chi-squared continuous random variable.  <br> 非中心卡方分布 |
| ncf | A non-central F distribution continuous random variable.   <br> 非中心F分布 |
| nct | A non-central Student’s T continuous random variable.  <br> 非中心Student’s T分布 |
| norm | A normal continuous random variable.  <br> 正态分布分布 |
| pareto | A Pareto continuous random variable.  <br> 帕累托分布 |
| pearson3 | A pearson type III continuous random variable. <br>  III型皮尔森分布 |
| powerlaw | A power-function continuous random variable. |
| powerlognorm | A power log-normal continuous random variable. |
| powernorm | A power normal continuous random variable. |
| rdist | An R-distributed continuous random variable.  <br> R-分布分布 |
| reciprocal | A reciprocal continuous random variable.  <br> 倒数分布 |
| rayleigh | A Rayleigh continuous random variable.  <br> 瑞利分布 |
| rice | A Rice continuous random variable. |
| recipinvgauss | A reciprocal inverse Gaussian continuous random variable. |
| semicircular | A semicircular continuous random variable. |
| t | A Student’s T continuous random variable. <br> Student’s T |
| triang | A triangular continuous random variable.  <br> 三角形分布 |
| truncexpon | A truncated exponential continuous random variable.  <br> 截断指数分布 |
| truncnorm | A truncated normal continuous random variable.  <br> 截断正态分布 |
| tukeylambda | A Tukey-Lamdba continuous random variable.  <br> 杜克 -Lamdba分布 |
| uniform | A uniform continuous random variable.  <br> 均匀分布 |
| vonmises | A Von Mises continuous random variable.  <br> 冯米塞斯分布 |
| wald | A Wald continuous random variable.  <br> 沃尔德分布 |
| weibull_min | A Frechet right (or Weibull minimum) continuous random variable. |
| weibull_max | A Frechet left (or Weibull maximum) continuous random variable. |
| wrapcauchy | A wrapped Cauchy continuous random variable. |

<br><br>**多变量分布**

| 分布 | 描述 |
| ---- | ---- |
| multivariate_normal | A multivariate normal random variable. <br> 多元正态分布 |

<br><br>**离散分布**

| 分布 | 描述 |
| ---- | ---- |
| bernoulli | A Bernoulli discrete random variable. <br> 伯努利分布 |
| binom | A binomial discrete random variable. <br> 二项式分布 |
| boltzmann | A Boltzmann (Truncated Discrete Exponential) random variable. <br> 玻尔兹曼分布 |
| dlaplace | A Laplacian discrete random variable. <br> 拉普拉斯分布 |
| geom | A geometric discrete random variable. <br> 几何分布 |
| hypergeom | A hypergeometric discrete random variable. <br> 超几何分布 |
| logser | A Logarithmic (Log-Series, Series) discrete random variable. <br> 对数分布 |
| nbinom | A negative binomial discrete random variable. <br> 负二项式分布 |
| planck | A Planck discrete exponential random variable. <br> 普朗克离散指数分布 |
| poisson | A Poisson discrete random variable. <br> 泊松分布 |
| randint | A uniform discrete random variable. <br> 均匀分布 |
| skellam | A Skellam discrete random variable. <br> |
| zipf | A Zipf discrete random variable. <br> 齐普夫分布 |

<br><br>**统计方法**

| 方法 | 描述 |
| --- | --- |
| describe(a[, axis]) | Computes several descriptive statistics of the passed array. <br> 计算传递数组的几个描述性统计信息 |
| gmean(a[, axis, dtype]) | Compute the geometric mean along the specified axis. <br>  计算指定轴的几何平均值 |
| hmean(a[, axis, dtype]) | Calculates the harmonic mean along the specified axis. <br> 计算沿指定轴的调和平均值 |
| kurtosis(a[, axis, fisher, bias]) | Computes the kurtosis (Fisher or Pearson) of a dataset. <br> 计算数据集的峰度（Fisher或Pearson） |
| kurtosistest(a[, axis]) | Tests whether a dataset has normal kurtosis <br> 测试数据集是否具有正常峰度 |
| mode(a[, axis]) | Returns an array of the modal (most common) value in the passed array. <br> 返回数组中模（最常见）值数组 |
| moment(a[, moment, axis]) | Calculates the nth moment about the mean for a sample. <br> 计算样本平均值的第n个矩 |
| normaltest(a[, axis]) | Tests whether a sample differs from a normal distribution. <br> 测试样本是否与正态分布不同 |
| skew(a[, axis, bias]) | Computes the skewness of a data set. <br> 计算数据集的偏度 |
| skewtest(a[, axis]) | Tests whether the skew is different from the normal distribution. <br> 测试歪斜是否与正态分布不同 |
| tmean(a[, limits, inclusive]) | Compute the trimmed mean. <br> 计算修剪的均值 |
| tvar(a[, limits, inclusive]) | Compute the trimmed variance <br> 计算修剪的方差 |
| tmin(a[, lowerlimit, axis, inclusive]) | Compute the trimmed minimum <br> 计算修剪的最小值 |
| tmax(a[, upperlimit, axis, inclusive]) | Compute the trimmed maximum <br> 计算修剪的最大值 |
| tstd(a[, limits, inclusive]) | Compute the trimmed sample standard deviation <br> 计算修剪的样本标准偏差 |
| tsem(a[, limits, inclusive]) | Compute the trimmed standard error of the mean. <br> 计算平均值的修剪标准误差 |
| nanmean(x[, axis]) | Compute the mean over the given axis ignoring nans. <br> 计算给定坐标轴上的平均值，忽略nans |
| nanstd(x[, axis, bias]) | Compute the standard deviation over the given axis, ignoring nans. <br> 计算给定轴上的标准偏差，忽略nans |
| nanmedian(x[, axis]) | Compute the median along the given axis ignoring nan values. <br> 计算沿给定轴的中位数，忽略nan值 |
| variation(a[, axis]) | Computes the coefficient of variation, the ratio of the biased standard deviation to the mean. <br> 计算变异系数，偏差标准偏差与平均值的比率 |
| cumfreq(a[, numbins, defaultreallimits, weights]) | Returns a cumulative frequency histogram, using the histogram function. <br> 使用直方图函数返回累积频率直方图 |
| histogram2(a, bins) | Compute histogram using divisions in bins. <br>使用分箱计算直方图 |
| histogram(a[, numbins, defaultlimits, ...]) | Separates the range into several bins and returns the number of instances in each bin. <br> 将范围分成几个分箱并返回每个分箱中的实例数量 |
| itemfreq(a) | Returns a 2-D array of item frequencies. <br> 返回项目频率的二维数组 |
| percentileofscore(a, score[, kind]) | The percentile rank of a score relative to a list of scores. <br> 打分列表中的打分的百分比等级 |
| scoreatpercentile(a, per[, limit, ...]) | Calculate the score at a given percentile of the input sequence. <br> 计算输入序列给定百分位数的得分 |
| relfreq(a[, numbins, defaultreallimits, weights]) | Returns a relative frequency histogram, using the histogram function. <br> 使用直方图函数返回相对频率直方图 |
| binned_statistic(x, values[, statistic, ...]) | Compute a binned statistic for a set of data. <br> 计算一组数据的分箱统计量 |
| binned_statistic_2d(x, y, values[, ...]) | Compute a bidimensional binned statistic for a set of data. <br> 计算一组数据的二维分箱统计量 |
| binned_statistic_dd(sample, values[, ...]) | Compute a multidimensional binned statistic for a set of data. <br> 计算一组数据的多维分箱统计量 |
| obrientransform(*args) | Computes the O’Brien transform on input data (any number of arrays). <br> 计算输入数据（任意数量的数组）上的O'Brien变换 |
| signaltonoise(a[, axis, ddof]) | The signal-to-noise ratio of the input data. <br> 输入数据的信噪比 |
| bayes_mvs(data[, alpha]) | Bayesian confidence intervals for the mean, var, and std. <br> 平均值，var和std的贝叶斯置信区间 |
| sem(a[, axis, ddof]) | Calculates the standard error of the mean (or standard error of measurement) of the values in the input array. <br> 计算输入数组中值的标准误差（或测量的标准误差） |
| zmap(scores, compare[, axis, ddof]) | Calculates the relative z-scores. <br> 计算相对z打分 |
| zscore(a[, axis, ddof]) | Calculates the z score of each value in the sample, relative to the sample mean and standard deviation. <br> 计算样本中每个值相对于样本均值和标准偏差的z值 |
| sigmaclip(a[, low, high]) | Iterative sigma-clipping of array elements. <br> 数组元素的迭代Σ-剪辑 |
| threshold(a[, threshmin, threshmax, newval]) | Clip array to a given value. <br> 将数组剪辑到给定的值 |
| trimboth(a, proportiontocut[, axis]) | Slices off a proportion of items from both ends of an array. <br> 从数组的两端切下一部分元素 |
| trim1(a, proportiontocut[, tail]) | Slices off a proportion of items from ONE end of the passed array distribution. <br> 从数组一端切下一部分元素 |
| f_oneway(*args) | Performs a 1-way ANOVA. <br> 执行单因素方差分析 |
| pearsonr(x, y) | Calculates a Pearson correlation coefficient and the p-value for testing non-correlation. <br> 计算Pearson相关系数和用于测试非相关性的p值 |
| spearmanr(a[, b, axis]) | Calculates a Spearman rank-order correlation coefficient and the p-value to test for non-correlation. <br> 计算Spearman排序相关系数和p值以测试非相关性 |
| pointbiserialr(x, y) | Calculates a point biserial correlation coefficient and the associated p-value. <br> 计算点双列相关系数和相关的p值 |
| kendalltau(x, y[, initial_lexsort]) | Calculates Kendall’s tau, a correlation measure for ordinal data. <br> 计算Kendall’s tau，一个有序数据的相关性度量 |
| linregress(x[, y]) | Calculate a regression line <br> 计算回归线 |
| ttest_1samp(a, popmean[, axis]) | Calculates the T-test for the mean of ONE group of scores. <br> 单样本T检验 |
| ttest_ind(a, b[, axis, equal_var]) | Calculates the T-test for the means of TWO INDEPENDENT samples of scores. <br> 两个独立样本的T检验 |
| ttest_rel(a, b[, axis]) | Calculates the T-test on TWO RELATED samples of scores, a and b. <br> 两个相关样本的T-检验 |
| kstest(rvs, cdf[, args, N, alternative, mode]) | Perform the Kolmogorov-Smirnov test for goodness of fit. <br> 检验拟合度的Kolmogorov-Smirnov检验 |
| chisquare(f_obs[, f_exp, ddof, axis]) | Calculates a one-way chi square test. <br> 计算一个单因素卡方检验 |
| power_divergence(f_obs[, f_exp, ddof, axis, ...]) | Cressie-Read power divergence statistic and goodness of fit test. <br> Cressie-Read权势分歧统计量和契合度检验 |
| ks_2samp(data1, data2) | Computes the Kolmogorov-Smirnov statistic on 2 samples. <br> 计算2样本的Kolmogorov-Smirnov统计量 |
| mannwhitneyu(x, y[, use_continuity]) | Computes the Mann-Whitney rank test on samples x and y. <br> 计算样本x和y的Mann-Whitney秩和检验 |
| tiecorrect(rankvals) | Tie correction factor for ties in the Mann-Whitney U and Kruskal-Wallis H tests. <br> 在Mann-Whitney U和Kruskal-Wallis H检验中的校正因子。 |
| rankdata(a[, method]) | Assign ranks to data, dealing with ties appropriately. <br> 数据排序，适当地处理关系 |
| ranksums(x, y) | Compute the Wilcoxon rank-sum statistic for two samples. <br> 计算两个样本的Wilcoxon秩和统计量 |
| wilcoxon(x[, y, zero_method, correction]) | Calculate the Wilcoxon signed-rank test. <br> 计算Wilcoxon秩检验 |
| kruskal(*args) | Compute the Kruskal-Wallis H-test for independent samples <br> 计算独立样本的Kruskal-Wallis H-检验 |
| friedmanchisquare(*args) | Computes the Friedman test for repeated measurements <br>  计算重复测量的Friedman检验 |
| ansari(x, y) | Perform the Ansari-Bradley test for equal scale parameters <br> 对等尺度参数执行Ansari-Bradley检验 |
| bartlett(*args) | Perform Bartlett’s test for equal variances <br> 执行Bartlett’s检验为方差齐性 |
| levene(*args, **kwds) | Perform Levene test for equal variances. <br> 进行Levene检验为方差齐性 |
| shapiro(x[, a, reta]) | Perform the Shapiro-Wilk test for normality. <br> 执行Shapiro-Wilk检验为正态 |
| anderson(x[, dist]) | Anderson-Darling test for data coming from a particular distribution <br> Anderson-Darling检验为来自特定分布的数据 |
| anderson_ksamp(samples[, midrank]) | The Anderson-Darling test for k-samples. <br> k-样本的Anderson-Darling检验 |
| binom_test(x[, n, p]) | Perform a test that the probability of success is p. <br> 进行检验，成功的概率是p |
| fligner(*args, **kwds) | Perform Fligner’s test for equal variances. <br>对Fligner检验为方差齐性  |
| mood(x, y[, axis]) | Perform Mood’s test for equal scale parameters. <br> 对同等比例参数进行Mood’s测试 |
| boxcox(x[, lmbda, alpha]) | Return a positive dataset transformed by a Box-Cox power transformation. <br> 返回由Box-Cox功率变换转换的正数据集 |
| boxcox_normmax(x[, brack, method]) | Compute optimal Box-Cox transform parameter for input data. <br> 计算输入数据的最佳Box-Cox变换参数 |
| boxcox_llf(lmb, data) | The boxcox log-likelihood function. <br> boxcox对数似然函数 |
| entropy(pk[, qk, base]) | Calculate the entropy of a distribution for given probability values. <br> 计算给定概率值的分布的熵 |

<br>SciPy中有超过60种统计函数。stats模块包括了诸如kstest 和normaltest等样本测试函数，用来检测样本是否服从某种分布。在使用这些工具前，要对数据有较好的理解，否则可能会误读它们的结果。样本分布检验为例，示例代码：
```
import numpy as np 
 from scipy import stats 
# 生成包括100个服从正态分布的随机数样本 
sample = np.random.randn(100) 
# 用normaltest检验原假设 
out = stats.normaltest(sample) 
print('normaltest output') 
print('Z-score = ' + str(out[0])) 
print('P-value = ' + str(out[1])) 
# kstest 是检验拟合度的Kolmogorov-Smirnov检验，这里针对正态分布进行检验

# D是KS统计量的值，越接近0越好 
out = stats.kstest(sample, 'norm') 
print('\nkstest output for the Normal distribution') 
print('D = ' + str(out[0])) 
print('P-value = ' + str(out[1])) 
# 类似地可以针对其他分布进行检验，例如Wald分布 
out = stats.kstest(sample, 'wald') 
print('\nkstest output for the Wald distribution') 
print('D = ' + str(out[0])) 
print('P-value = ' + str(out[1]))
```
<br> SciPy的stats模块中还提供了一些描述函数，如几何平均（gmean）、偏度（skew）、样本频数（itemfreq）等。示例代码：
```
import numpy as np 
from scipy import stats 
# 生成包括100个服从正态分布的随机数样本 
sample = np.random.randn(100)


# 调和平均数，样本值须大于0 
out = stats.hmean(sample[sample > 0]) 
print('Harmonic mean = ' + str(out)) 
# 计算-1到1之间样本的均值 
out = stats.tmean(sample, limits=(-1, 1)) 
print('\nTrimmed mean = ' + str(out)) 
# 计算样本偏度 
out = stats.skew(sample) 
print('\nSkewness = ' + str(out)) 
# 函数describe可以一次给出样本的多种描述统计结果 
out = stats.describe(sample) 
print('\nSize = ' + str(out[0])) 
print('Min = ' + str(out[1][0])) 
print('Max = ' + str(out[1][1])) 
print('Mean = ' + str(out[2])) 
print('Variance = ' + str(out[3])) 
print('Skewness = ' + str(out[4])) 
print('Kurtosis = ' + str(out[5]))
```



<br><br>**列联表函数**

|函数|说明|
|----|----|
| chi2_contingency(observed[, correction, lambda_]) | Chi-square test of independence of variables in a contingency table. <br> 列联表中变量独立性的卡方检验 |
| contingency.expected_freq(observed) | Compute the expected frequencies from a contingency table. <br> 从列联表中计算预期的频率 |
| contingency.margins(a) | Return a list of the marginal sums of the array a. <br> 返回数组a的边际和的列表 |
| fisher_exact(table[, alternative]) | Performs a Fisher exact test on a 2x2 contingency table. <br> 对2×2列联表执行Fisher精确检验 |


<br><br>**Plot 检验**

|函数|说明|
|----|----|
| ppcc_max(x[, brack, dist]) | Returns the shape parameter that maximizes the probability plot correlation coefficient for the given data to a one-parameter family of distributions. <br> 返回使给定数据的概率图相关系数最大化为单参数分布族的形状参数。 |
| ppcc_plot(x, a, b[, dist, plot, N]) | Returns (shape, ppcc), and optionally plots shape vs. <br>  返回（形状，ppcc），并可选地绘制形状 |
| probplot(x[, sparams, dist, fit, plot]) | Calculate quantiles for a probability plot, and optionally show the plot. <br> 计算概率图的分位数，并可选择显示图 |
| boxcox_normplot(x, la, lb[, plot, N]) | Compute parameters for a Box-Cox normality plot, optionally show it. <br> 计算Box-Cox正态图的参数，可选择显示 |


<br><br>**蒙面统计函数**

Statistical functions for masked arrays (scipy.stats.mstats)
* scipy.stats.mstats.argstoarray
* scipy.stats.mstats.betai
* scipy.stats.mstats.chisquare
* scipy.stats.mstats.count_tied_groups
* scipy.stats.mstats.describe
* scipy.stats.mstats.f_oneway
* scipy.stats.mstats.f_value_wilks_lambda
* scipy.stats.mstats.find_repeats
* scipy.stats.mstats.friedmanchisquare
* scipy.stats.mstats.kendalltau
* scipy.stats.mstats.kendalltau_seasonal
* scipy.stats.mstats.kruskalwallis
* scipy.stats.mstats.kruskalwallis
* scipy.stats.mstats.ks_twosamp
* scipy.stats.mstats.ks_twosamp
* scipy.stats.mstats.kurtosis
* scipy.stats.mstats.kurtosistest
* scipy.stats.mstats.linregress
* scipy.stats.mstats.mannwhitneyu
* scipy.stats.mstats.plotting_positions
* scipy.stats.mstats.mode
* scipy.stats.mstats.moment
* scipy.stats.mstats.mquantiles
* scipy.stats.mstats.msign
* scipy.stats.mstats.normaltest
* scipy.stats.mstats.obrientransform
* scipy.stats.mstats.pearsonr
* scipy.stats.mstats.plotting_positions
* scipy.stats.mstats.pointbiserialr
* scipy.stats.mstats.rankdata
* scipy.stats.mstats.scoreatpercentile
* scipy.stats.mstats.sem
* scipy.stats.mstats.signaltonoise
* scipy.stats.mstats.skew
* scipy.stats.mstats.skewtest
* scipy.stats.mstats.spearmanr
* scipy.stats.mstats.theilslopes
* scipy.stats.mstats.threshold
* scipy.stats.mstats.tmax
* scipy.stats.mstats.tmean
* scipy.stats.mstats.tmin
* scipy.stats.mstats.trim
* scipy.stats.mstats.trima
* scipy.stats.mstats.trimboth
* scipy.stats.mstats.trimmed_stde
* scipy.stats.mstats.trimr
* scipy.stats.mstats.trimtail
* scipy.stats.mstats.tsem
* scipy.stats.mstats.ttest_onesamp
* scipy.stats.mstats.ttest_ind
* scipy.stats.mstats.ttest_onesamp
* scipy.stats.mstats.ttest_rel
* scipy.stats.mstats.tvar
* scipy.stats.mstats.variation
* scipy.stats.mstats.winsorize
* scipy.stats.mstats.zmap
* scipy.stats.mstats.zscore

<br><br>**单变量和多变量核密度估计(scipy.stats.kde)**

|函数|说明|
|----|----|
|gaussian_kde(dataset[, bw_method])|Representation of a kernel-density estimate using Gaussian kernels. <br> 使用高斯内核表示核密度估计|

<br><br>
>对于更多的统计相关功能，安装软件R和接口软件包rpy。


<br><br>**<font color='red'>Python来做假设检验</font>**

[原文](https://segmentfault.com/a/1190000007626742)

对于任何一个频率派的数据科学家而言，日常做数据分析难免还是会用到一些假设检验方法做一个数据探索和相关性、差异性分析，并且这也是做后续统计模型（机器学习类预测模型可以略过）预测的第一步。
这篇博文目的就是整理基本的假设检验方法、适用条件和调用Python（主要是scipy模块）的哪些方法。

<br>**正态性检验**

这个是很多统计建模的第一步，例如，普通线性回归就对残差有正态性要求。

<br>***K-S检验***

特点是比较严格，基于的原理是CDF，理论上可以检验任何分布。
```
scipy.stats.kstest(a_vector_like_data, 'norm')
```

<br>***Shapiro检验***

专门用来检验正态分布。
```
scipy.stats.shapiro(a_vector_like_data)
```

<br>***Normal检验***

原理是基于数据的skewness和kurtosis，如不明白这两个意思，自行百度。
```
scipy.stats.normaltest(a_vector_like_data)
```

<br>***Anderson检验***

是ks检验的正态检验加强版。
```
scipy.stats.anderson(a_vector_like_data, dist='norm')
```

<br>**检验方差是否齐**

<br>***Bartlett检验***

对数据有正态性要求
```
scipy.stats.bartlett(a, b)
```

<br>***Levene检验***

在数据非正态的情况下，精度比Bartlett检验好，可调中间值的度量
```
scipy.stats.levene(a, b, center = 'trimmed')
```

<br>***Fligner-Killeen检验***

非参检验，不依赖于分布
```
scipy.stats.fligner(a, b, center='mean')
```

<br>**两组数之间的比较**

<br>***参数方法***

```
# 独立两样本t检验 
scipy.stats.ttest_ind(a, b, equal_var=True, nan_policy='omit') 
# 成对两样本t检验 
scipy.stats.ttest_rel(a, b, equal_var=True, nan_policy='omit') 
# 通过基本统计量来做独立两样本检验 
scipy.stats.ttest_ind_from_stats(20.06, 2.902, 50, 13.26, 1.977, 50, equal_var=False)
```

<br>***非参数方法***

```
# wilcox秩序和检验，n < 20时独立样本效果比较好 
scipy.stats.ranksums(a, b) 
# Mann-Whitney U检验, n > 20时独立样本，比wilcox秩序和检验更稳健 
scipy.stats.mannwhitneyu(a, b) 
# Wilcox检验，成对数据 
scipy.stats.wilcoxn(a, b, zero_method='wilcox', correction=False)
```

<br>**多组数之间的比较**

<br>***参数方法（1-way anova）***

```
scipy.stats.f_oneway(a, b, c, ...)
```

<br>***非参数方法（Kruskal-Wallis H方法）***

```
scipy.stats.kruskal(a, b, c,..., nan_policy='omit')
```

<br>**(附送)相关性**

相关性可以做简单的特征工程（特征筛选）来做监督学习以及作为相似度（1 - 距离）来做非监督学习。

<br>***参数（Pearson相关系数）***

```
scipy.stats.pearsonr(a, b)
```

<br>***非参数（Spearman相关系数）***

```
scipy.stats.spearmanr(a, b)
```

<br>***二元值和连续值之间的关系（Point-biserial相关系数）***

```
scipy.stats.pointbiserialr(a, b)
```

<br>***分参数的Kendall's Tau***

理论上是检验两个变量是否具有单调关系
```
scipy,stats.kendalltau(a, b, initial_lexsort=None, nan_policy='omit')
```

### scipy

* [易百 - Scipy教程](https://www.yiibai.com/scipy/scipy_optimize.html)

**基本函数**

利用积分来求面积

```
from scipy.integrate import quad
#    所需要的常用参数: func, a, b。
#        func:传入的函数，
#        a:积分下限,
#        b:积分上限。
area,error = quad(func, a, b)
```






### 2. pandas

**1. 基本操作**

***1.1. 小数位数 精度的处理round()***

```
# 控制台打印时显示的2位小数
>>> pd.set_option('precision', 2)

# 实际修改数据精度
>>> df = pd.DataFrame(np.random.random([3, 3]), columns=['A', 'B', 'C'], index=['first', 'second', 'third']) 
>>> df
               A         B         C 
first   0.028208  0.992815  0.173891 
second  0.038683  0.645646  0.577595 
third   0.877076  0.149370  0.491027 
>>> df.round(2)
           A     B     C 
first   0.03  0.99  0.17 
second  0.04  0.65  0.58 
third   0.88  0.15  0.49 
>>> df.round({'A': 1, 'C': 2})
          A         B     C 
first   0.0  0.992815  0.17 
second  0.0  0.645646  0.58 
third   0.9  0.149370  0.49 
>>> decimals = pd.Series([1, 0, 2], index=['A', 'B', 'C']) 
>>> df.round(decimals)
          A  B     C 
first   0.0  1  0.17 
second  0.0  1  0.58 
third   0.9  0  0.49
```

***1.2. [pandas.DataFrame对行和列求和及添加新行和列](https://www.cnblogs.com/wuzhiblog/p/python_new_row_or_col.html)***

**<计算各列数据总和并作为新列添加到末尾>**

```
df['Col_sum'] = df.apply(lambda x: x.sum(), axis=1)
```

**<计算各行数据总和并作为新行添加到末尾>**

```
df.loc['Row_sum'] = df.apply(lambda x: x.sum())
```

***1.3. [在Pandas中更改列的数据类型](https://blog.csdn.net/jinruoyanxu/article/details/79150896)***

如果想要将这个操作应用到多个列，依次处理每一列是非常繁琐的，所以可以使用`DataFrame.apply`处理每一列。

```
>>> a = [['a', '1.2', '4.2'], ['b', '70', '0.03'], ['x', '5', '0']]
>>> df = pd.DataFrame(a, columns=['col1','col2','col3'])
>>> df
  col1 col2  col3
0    a  1.2   4.2
1    b   70  0.03
2    x    5     0
```

然后可以写：

```
df[['col2','col3']] = df[['col2','col3']].apply(pd.to_numeric)
```

那么'col2'和'col3'根据需要具有float64类型。

但是，可能不知道哪些列可以可靠地转换为数字类型。在这种情况下，设置参数：

```
df.apply(pd.to_numeric, errors='ignore')
```

然后该函数将被应用于整个DataFrame，可以转换为数字类型的列将被转换，而不能(例如，它们包含非数字字符串或日期)的列将被单独保留。

另外pd.to_datetime和pd.to_timedelta可将数据转换为日期和时间戳。


***1.4. 分位函数***

> DataFrame.quantile(q=0.5, axis=0, numeric_only=True, interpolation='linear')


***1.5. 对时间进行分组***

[Python Pandas Group by date using datetime data](https://stackoverflow.com/questions/39400115/python-pandas-group-by-date-using-datetime-data)

```
# 先按照测序方法(Array, NGS)将数据分为两类，在根据扩增时间将数据细分到每月，最后统计胚胎的数目
dx = dx.groupby("test_method").resample("M", on="amplify_date").count()["embryo_id"]
```


***1.6. 多个dataframe 与 N维数组的转换***

```
import numpy as np
import pandas as pd

## 将10个(5,20)的dataframe合并成一个(5,100)的dataframe

dfs = []  # 10个dataframe (shape: 5 x 20)
for i in range(10):
	df = pd.DataFrame(np.random.randint(0,100,(5,20)))
	dfs.append(df)
# 将10个(5,20)的dataframe转成(10,5,20)的数组
arrs = np.array([df.values for df in dfs])
# 将(10,5,20)的数组转成(10,100)的数组
arrs1 = arrs.reshape(10, -1)
# 再将(10,100)的数组转成dataframe
df1 = pd.DataFrame(arrs1)

```



***1.7. 其它***

* 将NaN和inf替换为0 ： `df[df.isin([np.nan, np.inf])] = 0`




**<font color="green",size=5>自我总结</font>**

**继承pd.DataFrame,构建自己的数据框类**

[python中如何实现“反向继承”？](https://www.zhihu.com/question/59704897/answer/168038061)
[Easier subclassing #60](https://github.com/pandas-dev/pandas/issues/60)
```
import pandas as pd

class MyDataFrame(pd.DataFrame):

    # 必须加这个属性, 不然使用self.copy()返回的是`pandas.core.frame.DataFrame`, 而不是`MyDataFram`
    @property
    def _constructor(self):
        # return MyDataFrame
        return self.__class__

    @classmethod
    def read_csv(cls, *args, **kwargs):
        df = pd.read_csv(*args, **kwargs)
        return cls.copy_dateframe(df)

    @classmethod
    def copy_dateframe(cls, df):
        return cls(df.values, index=df.index, columns=df.columns)

    def __init__(self, *args, **kwargs):
        # super(MyDataFrame, self).__init__(*args, **kwargs)
        super(self.__class__, self).__init__(*args, **kwargs)
        self = self.add_month()

    def add_month(self):
        df = self.copy()
        df['month'] = 1 
        return df

    def get_month(self):
        return df[df['month']==month]

df = MyDataFrame.read_csv("test.csv").get_month(month)

```

也可以向下面这样：

```
import pandas as pd

class MyDataFrame(pd.DataFrame):

    def __init__(self, data):
        self._data = pd.DataFrame(data)

    @classmethod
    def from_frame(self, frame):
        """frame可以是dict, pd.DataFrame, pd.Series等"""
        return cls(frame)

    @classmethod
    def read_xls(file):
        data = pd.read_table(file, index_col=0)
        return cls(data)

    def __str__(self):
        return self._data.to_string()

    def __repr__(self):
        return self._data.to_string()

    @property
    def shape(self):
        return self.abund.shape

    @property
    def T(self):
        data = self._data.T
        return self.__class__(data)

    def head(self, n=5):
        return self._data.head(n)

    def select_columns(self, columns):
        data = self._data(columns)
        return self.__class__(data)

```



### 3. numpy

* [Numpy练习题100题-提高你的数据分析技能](https://github.com/rougier/numpy-100)


1. **基本操作**

**获得矩阵的上三角数据 : np.triu_indices()**

```
>>> iu1 = np.triu_indices(4)
>>> iu2 = np.triu_indices(4, 2)
# Here is how they can be used with a sample array:
>>> a = np.arange(16).reshape(4, 4)
>>> a
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11],
       [12, 13, 14, 15]])
# Both for indexing:
>>> a[iu1]
array([ 0,  1,  2,  3,  5,  6,  7, 10, 11, 15])
# And for assigning values:
>>> a[iu1] = -1
>>> a
array([[-1, -1, -1, -1],
       [ 4, -1, -1, -1],
       [ 8,  9, -1, -1],
       [12, 13, 14, -1]])
# These cover only a small part of the whole array (two diagonals right of the main one):
>>> a[iu2] = -10
>>> a
array([[ -1,  -1, -10, -10],
       [  4,  -1,  -1, -10],
       [  8,   9,  -1,  -1],
       [ 12,  13,  14,  -1]])
```

**将多维数组转化为一维数组flatten()**

```
>>> a = np.array([[1,2], [3,4]])
>>> a.flatten()
array([1, 2, 3, 4])
>>> a.flatten('F')
array([1, 3, 2, 4])

#使用np.r_()
>>> np.r_[np.array([1,2,3]), 0, 0, np.array([4,5,6])]
>>> array([1, 2, 3, 0, 0, 4, 5, 6])
>>> np.r_[-1:1:6j, [0]*3, 5, 6]
array([-1. , -0.6, -0.2,  0.2,  0.6,  1. ,  0. ,  0. ,  0. ,  5. ,  6. ])
```

**分位函数**

```
#求数组a的四分位数
np.percentile(a, [25, 50, 75])
```

**获得数组值从小到大的索引值**

```
>>> x = np.array([3, 1, 2])
>>> np.argsort(x) #按升序排列
array([1, 2, 0])
>>> np.argsort(-x) #按降序排列
array([0, 2, 1])
>>> x[np.argsort(x)] #通过索引值排序后的数组
array([1, 2, 3])
>>> x[np.argsort(-x)]
array([3, 2, 1])
```

**求以n为底的对数值**

* [numpy.log(math.log)](https://blog.csdn.net/Mr_Cat123/article/details/78806827)

```
np.log()   # 以e为底
np.log2()  # 以2为底
np.log10()

# 除了以e,2,10为底以外，没有以其它值为底的函数，需要用到换底公式：
#   logaB = logcB / logcA
# 如以3为底4的对数
np.log(4) / np.log(3)

# math.log可以以任意数为底
math.log(4,3)
```

**获得index**

* `np.nonzero`: 返回非0元素的index
* `np.where`: 获得符合条件的元素的index


**提取对角线或构造对角线数组**

* `np.diag`: 提取对角线或构造对角线数组
* `np.diag_indices`: 返回索引以访问数组的主对角线
* `np.diag_indices_from`: 返回索引以访问n维数组的主对角线
* `np.diagflat`: 创建一个二维数组，将扁平的输入作为对角线
* `np.diagonal`: 返回指定的对角线
* `np.fill_diagonal`: 填充给定数组的任意维数的主对角线


**连接数组**

* `np.append`: 添加值(或数组)到数组
* `np.concatenate`: 连接数组
* `np.vstack`: 垂直连接数组
* `np.hstack`: 水平连接数组
* `np.c_[]`: 将向量按列合并


**调整轴顺序**

* `np.transpose`: 重新指定轴顺序
* `np.swapaxes`: 交换两个轴


**空或非空操作**

* `np.nan`: 空值，float类型
* `np.nan_to_num`: 用0替代nan；用最大的有限数替代无穷值(∞)
* `np.nanargmin`: 忽略nan，返回最小值的坐标
* `np.nanargmax`: 
* `np.nancumprod`: 累乘，nan置为1
* `np.nancumsum`: 累加，nan置为0
* `np.nanmax`: 
* `np.nanmean`: 忽略nan，再求平均
* `np.nanmedian`: 
* `np.nanmin`: 
* `np.nanpercentile`: 忽略nan，求分位数
* `np.nanprod`: 乘，nan置为1
* `np.nanquantile`: 忽略nan，求分位数
* `np.nanstd`: 
* `np.nansum`: 
* `np.nanvar`: 忽略nan，计算方差


**数组属性**
* `ndarray.ndim`: 秩，即轴的数量或维度的数量
* `ndarray.shape`: 数组的维度，对于矩阵，n 行 m 列
* `ndarray.size`: 数组元素的总个数，相当于 .shape 中 n*m 的值
* `ndarray.dtype`: ndarray 对象的元素类型
* `ndarray.itemsize`: ndarray 对象中每个元素的大小，以字节为单位
* `ndarray.flags`: ndarray 对象的内存信息
* `ndarray.real`: ndarray元素的实部
* `ndarray.imag`: ndarray 元素的虚部
* `ndarray.data`: 包含实际数组元素的缓冲区，由于一般通过数组的索引获取元素，所以通常不需要使用这个属性。

ndarray.flags 返回 ndarray 对象的内存信息，包含以下属性：

|属性|描述|
|----|----|
|C_CONTIGUOUS (C)|数据是在一个单一的C风格的连续段中|
|F_CONTIGUOUS (F)|数据是在一个单一的Fortran风格的连续段中|
|OWNDATA (O)|数组拥有它所使用的内存或从另一个对象中借用它|
|WRITEABLE (W)|数据区域可以被写入，将该值设置为 False，则数据为只读|
|ALIGNED (A)|数据和所有元素都适当地对齐到硬件上|
|UPDATEIFCOPY (U)|这个数组是其它数组的一个副本，当这个数组被释放时，原数组的内容将被更新|


**创建数组**

* `np.empty`:
* `np.zeros`:
* `np.ones`:
* `np.full`: 创建一个数组，并填充某个值。如创建一个全是NaN的数组
* `np.asarray`:
* `np.frombuffer`: 用于实现动态数组. 接受 buffer 输入参数，以流的形式读入转化成 ndarray 对象。
buffer 是字符串的时候，Python3 默认 str 是 Unicode 类型，所以要转成 bytestring 在原 str 前加上 b。
* `np.fromiter`: 从可迭代对象中建立 ndarray 对象，返回一维数组。
* `np.arange`:
* `np.linspace`: 函数用于创建一个一维数组，数组是一个等差数列构成的
* `np.logspace`: 函数用于创建一个于等比数列


**算数函数**

* `np.add`: 加
* `np.subtract`: 减
* `np.multiply`: 乘
* `np.divide`: 除
* `np.reciprocal`: 求倒数
* `np.power`: 求指数
* `np.mod`: 求模; 同`np.remainder`

**位运算**

NumPy "bitwise_" 开头的函数是位运算函数。

* `np.bitwise_and`: 对数组元素执行位与操作
* `np.bitwise_or`: 对数组元素执行位或操作
* `np.invert`: 按位取反
* `np.left_shift`: 向左移动二进制表示的位
* `np.right_shift`: 向右移动二进制表示的位

也可以使用 "&"、 "~"、 "|" 和 "^" 等操作符进行计算。


**字符串函数**

以下函数用于对 dtype 为 numpy.string_ 或 numpy.unicode_ 的数组执行向量化字符串操作。
 它们基于 Python 内置库中的标准字符串函数。

这些函数在字符数组类（numpy.char）中定义。

* `np.char.add`:
* `np.char.center`:
* `np.char.split`:

...


**排序、条件刷选函数**

NumPy 提供了多种排序的方法。 这些排序函数实现不同的排序算法，
每个排序算法的特征在于执行速度，最坏情况性能，所需的工作空间和算法的稳定性。 
下表显示了三种排序算法的比较。

|算法|速度|最坏情况|工作空间|稳定性|
|----|----|----|----|----|
|quicksort 快速排序|1|O(n^2)|0|否|
|mergesort 归并排序|2|O(n*log(n))|~n/2|是|
|heapsort 堆排序|3|O(n*log(n))|0|否|

* `np.argsort`: 返回数组值从小到大的索引值
* `np.lexsort`: 用于对多个序列进行排序。把它想象成对电子表格进行排序，每一列代表一个序列，
排序时优先照顾靠后的列。这里举一个应用场景：小升初考试，重点班录取学生按照总成绩录取。
在总成绩相同时，数学成绩高的优先录取，在总成绩和数学成绩都相同时，按照英语成绩录取…… 这里，
总成绩排在电子表格的最后一列，数学成绩在倒数第二列，英语成绩在倒数第三列。
* `np.msort`: 数组按第一个轴排序，返回排序后的数组副本。np.msort(a) 相等于 np.sort(a, axis=0)。
* `np.sort_complex`: 对复数按照先实部后虚部的顺序进行排序。
* `np.partition`: 指定一个数，对数组进行分区
* `np.argpartition`: 指定一个数，对数组进行分区

* `numpy.extract`: 根据某个条件从数组中抽取元素，返回满条件的元素。

```
x = np.arange(9.).reshape(3,  3)  
# 定义条件, 选择偶数元素
condition = np.mod(x,2)  ==  0  
# 使用条件提取元素
np.extract(condition, x)
```


**矩阵库**

NumPy 中包含了一个矩阵库 numpy.matlib，该模块中的函数返回的是一个矩阵，而不是 ndarray 对象。

* `np.matlib.empty`: 返回一个新的矩阵(填充为随机数据)
* `np.matlib.zeros`: 创建一个以 0 填充的矩阵
* `np.matlib.ones`: 创建一个以 1 填充的矩阵。
* `np.matlib.eye`: 返回一个矩阵，对角线元素为 1，其他位置为零。
* `np.matlib.identity`: 返回给定大小的单位矩阵
* `np.matlib.rand`: 创建一个给定大小的矩阵，数据是随机填充的。


**线性代数**

NumPy 提供了线性代数函数库 linalg，该库包含了线性代数所需的所有功能，可以看看下面的说明：

* `np.dot`: 两个数组的点积，即元素对应相乘。
* `np.vdot`: 两个向量的点积。如果第一个参数是复数，那么它的共轭复数会用于计算。 如果参数是多维数组，它会被展开。
* `np.inner`: 两个数组的内积。对于更高的维度，它返回最后一个轴上的和的乘积。
* `np.matmul`: 两个数组的矩阵积
* `np.determinant`: 数组的行列式
* `np.solve`: 求解线性矩阵方程
* `np.inv`: 计算矩阵的乘法逆矩阵
* `np.linalg.det`: 计算输入矩阵的行列式
* `np.linalg.solve`: 给出了矩阵形式的线性方程的解
* `np.linalg.inv`: 计算矩阵的乘法逆矩阵


**IO操作**

NumPy 为 ndarray 对象引入了一个简单的文件格式：npy。npy 文件用于存储重建 ndarray 所需的数据、图形、dtype 和其他信息。

常用的 IO 函数有：

* load() 和 save() 函数是读写文件数组数据的两个主要函数，默认情况下，数组是以未压缩的原始二进制格
式保存在扩展名为 .npy 的文件中。
* savez() 函数用于将多个数组写入文件，默认情况下，数组是以未压缩的原始二进制格式保存在扩展名为 
.npz 的文件中。 savez_compressed() 压缩的原始二进制保存
* loadtxt() 和 savetxt() 函数处理正常的文本文件(.txt 等)

```
np.savetxt(outfile, x, delimiter="\t", header=title, comments="# ", fmt="%s")

# delimiter: 分隔符
# header: 放在文件开头的字符串
# footer: 放在文件结尾的字符串
# comments: 将文件开头和结尾的字符串转成注释信息, 默认为"# "
# encoding: 编码格式
# newline: 每行的界定符， 默认为"\n"
# fmt: 书写格式, 如"%.18e", "%10.5f", " %.4e %+.4ej %.4e %+.4ej %.4e %+.4ej", "['%.3e + %.3ej', '(%.15e%+.15ej)']"
```


**其它**

`np.allclose()`: numpy的allclose方法，比较两个array是不是每一元素都相等，默认在1e-05的误差范围内
`np.ptp()`: 计算数组中元素最大值与最小值的差（最大值 - 最小值）
`np.amin()`和`np.amax()`: 计算数组中的元素沿指定轴的最小(大)值
`np.ndarray.byteswap`: 将 ndarray 中每个元素中的字节进行大小端转换
`np.packbits`, `np.unpackbits`: 将二进制值数组的元素打包成uint8数组中的位
`np.nbytes`: 查看数组占用的总内存空间  (也可以用sys.getsizeof函数)
`np.itemsize`: 查看数组中单个元素占用的内存空间


**参考**

将bool数组压缩成位。[numpy boolean array with 1 bit entries](https://stackoverflow.com/questions/5602155/numpy-boolean-array-with-1-bit-entries)




### 4. click

[官网](http://click.pocoo.org/6/)

[命令行神器 Click 简明笔记](http://python.jobbole.com/87111/)

[Python Click 学习笔记](https://isudox.com/2016/09/03/learning-python-package-click/)

[pyspider源代码-run.py click模块](https://www.jianshu.com/p/fb75bcacaaa0)

[Python click.pass_context() Examples](https://www.programcreek.com/python/example/86569/click.pass_context)

[使用 Flask 开发 Web 应用（二）](https://segmentfault.com/a/1190000008426273)

[怎样定制help或epilog格式--format_epilog()](https://stackoverflow.com/questions/42446923/python-click-help-formatting-newline#)


* `click.group` : 命令可以通过group添加其他的命令.可以在脚本中随意嵌套
* `click.option` : 使用option()和argument()添加参数
* `click.version_option`: 添加一个--version选项,让程序在打印出version之后立即退出,Click 提供 eager 标识对参数名进行标识，如果输入该参数，则会拦截既定的命令行执行流程，跳转去执行一个回调函数
* `click.pass_context` : 返回当前上下文作为第一个参数传递给对应的方法. 每次一个命令被调用,一个新的上下文被处创建和指向父类上下文.通常,你看不到这些上下文.但是,上下文自动传递给参数和方法.命令可以通过 pass_context()来请求和传递上下文.在这种情况下上下文作文第一个参数.
*  `click.Choice` : 让一个参数有一个选择列表.

**自我总结1**

```
import click

group_arguments = {
    "context_settings": {
        "help_option_names": ['-h', '--help']  # make `-h` as same as `--help`
    },
    "invoke_without_command": True,  # make the group can be invoked without sub-command
                     # 使这组命令可以不调用子命令，即可以调用下文中的cli
}

@click.group(**group_arguments) 
@click.option("--debug", envvar='DEBUG', default=False, is_flag=True, help='debug mode')
@click.version_option(version="0.1", prog_name="test")  # 增加版本信息
@click.pass_context  # 返回当前上下文(ctx)作为第一个参数传递给对应的方法
def cli(ctx, **kwargs):
    if ctx.invoked_subcommand is None:   # 如果不调用子命令，就自动调用initdb子命令
        ctx.invoke(initdb)

@cli.command()
@click.option("--db-host", help="database host", default="127.0.0.1")  # 自动加"-"改为"_"
@click.option("--db-port", help="database port", default="8080")
@click.pass_context
def initdb(ctx, db_host, db_port):
    click.echo("Initialized the database")
    click.echo("host: {} prot: {}".format(db_host, db_port))

@cli.command()
@click.option("--name", help="user name", default="root")
@click.option("-pw", "--password", help="password") # 使用"password"作为参数
@click.pass_context
def dropdb(ctx, name, password):
    click.echo("Dropped the database")
    click.echo("uesr: {} passward: {}".format(name, password))

cli()


```

**自我总结2**

1. 如果想用`-h`代替`--help`，可以使用`@cli.command(context_settings=dict(help_option_names=['-h', '--help']))`
2. 



### 5. sqlite3

[使用SQLite](https://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001388320596292f925f46d56ef4c80a1c9d8e47e2d5711000)

[用Python进行SQLite数据库操作](https://www.cnblogs.com/yuxc/archive/2011/08/18/2143606.html)

SQLite是一种嵌入式数据库，它的数据库就是一个文件。由于SQLite本身是C写的，而且体积很小，所以，经常被集成到各种应用程序中，甚至在iOS和Android的App中都可以集成。
Python就内置了SQLite3，所以，在Python中使用SQLite，不需要安装任何东西，直接使用。
在使用SQLite前，我们先要搞清楚几个概念：
表是数据库中存放关系数据的集合，一个数据库里面通常都包含多个表，比如学生的表，班级的表，学校的表，等等。表和表之间通过外键关联。
要操作关系数据库，首先需要连接到数据库，一个数据库连接称为Connection；
连接到数据库后，需要打开游标，称之为Cursor，通过Cursor执行SQL语句，然后，获得执行结果。
Python定义了一套操作数据库的API接口，任何数据库要连接到Python，只需要提供符合Python标准的数据库驱动即可。
由于SQLite的驱动内置在Python标准库中，所以我们可以直接来操作SQLite数据库。
我们在Python交互式命令行实践一下：

```
# 导入SQLite驱动: 
>>> import sqlite3 
# 连接到SQLite数据库 
# 数据库文件是test.db 
# 如果文件不存在，会自动在当前目录创建: 
>>> conn = sqlite3.connect('test.db') 
# 创建一个Cursor: 
>>> cursor = conn.cursor() 
# 执行一条SQL语句，创建user表: 
>>> cursor.execute('create table user (id varchar(20) primary key, name varchar(20))') 
<sqlite3.Cursor object at 0x10f8aa260> 
# 继续执行一条SQL语句，插入一条记录: 
>>> cursor.execute('insert into user (id, name) values (\'1\', \'Michael\')') 
<sqlite3.Cursor object at 0x10f8aa260> 
# 通过rowcount获得插入的行数: 
>>> cursor.rowcount 
1 
# 关闭Cursor: 
>>> cursor.close() 
# 提交事务: 
>>> conn.commit() 
# 关闭Connection: 
>>> conn.close()
```

我们再试试查询记录：

```
>>> conn = sqlite3.connect('test.db') 
>>> cursor = conn.cursor() 
# 执行查询语句: 
>>> cursor.execute('select * from user where id=?', ('1',)) 
<sqlite3.Cursor object at 0x10f8aa340> 
# 获得查询结果集: 
>>> values = cursor.fetchall() 
>>> values

[(u'1', u'Michael')] 
>>> cursor.close() 
>>> conn.close()
```

使用Python的DB-API时，只要搞清楚Connection和Cursor对象，打开后一定记得关闭，就可以放心地使用。
使用Cursor对象执行`insert`，`update`，`delete`语句时，执行结果由`rowcount`返回影响的行数，就可以拿到执行结果。
使用Cursor对象执行`select`语句时，通过`featchall()`可以拿到结果集。结果集是一个list，每个元素都是一个tuple，对应一行记录。
如果SQL语句带有参数，那么需要把参数按照位置传递给`execute()`方法，有几个?占位符就必须对应几个参数，例如：
```
cursor.execute('select * from user where name=? and pwd=?', ('abc', '123456'))
```
SQLite支持常见的标准SQL语句以及几种常见的数据类型。具体文档请参阅SQLite官方网站。
小结
在Python中操作数据库时，要先导入数据库对应的驱动，然后，通过Connection对象和Cursor对象操作数据。
要确保打开的Connection对象和Cursor对象都正确地被关闭，否则，资源就会泄露。
如何才能确保出错的情况下也关闭掉Connection对象和Cursor对象呢？请回忆`try:...except:...finally:...`的用法。

</br>

**自我总结**

查询数据库中的所有表
```
>>>cursor.execute("SELECT name FROM sqlite_master WHERE type='table' ORDER BY name;")
>>>cursor.fetchall()
[(u'projectdb',)]
```
查询某表中的所有字段名（字段信息）
```
>>>cursor.execute("PRAGMA table_info(projectdb)")
>>>cursor.fetchall()
[(0, u'name', u'', 0, None, 1),
 (1, u'group', u'', 0, None, 0),
 (2, u'status', u'', 0, None, 0),
 (3, u'script', u'', 0, None, 0),
 (4, u'comments', u'', 0, None, 0),
 (5, u'rate', u'', 0, None, 0),
 (6, u'burst', u'', 0, None, 0),
 (7, u'updatetime', u'', 0, None, 0)]
```
查询某表中的所有字段
```
>>>cursor.execute("SELECT * name FROM from projectdb")
[(u'taonvlang',
  None,
  u'STOP',
  u'#!/usr/bin/env',
  None,
  1,
  3,
  1517965200.333391)]
```

### 6. JSON 和 pickle

[python 序列化之JSON和pickle详解](https://www.cnblogs.com/tkqasn/p/6005025.html)

[Python中 pickle有什么意义，pickle了再恢复？](https://www.zhihu.com/question/38355589)

很多入门教程里讲解序列化一般是这个流程：
>对象1  -- 序列化 ->  字节串  -- 反序列化 ->  对象2

所以很多人并不知道为什么要序列化。
估计很多人都有耳闻 Python 在处理计算密集型的任务时性能不好，一般不能充分使用多核 CPU 的优势，这时候会使用多进程来优化。
有一种多进程的计算方式是这样的，进程分为 master 和 worker，master 负责调度任务，worker 则专于计算，比如 Celery 这个库。
那么问题来了，master 中产生了一个任务需要交给 worker 来计算，因为进程之间内存是隔离的，worker 不能直接访问到这个任务对象。
所以 master 需要以某种方式将这个对象表示出来传递给 worker，而且 worker 能够根据这个表示方式来构造出这个对象（的替身），这个过程就是序列化和反序列化。而 pickle 是 Python 内部的一种序列化方式，对 Python 对象有很好的支持，而这个原因也正是 Celery 默认使用 pickle 的原因，Is Celery dependent on pickle? 。从序列化的角度来看，pickle 的方案和 JSON，YAML，XML 等没有本质的区别。不过 pickle 的安全性不足，永远不要反序列化不可信来源的 pickle 字节串，因此 pickle 方案不适合用于网络通信。

**JSON模块**

JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。它基于ECMAScript的一个子集。 JSON采用完全独立于语言的文本格式，但是也使用了类似于C语言家族的习惯(包括C、C++、Java、JavaScript、Perl、Python等)。这些特性使JSON成为理想的数据交换语言。易于人阅读和编写，同时也易于机器解析和生成(一般用于提升网络传输速率)。
JSON在python中分别由list和dict组成。

***一、python类型数据和JSON数据格式互相转换***

![python类型数据和JSON数据格式互相转换](https://images2015.cnblogs.com/blog/996085/201610/996085-20161027174512437-1325085036.png)
pthon 中str类型到JSON中转为unicode类型，None转为null,dict对应object

***二、数据encoding和decoding***

*1、简单类型数据编解码*

所谓简单类型就是指上表中出现的python类型。
`dumps`:　　将对象序列化
```
#coding:utf-8
import json

# 简单编码===========================================
print json.dumps(['foo', {'bar': ('baz', None, 1.0, 2)}])
# ["foo", {"bar": ["baz", null, 1.0, 2]}]

#字典排序
print json.dumps({"c": 0, "b": 0, "a": 0}, sort_keys=True)
# {"a": 0, "b": 0, "c": 0}

#自定义分隔符
print json.dumps([1,2,3,{'4': 5, '6': 7}], sort_keys=True, separators=(',',':'))
# [1,2,3,{"4":5,"6":7}]
print json.dumps([1,2,3,{'4': 5, '6': 7}], sort_keys=True, separators=('/','-'))
# [1/2/3/{"4"-5/"6"-7}]

#增加缩进，增强可读性，但缩进空格会使数据变大
print json.dumps({'4': 5, '6': 7}, sort_keys=True,indent=2, separators=(',', ': '))
# {
#   "4": 5,
#   "6": 7
# }

# 另一个比较有用的dumps参数是skipkeys，默认为False。
# dumps方法存储dict对象时，key必须是str类型，如果出现了其他类型的话，那么会产生TypeError异常，如果开启该参数，设为True的话，会忽略这个key。
data = {'a':1,(1,2):123}
print json.dumps(data,skipkeys=True)
#{"a": 1}

# 输出中文，设置ensure_ascii=False
json.dumps(data, ensure_ascii=False)

```

`dump`:　　将对象序列化并保存到文件

```
#将对象序列化并保存到文件 
obj = ['foo', {'bar': ('baz', None, 1.0, 2)}] 
with open(r"c:\json.txt","w+") as f:
    json.dump(obj,f)
```

`loads`:　　将序列化字符串反序列化

```
import json

obj = ['foo', {'bar': ('baz', None, 1.0, 2)}]
a= json.dumps(obj)
print json.loads(a)
# [u'foo', {u'bar': [u'baz', None, 1.0, 2]}]
```

`load`:　　将序列化字符串从文件读取并反序列化

```
with open(r"c:\json.txt","r") as f:
    print json.load(f)
```

***三、自定义复杂数据类型编解码***

例如我们碰到对象datetime，或者自定义的类对象等json默认不支持的数据类型时，我们就需要自定义编解码函数。有两种方法来实现自定义编解码。

*1、方法一：自定义编解码函数*

```
#! /usr/bin/env python
# -*- coding:utf-8 -*-
# __author__ = "TKQ"
import datetime,json

dt = datetime.datetime.now()



def time2str(obj):
    #python to json
    if isinstance(obj, datetime.datetime):
        json_str = {"datetime":obj.strftime("%Y-%m-%d %X")}
        return json_str
    return obj

def str2time(json_obj):
    #json to python
    if "datetime" in json_obj:
        date_str,time_str = json_obj["datetime"].split(' ')
        date = [int(x) for x in date_str.split('-')]
        time = [int(x) for x in time_str.split(':')]
        dt = datetime.datetime(date[0],date[1], date[2], time[0],time[1], time[2])
        return dt
    return json_obj


a = json.dumps(dt,default=time2str)
print a
# {"datetime": "2016-10-27 17:38:31"}
print json.loads(a,object_hook=str2time)
# 2016-10-27 17:38:31
```

*2、方法二：继承JSONEncoder和JSONDecoder类，重写相关方法*

```
#! /usr/bin/env python
# -*- coding:utf-8 -*-
# __author__ = "TKQ"
import datetime,json

dt = datetime.datetime.now()
dd = [dt,[1,2,3]]

class MyEncoder(json.JSONEncoder):
    def default(self,obj):
        #python to json
        if isinstance(obj, datetime.datetime):
            json_str = {"datetime":obj.strftime("%Y-%m-%d %X")}
            return json_str
        return obj

class MyDecoder(json.JSONDecoder):
    def __init__(self):
        json.JSONDecoder.__init__(self, object_hook=self.str2time)

    def str2time(self,json_obj):
        #json to python
        if "datetime" in json_obj:
            date_str,time_str = json_obj["datetime"].split(' ')
            date = [int(x) for x in date_str.split('-')]
            time = [int(x) for x in time_str.split(':')]
            dt = datetime.datetime(date[0],date[1], date[2], time[0],time[1], time[2])
            return dt
        return json_obj


# a = json.dumps(dt,default=time2str)
a =MyEncoder().encode(dd)
print a
# [{"datetime": "2016-10-27 18:14:54"}, [1, 2, 3]]
print MyDecoder().decode(a)
# [datetime.datetime(2016, 10, 27, 18, 14, 54), [1, 2, 3]]
```

**pickle模块**

python的pickle模块实现了python的所有数据序列和反序列化。基本上功能使用和JSON模块没有太大区别，方法也同样是dumps/dump和loads/load。cPickle是pickle模块的C语言编译版本相对速度更快。
与JSON不同的是pickle不是用于多种语言间的数据传输，它仅作为python对象的持久化或者python程序间进行互相传输对象的方法，因此它支持了python所有的数据类型。
pickle反序列化后的对象与原对象是等值的副本对象，类似与deepcopy。
`dumps/dump序列化`
```
from datetime import date

try:
    import cPickle as pickle    #python 2
except ImportError as e:
    import pickle   #python 3


src_dic = {"date":date.today(),"oth":([1,"a"],None,True,False),}
det_str = pickle.dumps(src_dic)
print det_str
# (dp1
# S'date'
# p2
# cdatetime
# date
# p3
# (S'\x07\xe0\n\x1b'
# tRp4
# sS'oth'
# p5
# ((lp6
# I1
# aS'a'
# aNI01
# I00
# tp7
# s.
with open(r"c:\pickle.txt","w") as f:
    pickle.dump(src_dic,f)
```

`loads/load反序列化`

```
from datetime import date

try:
    import cPickle as pickle    #python 2
except ImportError as e:
    import pickle   #python 3


src_dic = {"date":date.today(),"oth":([1,"a"],None,True,False),}
det_str = pickle.dumps(src_dic)
with open(r"c:\pickle.txt","r") as f:
    print pickle.load(f)
# {'date': datetime.date(2016, 10, 27), 'oth': ([1, 'a'], None, True, False)}
```

**JSON和pickle模块的区别**

1、JSON只能处理基本数据类型。pickle能处理所有Python的数据类型。
2、JSON用于各种语言之间的字符转换。pickle用于Python程序对象的持久化或者Python程序间对象网络传输，但不同版本的Python序列化可能还有差异。
  
### 7. six

python2和3的兼容库

[Six: Python 2 and 3 Compatibility Library](http://pythonhosted.org/six/)

</br>


### 8. pathlib

pathlib是python3中的新模块，比os.path使用更方便。

[python3中pathlib库的Path类的使用-AManFromEarth的博客](https://blog.csdn.net/amanfromearth/article/details/80265843)

[让我们重新认识python3的pathlib-豆瓣](https://www.douban.com/group/topic/106994006/)

**基本用法:**

* `Path.iterdir()`　　#遍历目录的子目录或者文件
* `Path.is_dir()`　　#判断是否是目录
* `Path.glob()`　　#过滤目录(返回生成器)
* `Path.resolve()`　　#返回绝对路径
* `Path.exists()`　　#判断路径是否存在
* `Path.open()`　　#打开文件(支持with)
* `Path.unlink()`　　#删除文件或目录(目录非空触发异常)

**基本属性:**

* `Path.parts`　　#分割路径 类似os.path.split(), 不过返回元组
* `Path.drive`　　#返回驱动器名称
* `Path.root`　　#返回路径的根目录
* `Path.anchor`　　#自动判断返回drive或root
* `Path.parents`　　#返回所有上级目录的列表
* `Path.suffix`   #文件后缀
* `Path.stem`     #文件名不带后缀
* `Path.name`     #带后缀的完整文件名
* `Path.parent`   #路径的上级目录

**改变路径:**

* `Path.with_name()`　　#更改路径名称, 更改最后一级路径名
* `Path.with_suffix()`　　#更改路径后缀
* `Path.joinpath()`　　#拼接路径
* `Path.relative_to()`　　#计算相对路径

**测试路径:**

* `Path.match()`　　#测试路径是否符合pattern
* `Path.is_dir()`　　#是否是文件
* `Path.is_absolute()`　　#是否是绝对路径
* `Path.is_reserved()`　　#是否是预留路径
* `Path.exists()`　　#判断路径是否真实存在

**其他方法:**

* `Path.cwd()`　　#返回当前目录的路径对象
* `Path.home()`　　#返回当前用户的home路径对象
* `Path.stat()`　　#返回路径信息, 同os.stat()
* `Path.chmod()`　　#更改路径权限, 类似os.chmod()
* `Path.expanduser()`　　#展开~返回完整路径对象
* `Path.mkdir()`　　#创建目录
* `Path.rename()`　　#重命名路径
* `Path.rglob()`　　#递归遍历所有子目录的文件



### 9. schedule

* [官网](https://schedule.readthedocs.io/en/stable/)
* [使用Python完美管理和调度你的多个任务](https://blog.csdn.net/oh5W6HinUg43JvRhhB/article/details/78589009)
* [python中schedule模块的使用](https://blog.csdn.net/kamendula/article/details/51452352)
* [python中的轻量级定时任务调度库：schedule](http://www.cnblogs.com/anpengapple/p/8051923.html)

例子：

```
import schedule
import time

def job():
    print("I'm working...")

schedule.every(10).minutes.do(job)
schedule.every().hour.do(job)
schedule.every().day.at("10:30").do(job)
schedule.every().monday.do(job)
schedule.every().wednesday.at("13:15").do(job)

while True:
    schedule.run_pending()
    time.sleep(1)
```

### 10. PyPDF2 和 Reportlab

* [pyhton之Reportlab模块](http://www.cnblogs.com/hujq1029/p/7767980.html)

**对PDF页面进行截取**

下边代码是对pdf文件中的所有图片进行截取

```
from PyPDF2 import PdfFileReader, PdfFileWriter

pr = PdfFileReader(open("15PK1175-127_L1_I517.cnv.pdf", "rb"))

pw = PdfFileWriter()

for i in range(24):
    po = pr.getPage(i)
    #po.trimBox.lowerLeft = (0, 216)
    #po.trimBox.upperRight = (864, 432)
    #po.cropBox.lowerLeft = (0, 216)
    #po.cropBox.upperRight = (864, 432)
    po.mediaBox.lowerLeft = (0, 216)
    po.mediaBox.upperRight = (864, 432)
    po.compressContentStreams()                                                                                                     
    pw.addPage(po)

with open("e.pdf","wb") as f:
    pw.write(f)

```

截取成功，但奇怪的是，截取前后pdf的大小没有发生改变，使用identify查看发现：

原pdf信息

```
15PK1175-127_L1_I517.cnv.pdf[0] PDF 864x648 864x648+0+0 16-bit Bilevel DirectClass 70KB 0.040u 0:00.030
15PK1175-127_L1_I517.cnv.pdf[1] PDF 864x648 864x648+0+0 16-bit Bilevel DirectClass 70KB 0.040u 0:00.030
15PK1175-127_L1_I517.cnv.pdf[2] PDF 864x648 864x648+0+0 16-bit Bilevel DirectClass 70KB 0.040u 0:00.030
15PK1175-127_L1_I517.cnv.pdf[3] PDF 864x648 864x648+0+0 16-bit Bilevel DirectClass 70KB 0.030u 0:00.030
```

截取后pdf信息

```
e.pdf[0] PDF 864x216 864x216+0+0 16-bit Bilevel DirectClass 23.4KB 0.010u 0:00.010
e.pdf[1] PDF 864x216 864x216+0+0 16-bit Bilevel DirectClass 23.4KB 0.000u 0:00.010
e.pdf[2] PDF 864x216 864x216+0+0 16-bit Bilevel DirectClass 23.4KB 0.000u 0:00.010
e.pdf[3] PDF 864x216 864x216+0+0 16-bit Bilevel DirectClass 23.4KB 0.000u 0:00.010
```

每页图片大小确实变小了，但看整个pdf大小竟然没有变小。遇到这种情况，看来只能会用gs压缩了：

```
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dQUIET -dBATCH -sOutputFile=e.pdf f.pdf
```

**为PDF页面添加文本**

* [Python添加pdf水印](http://blog.51cto.com/walkerqt/1378142)
* [使用Python将文本添加到现有PDF](http://landcareweb.com/questions/5051/shi-yong-pythonjiang-wen-ben-tian-jia-dao-xian-you-pdf)
* [用PDFlib给PDF添加水印（Python）](http://www.voidcn.com/article/p-pensbcbe-dh.html)

用到两个扩展模块：ReportLab、PyPDF2。

**创建水印PDF**

1 创建文字水印pdf文件

```
#encoding=utf-8
#author: walker
#date: 2014-03-17
#function: 创建文字水印pdf
from reportlab.pdfgen import canvas
from reportlab.lib.units import cm
def create_watermark(content):
    #默认大小为21cm*29.7cm
    c = canvas.Canvas("mark.pdf", pagesize = (30*cm, 30*cm))
    #移动坐标原点(坐标系左下为(0,0))
    c.translate(10*cm, 5*cm)
                                                                                                                               
    #设置字体
    c.setFont("Helvetica", 80)
    #指定描边的颜色
    c.setStrokeColorRGB(0, 1, 0)
    #指定填充颜色
    c.setFillColorRGB(0, 1, 0)
    #画一个矩形
    c.rect(cm, cm, 7*cm, 17*cm, fill=1)
                                                                                                                               
    #旋转45度，坐标系被旋转
    c.rotate(45)
    #指定填充颜色
    c.setFillColorRGB(0.6, 0, 0)
    #设置透明度，1为不透明
    c.setFillAlpha(0.3)
    #画几个文本，注意坐标系旋转的影响
    c.drawString(3*cm, 0*cm, content)
    c.setFillAlpha(0.6)
    c.drawString(6*cm, 3*cm, content)
    c.setFillAlpha(1)
    c.drawString(9*cm, 6*cm, content)
                                                                                                                               
    #关闭并保存pdf文件
    c.save()
create_watermark('walker')
```

2. 创建图片水印pdf

```
#encoding=utf-8
#author: walker
#date: 2014-03-17
#function: 创建图片水印pdf
from reportlab.pdfgen import canvas
from reportlab.lib.units import cm
def create_watermark(f_jpg):
    f_pdf = 'mark.pdf'
    w_pdf = 20*cm
    h_pdf = 20*cm
                                                                                          
    c = canvas.Canvas(f_pdf, pagesize = (w_pdf, h_pdf))
    c.setFillAlpha(0.3) #设置透明度
    print c.drawImage(f_jpg, 7*cm, 7*cm, 6*cm, 6*cm)    #这里的单位是物理尺寸
    c.save()
create_watermark('eg.png')
```

**添加水印**

```
#encoding=utf-8
#author: walker
#date: 2014-03-18
#function:给pdf添加水印
from PyPDF2 import PdfFileWriter, PdfFileReader
from reportlab.pdfgen import canvas
#所有路径为绝对路径
def add_watermark(pdf_file_in, pdf_file_mark, pdf_file_out):
    pdf_output = PdfFileWriter()
    input_stream = file(pdf_file_in, 'rb')
    pdf_input = PdfFileReader(input_stream)
                                                                               
    # PDF文件被加密了
    if pdf_input.getIsEncrypted():
        print '该PDF文件被加密了.'
        # 尝试用空密码解密
        try:
            pdf_input.decrypt('')
        except Exception, e:
            print '尝试用空密码解密失败.'
            return False
        else:
            print '用空密码解密成功.'
    # 获取PDF文件的页数
    pageNum = pdf_input.getNumPages()
    #读入水印pdf文件
    pdf_watermark = PdfFileReader(file(pdf_file_mark, 'rb'))
    # 给每一页打水印
    for i in range(pageNum):
        page = pdf_input.getPage(i)
        page.mergePage(pdf_watermark.getPage(0))
        page.compressContentStreams()   #压缩内容
        pdf_output.addPage(page)
```

这种方式唯一的缺点就是效率极低，不适合大批量文件处理。主要限速步骤是page.mergePage()和
page.compressContentStreams()。要想加速，可以换一种思维：添加空白页，在空白页上添加文本，
再将该页添加到pdf中，即可避免使用这两个函数。

用PDFlib处理效率会比这种方式高几十倍。



### 11. matplotlib

* [matplotlib核心剖析](http://www.cnblogs.com/vamei/archive/2013/01/30/2879700.html)
* [Matplotlib 教程](http://www.runoob.com/w3cnote/matplotlib-tutorial.html)


* `设置中文字体`: [matplotlib显示中文](https://www.cnblogs.com/hhh5460/p/4323985.html)



**1.python matplotlib 画的多张图，如何合并写入同一pdf？**

官方文档提供了一个解决方案: [pylab_examples example code: multipage_pdf.py](https://link.zhihu.com/?target=https%3A//matplotlib.org/examples/pylab_examples/multipage_pdf.html)

```
import datetime
import numpy as np
from matplotlib.backends.backend_pdf import PdfPages
import matplotlib.pyplot as plt

with PdfPages('multipage_pdf.pdf') as pdf:
    plt.figure(figsize=(3, 3))
    #对figure进行操作
    pdf.savefig()  # 将当前图存为pdf中的一页
    plt.close()

    # 创建更多的图并存为pdf

    # 为pdf文件添加辅助信息
    d = pdf.infodict()
    d['Title'] = 'Multipage PDF Example'
    d['Author'] = u'Jouni K. Sepp\xe4nen'
    d['Subject'] = 'How to create a multipage pdf file and set its metadata'
    d['Keywords'] = 'PdfPages multipage keywords author title subject'
    d['CreationDate'] = datetime.datetime(2009, 11, 13)
    d['ModDate'] = datetime.datetime.today()
```

**2. 箱线图**

* [箱线图boxplot](https://www.cnblogs.com/wyy1480/p/9526264.html)

plt.boxplot(x, notch=None, sym=None, vert=None, whis=None, positions=None, widths=None, patch_artist=None,

            bootstrap=None, usermedians=None, conf_intervals=None, meanline=None, showmeans=None, 

            showcaps=None, showbox=None, showfliers=None, boxprops=None, labels=None, flierprops=None,

            medianprops=None, meanprops=None, capprops=None, whiskerprops=None, manage_xticks=True,

            autorange=False, zorder=None, hold=None, data=None)

* x：指定要绘制箱线图的数据；
* notch：是否是凹口的形式展现箱线图，默认非凹口；
* sym：指定异常点的形状，默认为+号显示；
* vert：是否需要将箱线图垂直摆放，默认垂直摆放；
* whis：指定上下须与上下四分位的距离，默认为1.5倍的四分位差；
* positions：指定箱线图的位置，默认为[0,1,2…]；
* widths：指定箱线图的宽度，默认为0.5；
* patch_artist：是否填充箱体的颜色；
* meanline：是否用线的形式表示均值，默认用点来表示；
* showmeans：是否显示均值，默认不显示；
* showcaps：是否显示箱线图顶端和末端的两条线，默认显示；
* showbox：是否显示箱线图的箱体，默认显示；
* showfliers：是否显示异常值，默认显示；
* boxprops：设置箱体的属性，如边框色，填充色等；
* labels：为箱线图添加标签，类似于图例的作用；
* filerprops：设置异常值的属性，如异常点的形状、大小、填充色等；
* medianprops：设置中位数的属性，如线的类型、粗细等；
* meanprops：设置均值的属性，如点的大小、颜色等；
* capprops：设置箱线图顶端和末端线条的属性，如颜色、粗细等；
* whiskerprops：设置须的属性，如颜色、粗细、线的类型等；


```python
# https://github.com/matplotlib/matplotlib.github.com/blob/master/mpl_examples/statistics/boxplot_demo.py

boxprops = dict(linestyle='--', linewidth=3, color='darkgoldenrod')
flierprops = dict(marker='o', markerfacecolor='green', markersize=12,
                  linestyle='none')
medianprops = dict(linestyle='-.', linewidth=2.5, color='firebrick')
meanpointprops = dict(marker='D', markeredgecolor='black',
                      markerfacecolor='firebrick')
meanlineprops = dict(linestyle='--', linewidth=2.5, color='purple')

plt.boxplot(data, meanprops=meanpointprops, meanline=False,
                   showmeans=True)
```


**设置中文字体**

```
import numpy as np 
from matplotlib import pyplot as plt 
import matplotlib
 
# fname 为 你下载的字体库路径，注意 SimHei.ttf 字体的路径
zhfont1 = matplotlib.font_manager.FontProperties(fname="SimHei.ttf") 
 
x = np.arange(1,11) 
y =  2  * x +  5 
plt.title("菜鸟教程 - 测试", fontproperties=zhfont1) 
 
# fontproperties 设置中文显示，fontsize 设置字体大小
plt.xlabel("x 轴", fontproperties=zhfont1)
plt.ylabel("y 轴", fontproperties=zhfont1)
plt.plot(x,y) 
plt.show()
```


### 12. Bokeh

* [干货推荐 | 掌握这几点，轻松玩转 Bokeh 可视化 （项目实战经验分享）](https://mp.weixin.qq.com/s/ArXJyT2LOPWMXNOLh8xv5A)


### 13. tqdm

* [使用python Tqdm进度条库让你的python进度可视化](https://ptorch.com/news/170.html)

当我们使用pip或conda安装包的时候，安装进度条是怎么生成的呢？没错，就是tqdm！


### 14. statsmodels

普通最小二乘法（OLS）

* [Python统计分析库statsmodels的OLS](https://blog.csdn.net/cymy001/article/details/78364652)

```
import statsmodels.api as sm 
#最小二乘
from statsmodels.stats.outliers_influence import summary_table 
#获得汇总信息

x=sm.add_constant(daily_data['temp'])
#线性回归增加常数项 y=kx+b
y=daily_data['cnt']
regr=sm.OLS(y,x)
res=regr.fit() 

st, data, ss2 = summary_table(res, alpha=0.05) 
#置信水平alpha=5%，st数据汇总，data数据详情，ss2数据列名
fitted_values = data[:,2]  
#等价于res.fittedvalues
```


### 15. sklearn

**数据集**

使用sklearn.datasets.load_boston即可加载相关数据。该数据集是一个回归问题。
每个类的观察值数量是均等的，共有 506 个观察，13 个输入变量和1个输出变量。

每条数据包含房屋以及房屋周围的详细信息。其中包含城镇犯罪率，一氧化氮浓度，
住宅平均房间数，到中心区域的加权距离以及自住房平均房价等等。

* CRIM：城镇人均犯罪率。
* ZN：住宅用地超过 25000 sq.ft. 的比例。
* INDUS：城镇非零售商用土地的比例。
* CHAS：查理斯河空变量（如果边界是河流，则为1；否则为0）。
* NOX：一氧化氮浓度。
* RM：住宅平均房间数。
* AGE：1940 年之前建成的自用房屋比例。
* DIS：到波士顿五个中心区域的加权距离。
* RAD：辐射性公路的接近指数。
* TAX：每 10000 美元的全值财产税率。
* PTRATIO：城镇师生比例。
* B：1000（Bk-0.63）^ 2，其中 Bk 指代城镇中黑人的比例。
* LSTAT：人口中地位低下者的比例。
* MEDV：自住房的平均房价，以千美元计。

预测平均值的基准性能的均方根误差（RMSE）是约 9.21 千美元。



### 15. seaborn

JointGrid

```
import seaborn as sns
from scipy import stats
g1 = sns.JointGrid(x, y, space=0, dropna=True, xlim=(0.2, 0.8), ylim=(0, 80))\                                       
        .plot_joint(plt.scatter, c="black", s=0.8)\
        .plot_marginals(sns.kdeplot, gridsize=200, shade=True, color="black")\
        .annotate(stats.pearsonr)\
        .set_axis_labels("GC content", "Reads count")
```

怎么在一张图上画两个JointGrid？

[How to plot multiple Seaborn Jointplot in Subplot](https://stackoverflow.com/questions/35042255/how-to-plot-multiple-seaborn-jointplot-in-subplot)

```
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec
import seaborn as sns
import numpy as np

class SeabornFig2Grid():

    def __init__(self, seaborngrid, fig,  subplot_spec):
        self.fig = fig
        self.sg = seaborngrid
        self.subplot = subplot_spec
        if isinstance(self.sg, sns.axisgrid.FacetGrid) or \
            isinstance(self.sg, sns.axisgrid.PairGrid):
            self._movegrid()
        elif isinstance(self.sg, sns.axisgrid.JointGrid):
            self._movejointgrid()
        self._finalize()

    def _movegrid(self):
        """ Move PairGrid or Facetgrid """
        self._resize()
        n = self.sg.axes.shape[0]
        m = self.sg.axes.shape[1]
        self.subgrid = gridspec.GridSpecFromSubplotSpec(n,m, subplot_spec=self.subplot)
        for i in range(n):
            for j in range(m):
                self._moveaxes(self.sg.axes[i,j], self.subgrid[i,j])

    def _movejointgrid(self):
        """ Move Jointgrid """
        h= self.sg.ax_joint.get_position().height
        h2= self.sg.ax_marg_x.get_position().height
        r = int(np.round(h/h2))
        self._resize()
        self.subgrid = gridspec.GridSpecFromSubplotSpec(r+1,r+1, subplot_spec=self.subplot)

        self._moveaxes(self.sg.ax_joint, self.subgrid[1:, :-1])
        self._moveaxes(self.sg.ax_marg_x, self.subgrid[0, :-1])
        self._moveaxes(self.sg.ax_marg_y, self.subgrid[1:, -1])

    def _moveaxes(self, ax, gs):
        #https://stackoverflow.com/a/46906599/4124317
        ax.remove()
        ax.figure=self.fig
        self.fig.axes.append(ax)
        self.fig.add_axes(ax)
        ax._subplotspec = gs
        ax.set_position(gs.get_position(self.fig))
        ax.set_subplotspec(gs)

    def _finalize(self):
        plt.close(self.sg.fig)
        self.fig.canvas.mpl_connect("resize_event", self._resize)
        self.fig.canvas.draw()

    def _resize(self, evt=None):
        self.sg.fig.set_size_inches(self.fig.get_size_inches())
```

用法如下：

```
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec
import seaborn as sns; sns.set()
import SeabornFig2Grid as sfg


iris = sns.load_dataset("iris")
tips = sns.load_dataset("tips")

# An lmplot
g0 = sns.lmplot(x="total_bill", y="tip", hue="smoker", data=tips, 
                palette=dict(Yes="g", No="m"))
# A PairGrid
g1 = sns.PairGrid(iris, hue="species")
g1.map(plt.scatter, s=5)
# A FacetGrid
g2 = sns.FacetGrid(tips, col="time",  hue="smoker")
g2.map(plt.scatter, "total_bill", "tip", edgecolor="w")
# A JointGrid
g3 = sns.jointplot("sepal_width", "petal_length", data=iris,
                   kind="kde", space=0, color="g")


fig = plt.figure(figsize=(13,8))
gs = gridspec.GridSpec(2, 2)

mg0 = sfg.SeabornFig2Grid(g0, fig, gs[0])
mg1 = sfg.SeabornFig2Grid(g1, fig, gs[1])
mg2 = sfg.SeabornFig2Grid(g2, fig, gs[3])
mg3 = sfg.SeabornFig2Grid(g3, fig, gs[2])

gs.tight_layout(fig)
#gs.update(top=0.7)

plt.show()
```



## 黑客模块

### 1. pywin32

* [Win32API参考手册](http://www.yfvb.com/help/win32sdk/index.htm?page=html/tizm5q.htm)
* [pywin32-docs](http://timgolden.me.uk/pywin32-docs/contents.html)


### 2. psutil

* [github](https://github.com/giampaolo/psutil)
* [python模块之psutil详解](https://www.cnblogs.com/saneri/p/7528283.html)
* [psutil 实现netstat的功能来获得本机的所有网络连接(网络端口)](https://github.com/giampaolo/psutil/blob/master/scripts/netstat.py)

psutil是一个跨平台库(http://pythonhosted.org/psutil/)能够轻松实现获取系统运行的进程和系统利用率
（包括CPU、内存、磁盘、网络等）信息。它主要用来做系统监控，性能分析，进程管理。它实现了同等命令行工具提供的功能，
如ps、top、lsof、netstat、ifconfig、who、df、kill、free、nice、ionice、iostat、iotop、uptime、pidof、tty、taskset、pmap等。
目前支持32位和64位的Linux、Windows、OS X、FreeBSD和Sun Solaris等操作系统.

### 3. pypcap

pypcap 是 WinPcap 或libpcap 的 python 接口, 可以捕获网络数据封包


### 4. pyhook

[pyHook监测键盘鼠标事件等](https://www.cnblogs.com/franknihao/p/7904434.html)

pyHook是一个用来进行键盘、鼠标等层面事件监控的库。这个库的正常工作需要pythoncom等操作系统的API的支持


### 5. PyUserInput

[Python-模拟鼠标键盘动作](https://www.jianshu.com/p/552f96aa85dc)

PyUserInput中的pymouse和pykeyboard模块可以用来进行键盘、鼠标等层面事件监控


### 6. pydivert

[github](https://github.com/ffalcinelli/pydivert)

pydivert 是 WinDivert 的python接口。与WinPcap只能复制封包副本不同，WinDivert能够截获封包，
修改并发送到目标地址。



### 7. redsails

[超级隐蔽之后门技巧](https://blog.csdn.net/Fly_hps/article/details/80428167)

Redsails是使用python开发的一款后渗透测试工具，其目的是可以使我们在目标主机上执行命令且无需创建任何事件日志以及网络连接.




----


# 3. 模块比较

## 3.1. xml解析模块

>常见的XML编程接口有DOM和SAX，这两种接口处理XML文件的方式不同，当然使用场合也不同。

python有三种方法解析XML:
        * `SAX (simple API for XML )`   #python 标准库包含SAX解析器，SAX用事件驱动模型，通过在解析XML的过程中触发一个个的事件并调用用户定义的回调函数来处理XML文件。
        * `DOM (Document Object Model)`   #将XML数据在内存中解析成一个树，通过对树的操作来操作XML。
        * `ElementTree (元素树)`  #ElementTree就像一个轻量级的DOM，具有方便友好的API。代码可用性好，速度快，消耗内存少。

>DOM需要将XML数据映射到内存中的树，一是比较慢，二是比较耗内存，
SAX流式读取XML文件，比较快，占用内存少，但需要用户实现回调函数（handler）。
ElementTree就像一个轻量级的DOM，具有方便友好的API。代码可用性好，速度快，消耗内存少。

ElementTree常用模块包括：[xml.etree.ElementTree](https://docs.python.org/3/library/xml.etree.elementtree.html#module-xml.etree.ElementTree)和[lxml](http://lxml.de/tutorial.html)
>`xml.etree.ElementTree`功能比较简单，但不支持复杂操作
`lxml`类似`xml.etree.ElementTree`，但功能更全，能够进行复杂操作，同时能够完全支持[xpath](http://www.w3school.com.cn/xpath/xpath_syntax.asp)语法，查询功能非常强大

```

try:
  from lxml import etree
  print("running with lxml.etree")
except ImportError:
  try:
    # Python 2.5
    import xml.etree.cElementTree as etree
    print("running with cElementTree on Python 2.5+")
  except ImportError:
    try:
      # Python 2.5
      import xml.etree.ElementTree as etree
      print("running with ElementTree on Python 2.5+")
    except ImportError:
      try:
        # normal cElementTree install
        import cElementTree as etree
        print("running with cElementTree")
      except ImportError:
        try:
          # normal ElementTree install
          import elementtree.ElementTree as etree
          print("running with ElementTree")
        except ImportError:
          print("Failed to import ElementTree from any known place")
```
**结论：**<font color="red">**强烈**推荐使用**lxml**</font>


----

# 4. 学习资料

## 4.1 Python 资源大全中文版

[github](https://github.com/jobbole/awesome-python-cn)

我想很多程序员应该记得 GitHub 上有一个 Awesome - XXX 系列的资源整理。awesome-python 是 vinta 发起维护的 Python 资源列表，内容包括：Web 框架、网络爬虫、网络内容提取、模板引擎、数据库、数据可视化、图片处理、文本处理、自然语言处理、机器学习、日志、代码分析等。由伯乐在线持续更新。
 
Awesome 系列虽然挺全，但基本只对收录的资源做了极为简要的介绍，如果有更详细的中文介绍，对相应开发者的帮助会更大。这也是我们发起这个开源项目的初衷。


## 4.2 \<\<Python Cookbook\>\>

[Python Cookbook 3rd Edition Documentation](https://python3-cookbook-personal.readthedocs.io/zh_CN/latest/index.html)


## 4.3 python各路大神

* [Armin Ronacher(阿明·罗纳彻)](https://github.com/pallets), 代表作：flask，werkzeug，jinja，click
* [Kenneth Reitz(肯尼斯·赖茨)](https://github.com/kennethreitz), 代表作：requests, pipenv, python-guide


## 4.4 Python Code Examples

[Python Code Examples](https://www.programcreek.com/python/)

## 4.5 openCV

[http://blog.csdn.net/gangzhucoll/article/category/7284578/1](http://blog.csdn.net/gangzhucoll/article/category/7284578/1)

* [Python3与OpenCV3.3 图像处理（一）--环境搭建与简单DEMO](http://blog.csdn.net/gangzhucoll/article/details/78516292)
* [Python3与OpenCV3.3 图像处理（二）--图像基本操作](http://blog.csdn.net/gangzhucoll/article/details/78525898)
* [Python3与OpenCV3.3 图像处理（三）--Numpy数组操作 ](http://blog.csdn.net/gangzhucoll/article/details/78546290)
* [Python3与OpenCV3.3 图像处理（补）--第三节补充 ](http://blog.csdn.net/gangzhucoll/article/details/78569619)
* [Python3与OpenCV3.3 图像处理（四）--色彩空间 ](http://blog.csdn.net/gangzhucoll/article/details/78574856)
* [Python3与OpenCV3.3 图像处理（五）--图像运算 ](http://blog.csdn.net/gangzhucoll/article/details/78598238)
* [Python3与OpenCV3.3 图像处理(六）--ROI ](http://blog.csdn.net/gangzhucoll/article/details/78609771)
* [Python3与OpenCV3.3 图像处理(七）--洪填充 ](http://blog.csdn.net/gangzhucoll/article/details/78650056)
* [Python3与OpenCV3.3 图像处理(八）--模糊 ](http://blog.csdn.net/gangzhucoll/article/details/78660422)
* [Python3与OpenCV3.3 图像处理(九）--高斯模糊 ](http://blog.csdn.net/gangzhucoll/article/details/78682492)
* [Python3与OpenCV3.3 图像处理(十)--EPF ](http://blog.csdn.net/gangzhucoll/article/details/78700989)
* [Python3与OpenCV3.3 图像处理(十一)--图像直方图 ](http://blog.csdn.net/gangzhucoll/article/details/78715208)
* [Python3与OpenCV3.3 图像处理(十二)--图像直方图应用 ](http://blog.csdn.net/gangzhucoll/article/details/78726069)
* [Python3与OpenCV3.3 图像处理(十三)--反射投影 ](http://blog.csdn.net/gangzhucoll/article/details/78736768)
* [Python3与OpenCV3.3 图像处理(十四)--模板匹配 ](http://blog.csdn.net/gangzhucoll/article/details/78747256)
* [Python3与OpenCV3.3 图像处理(十五)--图像二值化 ](http://blog.csdn.net/gangzhucoll/article/details/78760747)
* [Python3与OpenCV3.3 图像处理(补)--第十五节补充 ](http://blog.csdn.net/gangzhucoll/article/details/78768283)
* [Python3与OpenCV3.3 图像处理(十六）--图像金字塔 ](http://blog.csdn.net/gangzhucoll/article/details/78787377)
* [Python3与OpenCV3.3 图像处理(十七）--图像梯度 ](http://blog.csdn.net/gangzhucoll/article/details/78808064)
* [Python3与OpenCV3.3 图像处理(十八）--Canny边缘提取 ](http://blog.csdn.net/gangzhucoll/article/details/78824590)
* [Python3与OpenCV3.3 图像处理(十九）--直线检测 ](http://blog.csdn.net/gangzhucoll/article/details/78848597)
* [Python3与OpenCV3.3 图像处理(二十一）--轮廓发现 ](http://blog.csdn.net/gangzhucoll/article/details/78868703)
* [Python3与OpenCV3.3 图像处理(二十二）--对象测量（纯代码） ](http://blog.csdn.net/gangzhucoll/article/details/78886960)
* [Python3与OpenCV3.3 图像处理(二十三）--膨胀与腐蚀 ](http://blog.csdn.net/gangzhucoll/article/details/78917011)
* [Python3与OpenCV3.3 图像处理(二十四）--开闭操作 ](http://blog.csdn.net/gangzhucoll/article/details/78927295)
* [Python3与OpenCV3.3 图像处理(二十五）--开闭操作（补充](http://blog.csdn.net/gangzhucoll/article/details/78956799)


----

# 5. 编写规范

## 5.1 软件目录结构规范

[Python-软件开发规范](https://www.cnblogs.com/guoxiangqian/p/7698081.html)

[python 软件目录结构规范](https://www.cnblogs.com/JayeHe/p/6696848.html)

[python基础——软件目录规范](http://blog.csdn.net/jorocco/article/details/77773648)

```
.
├── bin                                         # 用来放程序执行文件
│   └── start.py
├── conf                                       # 配置文件
│   ├── config.ini
│   ├── __init__.py
│   └── setting.py
├── core                                      # 放程序的核心逻辑
│   ├── __init__.py
│   ├── main.py
│   └── tests
│       ├── __init__.py
│       └── test_main.py
├── db                                         # 数据文件
├── docs                                      #  存放文档
├── lib                                          # 放模块和包
├── log                                        # 日志文件
├── README.txt                       # 项目说明文件
├── requirements.txt                    # 存放软件依赖的外部Python包列表
└── setup.py                                # 安装、部署、打包的脚本
```

**`start.py`**

```
import os
import sys

pipeline_dir = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
sys.path.append(pipeline_dir)

from core import main

if __name__ == "__main__":
    main.print_setting()
```

**`setting.py`**

```
AUTHOR = {
    "NAME": "luyl",
    "EMAIL": "luyl@biomarker.com.cn",
    "AGE": 27
}

BASE = {
    "DEBUG": True,
    "DIR": ""
}

MATH = {
    "PI": 3.1415,
    "E": 2.718
}
```

**`main.py`**

```
from conf import setting

def print_setting():
    print(setting.AUTHOR)
    print(setting.MATH)
    print(setting.BASE)
```

## 5.2 宏基因组项目框架

主要涉及到搭建框架的思路，以及｀日志记录｀和｀全局配置文件｀

```
.
├── bin
│   └── metagenome.py
├── conf
│   ├── base.config
│   ├── config.py
│   ├── __init__.py
│   ├── logging.config
│   └── metagenome.config
├── core
│   ├── __init__.py
│   └── metagenome.py
├── lib
│   ├── assembly.py
│   ├── base.py
│   └── __init__.py
├── requirements.txt
├── script
│   └── sleep.sh
└── test
    ├── config_test.py
    └── test.py
```

`bin/metagenome.py`

```
#conding:utf-8

import sys 
import os

pipeline_dir = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

sys.path.append(pipeline_dir)

from core import metagenome

if __name__ == "__main__":
    metagenome.run()
```

`core/metagenome.py`

```
import os
import logging
import logging.config
from os.path import join as pjoin

from conf.config import parse_config
from conf.config import Config as config
from lib.base import runOrDie
from lib.assembly import threadAssembly

CURRENT_DIR = os.path.dirname(os.path.abspath(__file__))
PROJECT_DIR = os.path.dirname(CURRENT_DIR)
CONFIG_DIR = pjoin(PROJECT_DIR, "conf")

logging_conf = pjoin(CONFIG_DIR, "logging.config")
logging.config.fileConfig(logging_conf)
root_logger = logging.getLogger("root")
logger = logging.getLogger("metagenome")

print config.config
metagenome_config = parse_config(pjoin(CONFIG_DIR, "metagenome.config"))
config.update(metagenome_config)

def data_processing():
    runOrDie(pjoin(PROJECT_DIR, "script/sleep.sh"))

def myassembly():
    threadAssembly()


def run():
    data_processing()
    myassembly()
```

`conf/config.py`

```
import os
import json

current_dir = os.path.dirname(os.path.abspath(__file__))

with open(os.path.join(current_dir, "base.config"), "r") as f:
    config = json.load(f)

class Config(object):
    config = config

    @classmethod
    def update(cls, myconf):
        def update_config(oldconfig, newconfig):
            for key in newconfig:
                if key in oldconfig and type(oldconfig[key]) == dict:
                    update_config(oldconfig[key], newconfig[key])
                else:
                    oldconfig[key] = newconfig[key]
        config = cls.config
        update_config(config, myconf)

def parse_config(config_file):
    """config_file: JSON format"""
    config_fp = open(config_file)
    config = json.load(config_fp)
    config_fp.close()
    return config
```

`conf/base.config`

```
{
    "software": {
        "cd-hit": "/share/nas2/genome/biosoft/cd-hit/v4.6.1",
        "perl": "/share/nas2/genome/biosoft/perl/5.20.0/bin/perl",
        "apython2": "/share/nas2/genome/biosoft/Anaconda2/4.1.1/bin/python -u"
    },
    "database": {
        "Nr": "/share/nas2/database/Micro_Refs/nr_meta/nr_meta_16_3_7/nr_meta",
        "Nt": "/share/nas2/database/ncbi/nr"
    }
}
```

`conf/logging.config`

```
[loggers] 
keys=root,main
 
[handlers] 
keys=consoleHandler,fileHandler 
 
[formatters] 
keys=fmt 
 
[logger_root] 
level=DEBUG 
handlers=consoleHandler 
 
[logger_main] 
level=DEBUG 
qualname=main 
handlers=fileHandler 
 
[handler_consoleHandler] 
class=StreamHandler 
level=DEBUG 
formatter=fmt 
args=(sys.stdout,) 
 
[handler_fileHandler] 
class=logging.handlers.RotatingFileHandler 
level=DEBUG 
formatter=fmt 
args=('main.log','w',100000000,5,) 
 
[formatter_fmt] 
format=%(asctime)s - %(name)s - %(threadName)s - %(levelname)s : %(message)s 
datefmt= %Y-%m-%d %H:%M:%S
```

`lib/assembly.py`

```
import logging
from time import sleep
from threading import Thread

from conf.config import Config as config
from lib.base import runOrDie

logger = logging.getLogger("main.assembly")

def assembly():
    logger.info("start assembly")
    sleep(1)
    print config.config
    logger.info("assembly end")

def threadAssembly():
    t = Thread(target=assembly, name="assembly")
    t.start()
```

`lib/base.py`

```
import os
import logging

logger = logging.getLogger("main.lib.base")

def runOrDie(shfile):
    cmd = "sh -e {} &> {}.log".format(shfile, shfile)
    logger.info(cmd)
    flag = os.system(cmd)
    if flag:
        logger.error("fail. {}".format(cmd))
        exit(1)
```



----

# 6. 常见问题

##  6.1 `mkl_serv_getenv: undefined symbol: mkl_serv_getenv`

github 解答：[https://github.com/conda/conda/issues/2031](https://github.com/conda/conda/issues/2031)

额外知识补充：
MKL( Intel Math Kernel Library)是`英特尔`的`数学核心函数库`。
`numpy`, `scipy`, `pandas`, `scikit-learn` and `numexpr` 都会调用MKL来提高计算性能。


## 6.2 `nicodeEncodeError: 'charmap' codec can't encode characters in position 7-8: character maps to <undefined>`

[python(三)：Python3—UnicodeEncodeError 'ascii' codec can't encode characters in position 0-1](https://blog.csdn.net/AckClinkz/article/details/78538462)

[python 3.2 UnicodeEncodeError: 'charmap' codec can't encode character '\u2013' in position 9629: character maps to <undefined>](https://stackoverflow.com/questions/16346914/python-3-2-unicodeencodeerror-charmap-codec-cant-encode-character-u2013-i)





----

# 7. 优秀框架

## 爬虫

### pyspider

[pyspider源码](https://github.com/binux/pyspider)

[网络爬虫剖析，以Pyspider为例](http://python.jobbole.com/81109/)

[Python爬虫进阶四之PySpider的用法](https://cuiqingcai.com/2652.html)

[]()

### scrapy

**scrapy如何处理404等状态的地址**

>默认情况下scrapy会把404等一些错误状态码的response直接过滤掉，我现在想让它不过滤掉，然后我自己判断状态码是否为404，进行后续操作，我查过官方文档，可以通过自己编写一个中间件，设置HttpErrorMiddleware.handle_httpstatus_list=[404]，就可以处理返回为404的response，但我试了，也不行，我想问问有什么办法可以达到我说的这种效果？

在spider的类中把404放在handle_httpstatus_list中。如下就行。

```
class MySpider(CrawlSpider):
    handle_httpstatus_list = [404]
```


## web服务

### Flask

[从零开始搭建论坛（1）：Web服务器与Web框架](http://python.jobbole.com/85874/)

[从零开始搭建论坛（2）：Web服务器网关接口](http://python.jobbole.com/85963/)

[从零开始搭建论坛（3）：Flask框架简介](http://python.jobbole.com/86707/)

[Flask web 开发(1):安装 - Python - 伯乐在线](http://python.jobbole.com/85943/)

[Flask web开发(2):程序的基本结构 - Python - 伯乐在线](http://python.jobbole.com/85944/)

[Flask web开发(3):模板 - Python - 伯乐在线](http://python.jobbole.com/85970/)

[Flask、Django、Pyramid三个框架的对比](http://python.jobbole.com/81396/)

[Flask 框架简介](http://python.jobbole.com/88621/?utm_source=blog.jobbole.com&utm_medium=relatedPosts)

[Flask零基础到项目实战 似水流年 CSDN博客]

**[专栏:我是怎么用flask开发个人博客的 - CSDN博客](http://blog.csdn.net/column/details/13819.html?page=1)**

[http://xiaorui.cc/](http://xiaorui.cc/)


常见问题：

[创建和部署flask中有关migrate可能遇到的问题](http://blog.csdn.net/kkevinyang/article/details/52183768)


### Django

文档：

* [Django 1.8.2 文档](https://yiyibooks.cn/xx/django_182/ref/forms/widgets.html)
* [Django 文档](https://docs.djangoproject.com/zh-hans/2.1/)
* [The Django Book](http://djangobook.py3k.cn/2.0/)

* [Form中字段及插件](https://www.jianshu.com/p/c4f1c25feb1c)
* [python 中单独调用 django 的数据库模块](https://cloud.tencent.com/developer/article/1005565)
* [Django 定时任务实现（django-crontab+command）](https://www.cnblogs.com/perfe/p/6198213.html)
* [django定时任务实现](https://blog.csdn.net/kong2030/article/details/82315251)
* [Django核心基础(5)：表单(Forms)的使用与验证](https://zhuanlan.zhihu.com/p/37558298)
* [python django 数据库查询方法总结](http://127.0.0.1:8000/pgs/search/)
* [django的登录注册系统](https://www.jianshu.com/p/0a1145167a8d)
* [[Django]几种重定向的方式](https://blog.csdn.net/orangleliu/article/details/38347863)

分页功能:

* [django 1.11通用视图自带分页功能](https://blog.csdn.net/l475378094/article/details/76850725)
* [Django之分页功能](https://www.cnblogs.com/kongzhagen/p/6640975.html)

Bootstrap美化：

* [有关Bootstrap你想要知道的都在这里](https://zhuanlan.zhihu.com/p/21472801)
* [Bootstrap 4 Tutorial](https://www.quackit.com/bootstrap/bootstrap_4/tutorial/)
* [Bootstrap4 教程](http://www.runoob.com/bootstrap4/bootstrap4-flex.html)
* [Bootstrap spacing间隔规范](http://code.z01.com/v4/utilities/spacing.html)

绘图：
* [echarts](http://echarts.baidu.com/examples/)

----

# 8. 第三方包安装教程

## 8.1 pypcap

[github](https://github.com/pynetwork/pypcap)

pypcap 是 WinPcap 的python接口。安装前需要先安装WinPcap，但win10系统不支持WinPcap，
所以可以使用Npcap来代替WinPcap。

具体安装步骤如下：

1. Npcap需要先安装nmap，而nmap又需要安装 Microsoft Visual C++ 14.0，所以第一步我们先安装VC++。[点击此处下载](https://go.microsoft.com/fwlink/?LinkId=691126), 差不多3G左右。 （python2可能需要Microsoft Visual C++ 9.0） [参考](https://blog.csdn.net/weixin_41184241/article/details/80144707)
2. 安装nmap: [nmap-7.70-setup.exe](https://nmap.org/dist/nmap-7.70-setup.exe), 安装时**一定要勾选Install Npcap in WinPcap API-compatible Mode**. [参考](https://nmap.org/download.html)
3. 下载[pypcap](https://github.com/pynetwork/pypcap)和[npcap-sdk-0.1.zip](https://nmap.org/npcap/), 并将他们解压后的文件夹放到同一级目录下，同时将npcap-sdk-0.1文件夹重命名为wpdpack
4. 进入pypcap文件夹中，执行：python setup.py install
5. 进入python， import pcap 检测是否成功



# 9. 常见问题及解决方案

## 9.1 numpy: ImportError: DLL load failed

解决方案：

添加以下5个path路径，并将其放到最前边：

* Anaconda3
* Anaconda3\Library\mingw-w64\bin
* Anaconda3\Library\usr\bin
* Anaconda3\Library\bin
* Anaconda3\Scripts