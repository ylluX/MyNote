# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
* [目录](#目录)
* [Windows编程-基本知识](#windows编程-基本知识)
   * [TCHAR](#tchar)
* [Office](#office)
   * [Excel](#excel)
      * [基本函数](#基本函数)
<!--te-->

----

# Windows编程-基本知识

## TCHAR

C++支持两种字符集，如下：

```
ANSI字符集：Multi-Byte Character
Unicode字符集：Unicode Character
```

微软为了统一这两套编码，所以有了TCHAR，通过条件编译(_UNICODE宏和UNICODE宏)控制实际使用的字符集。

```
typedef char CHAR
typedef wchar_t WCHAR

typedef CHAR * PCHAR, * LPCH, * PCH, * NPSTR, * LPSTR, * PSTR;
typedef CONST CHAR * LPCCH, * PCCH, * LPCSTR, * PCSTR;

typedef WCHAR * PWCHAR, * LPWCH, * PWCH, * NWPSTR, * LPWSTR, * PWSTR;
typedef CONST WCHAR * LPCWCH, * PCWCH, * LPCWSTR, * PCWSTR;

#ifdef UNICODE
typedef WCHAR TCHAR, * PTCHAR;
typedef LPWSTR LPTCH, PTCH, PTSTR, LPTSTR;
typedef LPCWSTR LPCTSTR;
#define __TEXT(quote) L##quote
#else
typedef char TCHAR, * PTCHAR;
typedef LPSTR LPTCH, PTCH, PTSTR, LPTSTR;
typedef LPCSTR LPCTSTR;
#define __TEXT(quote) quote
#endif

#define TEXT(quote) __TEXT(quote)

```

TCHAR类型在Multi-Byte字符集下占1个字节，在Unicode字符集下占2个字节。同一个TCAHR类型的数组变量在不同字符集下，长度是不同的。

```
TCHAR ptszArray[10];
在Unicode字符集下，长度为20个字节
在Multi-Byte字符集下，长度为10个字节
```

----

# Office

## Excel

### 基本函数

[EXCEL常用函数汇总（以Excel 2016版举例）](https://www.jianshu.com/p/d7cc9314195f)

第一类：文本处理函数

* `HYPERLINK`：超链接
* `CONCATENATE`: 将两个或多个文本字符串联接为一个字符串
* `LEFT`: 从文本字符串的第一个字符开始返回指定个数的字符
* `RIGHT`: 用法同Left，只是取数方向相反，从右侧开始取数
* `MID`: 从字符串指定位置返回指定长度的字符
* `TRIM`: 除了单词之间的单个空格之外，移除文本中的所有空格
* `Replace`: 将特定位置的字符串替换为不同的文本字符
* `Substitue`: 在某一文本字符串中替换指定的文本

第二类：信息反馈函数

* `Exact`: 比较两个文本字符串，如果它们完全相同，则返回 TRUE，否则返回 FALSE。 
* `LEN`: 返回文本中字符的个数，一般和其他函数配合使用
* `IS`: 此类函数可检验指定值并根据结果返回 TRUE 或 FALSE。
ISBLANK(value)，ISERR(value)，ISERROR(value)，ISLOGICAL(value)，ISNA(value)，
ISNONTEXT(value)，ISNUMBER(value)，ISREF(value)，ISTEXT(value)

第三类：查找引用函数

* `Vlookup`: 在表格区域中按行查找对应内容。
* `Hlookup`: 在表格中按列查找对应内容。
* `Index`: 返回表格或区域中的值或值的引用
* `Match`: 在范围单元格中搜索特定的项，然后返回该项在此区域中的相对位置。
* `Search`: 函数可在第二个文本字符串中查找第一个文本字符串，并返回第一个文本字符串的起始位置的编号，该编号从第二个文本字符串的第一个字符算起。
* `FIND`: FIND函数区分大小写，并且不能使用通配符，其他用法和SEARCH函数一致。
* `Choose`: 根据参数返回数值参数列表中的数值。
* `Row / Column`: ROW([reference])返回引用的行号，COLUMN([reference])返回引用的列号，如果reference省略，则返回该函数所在位置的行/列号。
* `Offset`: 返回对单元格或单元格区域中指定行数和列数的区域的引用
* `Indirect`: 返回文本字符串指定的引用
* `Address`: 根据指定行号和列号获得工作表中的某个单元格的地址，如ADDRESS(2,3) 返回 $C$2。

第四类：逻辑运算函数

* `If`: 对值和期待值进行逻辑比较
* `Iferror`: 如果公式的计算结果错误，则返回您指定的值；否则返回公式的结果。 使用 IFERROR 函数可捕获和处理公式中的错误。
* `Ifna`: 如果公式返回错误值 #N/A，则结果返回您指定的值；否则返回公式的结果。
* `AND`:
* `OR`:
* `NOT`:


第五类：数学统计函数

* `Sum`:
* `Sumif`: 对符合条件的值求和，例如，对B2~B25单元格大于5的值求和，可以使用公式
* `Sumifs`: 用于计算其满足多个条件的全部参数的总量。
* `Sumproduct`: 在给定的几组数组中，将数组间对应的元素相乘，并返回乘积之和。
* `Count`: 计算包含数字的单元格个数以及参数列表中数字的个数。
* `Countif`: 用于统计满足某个条件的单元格的数量
* `Countifs`:
* `Counta`: 计算不为空的单元格的个数
* `Countblank`: 计算选中区域的空单元格个数。
* `Max / Min`:
* `Rank`: 返回一列数字的数字排位， 数字的排位是其相对于列表中其他值的大小
* `Rand`: 返回大于等于 0 且小于 1 的均匀分布随机实数，每次计算工作表时都将返回一个新的随机实数。如要产生a与b之间的随机实数，可用公式RAND()*(b-a)+a
* `Randbetween`: 返回位于两个指定数之间的一个随机整数。 每次计算工作表时都将返回一个新的随机整数。
* `Average`: 返回参数的平均值（算术平均值）
* `Subtotal`: 返回列表或数据库中的分类汇总。

第六类：日期时间函数

* `Datedif`: 计算两个日期间隔的年数、月数、天数，常用于计算年龄的公式中。
* `Networkdays`: 返回两个日期之间的工作日个数。
* `Now`: 返回当前的日期和时间，每次打开工作表时间会更新。
* `Today`: 返回当前日期，在打开工作簿自动更新日期，常用于计算年龄等。
* `Weekday`: 返回对应日期为一周中第几天
* `Weeknum`: 返回日期的周数
* `Date`: 将三个独立的值合并为一个日期
* `Year / Month / Day`: 参数为日期，分别可以得到年月日信息。
* `Hour / Minute / Second`: 参数为时间，分别可以得到小时、分钟、秒。
* `Time`: 将三个独立的值合并为一个时间，功能类似DATE函数。

第七类：格式显示函数

* `Text`: 将数字按指定方式显示，常和其他函数配合使用，例如合并文本数值，需要数值以特定的格式显示，这时候可以使用TEXT函数
* `Upper / Lower`: 大小写
* `Proper`: 将文本字符串的首字母转换成大写，将其余字母转换为小写。
* `Roud`: 将数字四舍五入到指定的位数。
* `Roudup`: RANDUP语法同RAND，只是采用的使用将数字向上舍入而非四舍五入。
* `Rouddown`: RANDDOWN语法同RAND，只是采用的是将数字向下舍去而非四舍五入。
* `Rept`: 将文本重复指定次数，一般用于在单元格填充文本字符串。
* `Fixed`: 将数字舍入到指定的小数位数，使用句点和逗号，以十进制数格式对该数进行格式设置，并以文本形式返回结果。