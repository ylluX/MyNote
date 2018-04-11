
# 目录
[TOC]

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
### 2. `str.split('\n')`与`str.splitlines`区别
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

***避免语法错误错误***
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

### 4. 多进程（multiprocessing和subprocess）
[廖雪峰的官方网站-多进程](
https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001431927781401bb47ccf187b24c3b955157bb12c5882d000)

多进程
阅读: 222005
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


### 5. 多线程
[Python-threading并发操作](http://blog.csdn.net/y2701310012/article/details/40863145)

### 6. 字符编码
[Python中文字符的理解：str()、repr()、print](https://www.cnblogs.com/omg24/p/5048319.html)
[python中文编码问题深入分析（二）：print打印中文异常及显示乱码问题分析与解决](https://www.cnblogs.com/litaozijin/p/6416133.html)
[廖雪峰的官方网站-字符串和编码](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001431664106267f12e9bef7ee14cf6a8776a479bdec9b9000)
[Python中的str与unicode处理方法](http://python.jobbole.com/81244/)
[从原理上搞定编码-- Base64编码](http://www.cnblogs.com/chengxiaohui/articles/3951129.html) 


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
itertools模块可创建的迭代器一般分为三类:
* **无限迭代器** （Infinite Iterators）
* **终止于最短输入序列的迭代器**   （Iterators terminating on the shortest input sequence）
* **组合生成器** （Combinatoric generators）


1. **无限迭代器**
`count`  : itertools.count(start, step)             # count(5, 2)     #从5开始的整数循环器，每次增加2，即5, 7, 9, 11, 13, 15 ...
`cycle`  : itertools.cycle(iterable)                  # cycle('abc')    #重复序列的元素，既a, b, c, a, b, c ...
`repeat` :  itertools.repeat(object[, times])    # repeat(1.2)     #重复1.2，构成无穷循环器，即1.2, 1.2, 1.2, ...
2. **终止于最短输入序列的迭代器**
`chain`   :  itertools.chain(*iterables)            # chain([1, 2, 3], [4, 5, 7])      # 连接两个迭代器成为一个。1, 2, 3, 4, 5, 7
`compress` :  itertools.compress(data, selectors)  # data为数据对象, selectors为选择器(规则) # compress([1,2,3], True,False,True])  # 返回数据对象中对应规则为True的元素 1,3

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
>>> Point = namedtuple('Point', ['x', 'y'])
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


### 2. pandas
1. **基本操作**
1.1. 小数位数 精度的处理round()
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


### 3. numpy
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
```


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
        return MyDataFrame

    @classmethod
    def read_csv(cls, *args, **kwargs):
        df = pd.read_csv(*args, **kwargs)
        return cls.copy_dateframe(df)

    @classmethod
    def copy_dateframe(cls, df):
        return cls(df.values, index=df.index, columns=df.columns)

    def __init__(*args, **kwargs):
        super(MyDataFrame, self).__init__(*args, **kwargs)
        self = self.add_month()

    def add_month(self):
        df = self.copy()
        df['month'] = 1 
        return df

    def get_month(self):
        return df[df['month']==month]

df = MyDataFrame.read_csv("test.csv").get_month(month)

```








### 4. click
[官网](http://click.pocoo.org/6/)
[命令行神器 Click 简明笔记](http://python.jobbole.com/87111/)
[pyspider源代码-run.py click模块](https://www.jianshu.com/p/fb75bcacaaa0)
[Python click.pass_context() Examples](https://www.programcreek.com/python/example/86569/click.pass_context)
[使用 Flask 开发 Web 应用（二）](https://segmentfault.com/a/1190000008426273)

* `click.group` : 命令可以通过group添加其他的命令.可以在脚本中随意嵌套
* `click.option` : 使用option()和argument()添加参数
* `click.version_option`: 添加一个--version选项,让程序在打印出version之后立即退出,Click 提供 eager 标识对参数名进行标识，如果输入该参数，则会拦截既定的命令行执行流程，跳转去执行一个回调函数
* `click.pass_context` : 返回当前上下文作为第一个参数传递给对应的方法. 每次一个命令被调用,一个新的上下文被处创建和指向父类上下文.通常,你看不到这些上下文.但是,上下文自动传递给参数和方法.命令可以通过 pass_context()来请求和传递上下文.在这种情况下上下文作文第一个参数.
*  `click.Choice` : 让一个参数有一个选择列表.

**自我总结**
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

## 4.2 Python Code Examples
[Python Code Examples](https://www.programcreek.com/python/)

## 4.2 openCV
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


----
# 7. 优秀框架

## 爬虫

### pyspider
[pyspider源码](https://github.com/binux/pyspider)
[网络爬虫剖析，以Pyspider为例](http://python.jobbole.com/81109/)
[Python爬虫进阶四之PySpider的用法](https://cuiqingcai.com/2652.html)
[]()

### scrapy

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
